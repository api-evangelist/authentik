---
name: authentik-agent-account-token
description: Issue a scoped, expiring API token for an automation or AI agent in authentik,
  delegate time-boxed access to it, and revoke that access.
api: authentik Core + RBAC + Requests API (/api/v3)
generated: '2026-09-04'
method: generated
source: openapi/_original/authentik-openapi.yml,
  https://docs.goauthentik.io/users-sources/user/account-types/agent-accounts,
  https://docs.goauthentik.io/users-sources/user/account-types/service-accounts
operations:
  - core_users_me_retrieve
  - core_users_create
  - core_tokens_create
  - core_tokens_view_key_retrieve
  - core_tokens_list
  - core_tokens_destroy
  - rbac_permissions_list
  - rbac_roles_create
  - rbac_roles_add_user_create
  - requests_grant_requests_agent_create
  - requests_grant_requests_revoke_destroy
  - events_events_list
---

# Issue and govern an agent's API token

This is the flow authentik itself recommends for non-human identity. Its position, stated on
its own blog: agents should use scoped API tokens and RBAC — the same guardrails a human
gets — rather than a separate bridge.

**Auth:** `Authorization: Bearer <token>` as a user who may create accounts and tokens.

## Steps

1. **Establish the acting identity.** `GET /core/users/me/` (`core_users_me_retrieve`).

2. **Create the account.** `POST /core/users/` (`core_users_create`) with the service-account
   user type. An **agent account** is a service account that acts on behalf of a parent
   user: generated username, no usable password, an API token for Bearer auth, configurable
   policy inheritance, and audit events that name the parent user. (Agent accounts are an
   Enterprise feature, introduced in release 2026.8.)

   A self-service agent created by the parent always expires, always uses the deployment's
   default token duration, and always uses `NONE` policy behaviour — it copies no access
   from its parent.

3. **Scope the permissions before issuing the credential.**
   `GET /rbac/permissions/` (`rbac_permissions_list`) to enumerate what exists, then
   `POST /rbac/roles/` (`rbac_roles_create`) and
   `POST /rbac/roles/{uuid}/add_user/` (`rbac_roles_add_user_create`). Grant only the
   objects and actions the agent's task needs. A denial surfaces as **403**.

4. **Create the token.** `POST /core/tokens/` (`core_tokens_create`). Set `expiring: true`
   and an explicit `expires`. The default is 360 days — for an agent, choose far shorter.

5. **Read the secret exactly once.** `GET /core/tokens/{identifier}/view_key/`
   (`core_tokens_view_key_retrieve`). Store it in a secret manager. This call writes a
   `secret_view` event naming the caller.

6. **Delegate additional access time-boxed, not permanently.**
   `POST /requests/grant-requests/agent/` (`requests_grant_requests_agent_create`) —
   *"Delegate access an agent's owner already holds to the agent, time-boxed."* The agent may
   only ask for what its owner already has, so the owner's approval is the whole decision.
   The response carries a `fulfill_url` the agent hands to its owner.

## Revocation — the reversal path

- **End a delegated grant:** `DELETE /requests/grant-requests/{uuid}/revoke/`
  (`requests_grant_requests_revoke_destroy`) — *"Immediately end an active grant. Available
  to the same reviewers who could approve it in the first place."* Available for as long as
  the grant is active; grants also expire on their own.
- **Destroy the token:** `DELETE /core/tokens/{identifier}/` (`core_tokens_destroy`).
  Immediate and permanent — reissue, do not restore.

## Audit

`GET /events/events/` (`events_events_list`). Relevant actions: `secret_view`,
`secret_rotate`, `model_created`, `model_updated`, `model_deleted`,
`access_request_created`, `access_request_approved`, `access_request_revoked`. Every event
identifies the acting principal and, for an agent, its parent user.

## Cautions

- There is **no `Idempotency-Key` header** on this API. A retried `POST /core/tokens/`
  creates a **second token** — tokens carry no unique-name constraint that would stop it.
  Track the identifier you got back rather than retrying blind.
- CVE-2024-37905 in this product was a permission-check gap that let any authenticated user
  create a token and reassign its owner to escalate to superuser. Keep the deployment
  patched and keep agent RBAC narrow.
