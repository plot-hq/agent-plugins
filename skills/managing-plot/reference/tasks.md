# Tasks and planning

Read a task before changing it. List area statuses, labels and members when
their identifiers are unknown. Create tasks with a clear name and area; use
Markdown for descriptions. Dates accept Unix seconds or an ISO timestamp with a
timezone.

Patch updates preserve omitted fields. Use `null` only for fields whose tool
schema allows clearing. An explicit label list replaces existing labels; read
and preserve labels that the user did not ask to remove. Priority is a boolean,
not a numeric rank.

`task_create_tree` creates one parent with one level of subtasks through one API
mutation. Optional `ref` names allow `@ref` dependencies inside that payload;
real task handles identify existing tasks. `blockedBy` names prerequisites;
`blocking` names tasks that must wait. Child tasks cannot contain further
subtasks. The API validates inheritance, access, duplicate references and
dependency cycles.

For existing tasks use dependency and parent tools. Do not force a parent's area
or project onto a child unless the user intends that change. Read returned
errors before retrying parent changes.

Multiple independent tool calls are not an atomic batch. Earlier successful
writes remain saved if a later call fails. Report partial success accurately and
read the workspace before retrying uncertain writes.
