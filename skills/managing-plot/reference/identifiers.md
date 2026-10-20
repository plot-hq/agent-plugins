# Identifiers and pagination

Prefer friendly handles over internal UUIDs:

| Entity   | Handle                    | Example                        |
| -------- | ------------------------- | ------------------------------ |
| Task     | pathId                    | ENG-042                        |
| Area     | publicId                  | ENG                            |
| Project  | publicId or full slug     | checkout-redesign-apa7eb8jlkwh |
| Document | publicId or full slug     | launch-plan-78utu4m1d7iz       |
| User     | username, with optional @ | @alex                          |

UUIDs remain accepted. Copy handles exactly from responses; task `pathId`,
entity `publicId`, search `handle`, and user `username` are reusable. API `id`
may be an internal UUID. Never construct a UUID or resolve a handle by guessing
a name.

Some inputs require UUIDs: task-list `status`, task-write `labelIds`, and
comment `parentId`. Copy these from status, label, or comment list responses.
Status names are accepted for task-write `statusId` when an explicit area is
supplied, not for the task-list status filter. New area `publicId` values
require exactly three ASCII letters.

A Plot URL has `/{workspaceSlug}/{entityType}/{identifier}` after its host.
Extract the workspace and identifier from those segments. Compare the workspace
with `whoami` before reading or writing. A different workspace requires
reconnecting; passing its slug into a tool does not switch authorization.

Use `limit` (1–100 for most lists, 1–50 for search) and `cursor` from the
preceding page. `offset` is available where the API supports it. Do not combine
a cursor from one filter with different filters. Lists of statuses and labels
are area-specific.

On a 404, verify the handle and workspace. On a 403, verify membership and OAuth
scopes. On a 401, reconnect. On a 429, honor Retry-After. Validation errors
require corrected input rather than repeated calls.
