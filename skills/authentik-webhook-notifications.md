---
name: authentik-webhook-notifications
description: Route authentik events to an external webhook receiver by creating a
  notification transport, customizing its body, binding a rule, and testing delivery.
api: authentik Events + Property Mappings API (/api/v3)
generated: '2026-09-04'
method: generated
source: openapi/_original/authentik-openapi.yml,
  https://docs.goauthentik.io/sys-mgmt/events/event-actions,
  asyncapi/authentik-events-webhooks.yml
operations:
  - propertymappings_notification_create
  - events_transports_create
  - events_transports_list
  - events_transports_test_create
  - events_rules_create
  - policies_all_list
  - events_events_list
  - crypto_certificatekeypairs_list
---

# Send authentik events to a webhook

authentik publishes **no AsyncAPI document**. Its outbound event surface is the notification
transport: an operator-configured webhook fired by a rule that matches an event.

**Auth:** `Authorization: Bearer <token>`.

## Steps

1. **Decide which events matter.** The event catalogue is fixed and enumerated in the
   contract (`components.schemas.EventActions`). High-signal actions:
   `login`, `login_failed`, `password_set`, `secret_view`, `secret_rotate`,
   `impersonation_started`, `user_offboarded`, `access_request_approved`,
   `access_request_revoked`, `model_created`, `model_updated`, `model_deleted`,
   `system_exception`, `configuration_error`.

2. **Shape the payload (optional).** `POST /propertymappings/notification/`
   (`propertymappings_notification_create`) — an expression returning JSON-serializable data
   becomes the request body. Without one, authentik sends its default event envelope:
   `pk`, `user {pk, email, username}`, `action`, `app`, `context`, `client_ip`, `created`,
   `expires`, `brand`.

3. **Pin the receiver's TLS certificate (optional).**
   `GET /crypto/certificatekeypairs/` (`crypto_certificatekeypairs_list`) — the resulting
   `pk` goes in `webhook_ca` so authentik validates the receiver's certificate.

4. **Create the transport.** `POST /events/transports/` (`events_transports_create`):
   - `mode` — one of `local`, `webhook` (generic JSON POST), `webhook_slack`
     (Slack/Discord-compatible), `email`.
   - `webhook_url` — the receiver.
   - `webhook_mapping_body` — the mapping from step 2.
   - `webhook_ca` — the CA from step 3.

5. **Test before binding.** `POST /events/transports/{uuid}/test/`
   (`events_transports_test_create`). This is a real delivery to your receiver, not a
   simulation — point it at a test endpoint first.

6. **Create the rule.** `POST /events/rules/` (`events_rules_create`), naming the transport
   and the group to notify. Bind a policy (usually an Event Matcher policy — see
   `policies_all_list`) so only the actions you chose in step 1 fire it.

7. **Verify.** `GET /events/events/` (`events_events_list`) to correlate what authentik
   recorded with what your receiver got.

## What the docs do NOT promise

No signing scheme, no retry policy and no delivery guarantee is documented for notification
transports. **Do not assume replay protection.** Make your receiver idempotent on the
event `pk`, which is a UUID and stable per event.

## The standards-based alternative

For security signals specifically, authentik also acts as an **OpenID Shared Signals
Framework (SSF) transmitter**, pushing Security Event Tokens to a subscribed receiver
(`providers_ssf_create`, `ssf_streams_list`). Signals covered include MFA device added or
removed, logout, session revoked and credentials changed. Enterprise tier. If your receiver
already speaks SSF/CAEP, prefer it — no bespoke connector is needed.
