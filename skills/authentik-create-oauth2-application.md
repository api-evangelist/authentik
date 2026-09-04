---
name: authentik-create-oauth2-application
description: Create an OAuth2/OIDC provider and its application in authentik, wire the scope
  mappings, and bind an access policy.
api: authentik Providers + Core API (/api/v3)
generated: '2026-09-04'
method: generated
source: openapi/_original/authentik-openapi.yml,
  https://docs.goauthentik.io/add-secure-apps/providers/oauth2/create-oauth2-provider
operations:
  - flows_instances_list
  - propertymappings_provider_scope_list
  - providers_oauth2_create
  - providers_oauth2_list
  - core_applications_create
  - core_applications_retrieve
  - core_applications_used_by_list
  - policies_bindings_create
  - crypto_certificatekeypairs_list
---

# Create an OAuth2 / OIDC application

authentik is **OpenID Certified™** for OpenID Connect. The object model is a *provider* (the
protocol implementation) plus an *application* (the thing users see and policies bind to).
You always create both, in that order.

**Auth:** `Authorization: Bearer <token>`.

## Steps

1. **Pick the authorization flow.** `GET /flows/instances/?designation=authorization`
   (`flows_instances_list`). Record the flow's `pk` — the provider requires it.

2. **Pick the signing key.** `GET /crypto/certificatekeypairs/`
   (`crypto_certificatekeypairs_list`). Needed to sign ID tokens.

3. **Pick the scope mappings.** `GET /propertymappings/provider/scope/`
   (`propertymappings_provider_scope_list`). These are the property mappings that become
   OIDC scopes. Select the `pk` of each scope the client should receive — the defaults cover
   `openid`, `profile` and `email`.

4. **Create the provider.** `POST /providers/oauth2/` (`providers_oauth2_create`). Set
   `name`, `authorization_flow`, `client_type` (`confidential` or `public`),
   `redirect_uris`, `property_mappings` and `signing_key`.

   **Never use a wildcard or a regex-broad `redirect_uris` value.** CVE-2024-21637 in this
   product was exactly that: a permissive redirect URI plus `response_mode=form_post` let an
   attacker capture the session token.

   The response carries the generated `client_id` and, for a confidential client, the
   `client_secret`. Reading it writes a `secret_view` event.

5. **Create the application.** `POST /core/applications/` (`core_applications_create`) with
   `name`, `slug` and `provider` set to the provider's `pk`. **The slug is the application's
   address** — `GET /core/applications/{slug}/` — and it is not a random opaque id.

6. **Bind an access policy or group.** `POST /policies/bindings/`
   (`policies_bindings_create`) with the application as `target`. **Until you do this, who
   can reach the application is governed only by the default policy engine result** —
   binding is what actually restricts access, not group membership on its own.

7. **Verify.** `GET /core/applications/{slug}/` (`core_applications_retrieve`) and
   `GET /core/applications/{slug}/used_by/` (`core_applications_used_by_list`) to see what
   now depends on it.

## Related provider types

Same shape, different endpoint: `providers_saml_create` (SAML 2.0),
`providers_scim_create` (outbound SCIM provisioning), `providers_ssf_create` (Shared Signals
Framework backchannel — Enterprise), plus LDAP, RADIUS, Proxy and RAC.

## Reversal

Deleting a provider or an application is **immediate and permanent** — no undo. Call
`used_by` first. Blueprints
(https://docs.goauthentik.io/customize/blueprints) are the supported way to keep this
configuration reproducible.
