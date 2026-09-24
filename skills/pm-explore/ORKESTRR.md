# Orkestrr

Tasks are created through the Orkestrr MCP (`orkestrr-mcp`). The hierarchy is Project > Bundle > Goal > Task, and every task lives under an active goal.

If a tool fails with "Not logged in" or "Session expired", ask the PM to run `okr login` and retry.

## Find where the task goes

1. `list_projects(search=...)` to find the project for the product area.
2. `list_goals(project_id=..., status=...)` to list active goals. Pick the one that matches the request.
3. If more than one goal fits, or none does, include the candidates in step 5's questions with your recommendation. Creating goals is the PM's call outside this skill, so leave goals and bundles unchanged.

## Check for duplicates

`list_tasks(project_id=..., search="<concept>")`. Try two or three phrasings of the concept. Summaries are enough to spot a match; use `get_task` to confirm a likely one.

## Labels

`list_labels(project_id=...)` and attach the ones that apply:

- A risk label when the brief's risk is elevated, if the project has one (e.g. `risk:phi`, `risk:auth`).
- `ready-for-agent` for low-risk work an engineer can hand to a coding agent, `ready-for-human` for elevated risk.

Use only labels that already exist. If a useful one is missing, mention it to the PM instead of creating it.

## Create

```
create_task(
  goal_id=<goal>,
  title=<short imperative title>,
  description=<the full brief>,
  status="draft",
  label_ids=[...],
)
```

- Status stays `draft` so an engineer or EM confirms it before it is committed to.
- Set `assigned_to` only when the PM names an engineer. Resolve the name with `list_project_members(project_id=..., search=...)`.
- Acceptance criteria are not writable through the MCP, so they live in the description under "Acceptance criteria".
