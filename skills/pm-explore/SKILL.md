---
name: pm-explore
description: Turn a PM's product request into an engineer-ready Orkestrr task. Use when a PM describes a bug, feature, or change they want built, or asks to explore the codebase before writing a ticket.
---

# PM Explore

A PM describes what they want. You explore the codebase read-only, draft a **brief**, and after the PM approves it, create a draft task in Orkestrr. An engineer picks it up from there.

The PM owns product decisions. You own every fact you can find in the code. Speak to the PM in product language: behavior, users, screens. Keep file names and code out of the conversation unless the PM asks.

This session is **read-only**: read files and run read-only commands (`git`, `grep`, `ls`, `cat`). The one write is step 2's `git checkout main` and `git pull`. Otherwise leave the working tree exactly as you found it: no edits, no commits, no installs.

## Steps

### 1. Intake

Restate the request in one or two sentences: who is affected, what happens now, what should happen instead.

Done when you can state current and desired behavior. If the request is too vague for even that, ask the PM for it in one message and wait.

### 2. Sync and pin the snapshot

For each repo you will explore, before reading any code: `git checkout main`, then `git pull`. If the working tree has uncommitted changes, stop and tell the PM rather than switching branches. Then record the repo name and `git rev-parse --short HEAD`. Every finding in the brief is true as of these SHAs.

Done when every repo you will read is on an up-to-date `main` with a recorded SHA.

### 3. Explore

Find where the behavior lives today: the screens, endpoints, models, serializers, tasks, and permissions involved, and how data flows between them. Look for similar existing behavior the engineer can copy.

Flag **risk** when the change touches any of: patient data (PHI), authentication or permissions, billing or payments, database migrations, background jobs that mutate data, infrastructure.

Done when you can name the key interfaces that must change and the current behavior is confirmed in code, not assumed.

### 4. Check it isn't already done

- **Built:** search the code for the desired behavior by concept, not just by the PM's wording. If it already exists, tell the PM where it shows up in the product and stop.
- **Ticketed:** follow [ORKESTRR.md](ORKESTRR.md) to find the project and goal, then `list_tasks` with a `search` for the concept. If a matching task exists, show it to the PM and ask whether to stop or continue.

Done when both checks are reported to the PM.

### 5. Ask only blocking decisions

Collect questions whose answer changes **what gets built** and that only the PM can answer. Anything engineering can decide goes under "Open questions" in the brief instead.

- Ask **0 to 3** questions, all in one message.
- Give each a recommended answer, so the PM can reply "ok".
- If nothing is blocking, skip straight to the draft.

Done when every blocking question has an answer.

### 6. Draft the brief

Write the brief using [BRIEF.md](BRIEF.md). Show it to the PM along with the target project, goal, and labels.

Done when the PM approves it. Apply edits the PM asks for and show it again.

### 7. Create the task

Follow [ORKESTRR.md](ORKESTRR.md) to create the task as a draft with the brief as its description.

Done when the task exists. Reply with its title and id, and tell the PM an engineer will pick it up from here.
