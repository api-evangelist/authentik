---
name: authentik-provision-user-access
description: Provision a user in authentik and grant them access to an application through
  group membership, then verify the grant took effect.
api: authentik Core API (/api/v3)
generated: '2026-09-04'
method: generated
source: openapi/_original/authentik-openapi.yml, conventions/authentik-conventions.yml,
  errors/authentik-problem-types.yml
operations:
  - core_users_create
  - core_groups_list
  - core_groups_create
  - core_groups_add_user_create
  - core_applications_list
  - core_users_retrieve
  - core_users_set_password_create
  - core_groups_remove_user_create
---

# Provision a user and grant application access

**Base URL:** `https://{authentik_host}/api/v3` — authentik is self-hosted, so the host is
the operator's own deployment. There is no shared vendor endpoint.

**Auth:** `Authorization: Bearer <token>`. Use an agent account or service-account token
with only the RBAC permissions these operations need. A missing permission returns **403**,
not 401.

## Steps

1. **Confirm who you are acting as.** `GET /core/users/me/` (`core_users_me_retrieve`).
   Record the acting identity — every write below writes a `model_created` /
   `model_updated` event that names it.

2. **Find the target group before creating anything.** `GET /core/groups/?search=<name>`
   (`core_groups_list`). Paging is page-number based: read `pagination.count` and
   `pagination.next` — `next` is a PAGE NUMBER, not a URL, so increment `page` yourself.

3. **Create the group only if it does not exist.** `POST /core/groups/`
   (`core_groups_create`). `name` is unique, so a duplicate POST fails with **400** and a
   `name` array in the body rather than creating a twin. There is no `Idempotency-Key`
   header on this API — do not assume a retried POST is safe on resources without a unique
   constraint.

4. **Create the user.** `POST /core/users/` (`core_users_create`). Required at minimum:
   `username`, `name`. Set `type` to `internal` or `external` deliberately — external users
   are billed differently and cannot reach the application dashboard. Attach arbitrary
   customer data under `attributes`.

5. **Set a password only if the account is meant for interactive login.**
   `POST /core/users/{id}/set_password/` (`core_users_set_password_create`). Skip this for
   service and agent accounts — they have no usable password by design.

6. **Add the user to the group.**
   `POST /core/groups/{group_uuid}/add_user/` (`core_groups_add_user_create`) with the
   user's `pk` in the body.

7. **Verify the application binding actually grants access.**
   `GET /core/applications/` (`core_applications_list`). Access to an application is decided
   by its policy bindings, not by group membership alone — membership only matters if a
   binding references the group.

8. **Confirm.** `GET /core/users/{id}/` (`core_users_retrieve`) and check `groups_obj`.

## Reversal

Membership is fully reversible: `POST /core/groups/{group_uuid}/remove_user/`
(`core_groups_remove_user_create`), no time limit.

**Deleting the user is NOT reversible.** There is no soft delete, no trash and no restore
endpoint anywhere in this API. If the intent is "remove this person", prefer the scheduled
offboarding skill — it is cancellable and audited.

## Errors

| Status | Body | Meaning |
|---|---|---|
| 400 | `ValidationError` — `{<field>: [...], non_field_errors: [...], code}` | Fix the named fields; do not retry unchanged. |
| 403 | `GenericError` — `{detail, code}` | Missing RBAC permission, or a missing/invalid bearer token. |
| 404 | `GenericError` | Not found — or hidden from you by object-level permissions. |

No `429` and no rate-limit headers exist on this API. Back off on `500`.
