---
name: authentik-offboard-user-safely
description: Schedule a user's deactivation or deletion for a future time, with session and
  token revocation, and cancel it before it runs if the decision changes.
api: authentik Lifecycle API (/api/v3)
generated: '2026-09-04'
method: generated
source: openapi/_original/authentik-openapi.yml,
  https://docs.goauthentik.io/sys-mgmt/user-offboarding,
  conventions/authentik-conventions.yml
operations:
  - core_users_list
  - core_users_used_by_list
  - lifecycle_user_offboarding_create
  - lifecycle_user_offboarding_list
  - lifecycle_user_offboarding_destroy
  - core_authenticated_sessions_bulk_delete_destroy
  - events_events_list
---

# Offboard a user safely

**This is the reversible way to remove someone.** `DELETE /core/users/{id}/` is immediate
and permanent; a scheduled offboarding is cancellable right up until it runs, and it leaves
an audit record either way. Prefer this path.

**Auth:** `Authorization: Bearer <token>` with permission over the target user.

## Steps

1. **Preflight the blast radius.** `GET /core/users/{id}/used_by/`
   (`core_users_used_by_list`) — "Get a list of all objects that use this object". This is
   authentik's built-in consequence preview and there is no `dry_run` flag anywhere else in
   the API. Read it before scheduling a `delete` action.

2. **Schedule the offboarding.** `POST /lifecycle/user_offboarding/`
   (`lifecycle_user_offboarding_create`):
   - `action` — `deactivate` (account and data are retained, login is blocked) or `delete`
     (permanent).
   - `scheduled_for` — a future date and time.
   - revoke-sessions and revoke-tokens options — both default on. **Leave them on.**
     Without them, an existing session or API token keeps working after the offboarding runs.

   You cannot schedule an offboarding for your own account or for an internal service
   account, and each user may have only one pending offboarding.

3. **Confirm it is pending.** `GET /lifecycle/user_offboarding/`
   (`lifecycle_user_offboarding_list`). States are `PENDING`, `COMPLETED`, `FAILED`,
   `CANCELED`.

## Cancelling — the reversal window

`DELETE /lifecycle/user_offboarding/{id}/` (`lifecycle_user_offboarding_destroy`).

The contract's own description: *"Cancel a pending offboarding instead of deleting the
record. The row is retained (as `CANCELED`) so the offboarding stays visible in the audit
history."*

**Window:** any time before the scheduled date and time. authentik sweeps for due
offboardings **every five minutes**, so the action normally starts within five minutes after
the scheduled time — a cancellation must land before that sweep. You cannot cancel an
offboarding that targets you.

**After it runs with `action: delete`, there is no restore.** The window closes hard.

## Failure behaviour

If an attempt fails, authentik retries the whole action. After five failed attempts the
record is marked `FAILED` and **changes from failed attempts are rolled back**. Watch for it
with `GET /events/events/?action=user_offboarded` (`events_events_list`).

## Immediate alternative

To cut access now without deleting anything:
`DELETE /core/authenticated_sessions/bulk_delete/`
(`core_authenticated_sessions_bulk_delete_destroy`) — "Bulk revoke all sessions for multiple
users". Session revocation is terminal; the user must re-authenticate.
