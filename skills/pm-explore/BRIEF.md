# Brief template

The brief is the Orkestrr task description. It has two parts:

- **The spec** (top): behavior and interfaces. It stays true while files move, and it is the contract the engineer's agent works from.
- **Exploration notes** (bottom): file paths pinned to a SHA. These are hints, and they go stale. The engineer's agent verifies them before trusting them.

Write the spec as **behavior, not procedure**: say what the system should do, and leave how to the engineer.

## Rules

- **Acceptance criteria are observable.** Each one is independently checkable by a person in the app or by a test. "Works correctly" is not a criterion.
- **Key interfaces use names that survive refactors:** models, serializers, endpoints, components, Celery tasks, permission classes. Paths belong in the exploration notes only.
- **Out of scope** names the adjacent things an agent might be tempted to change.
- **Keep it short.** An engineer should read the spec in under two minutes.

## Template

```markdown
## Summary

One line: what changes, for whom.

**Category:** bug | enhancement
**Risk:** low | elevated (PHI / auth / billing / migration / jobs / infra: say which)

## Current behavior

What happens today. For a bug, the broken behavior and how to reproduce it.

## Desired behavior

What should happen after the change, including edge cases and error states.

## Acceptance criteria

- [ ] AC-1: Given <state>, when <action>, then <observable result>
- [ ] AC-2: ...

## Key interfaces

- `ModelOrComponentName`: what changes and why
- `GET /api/...`: current response vs needed response

## Out of scope

- ...

## Open questions

Decisions left to engineering, each with the option you would lean toward. Omit if none.

---

## Exploration notes (unverified hints)

Gathered at: `<repo>` @ `<branch>` `<short-sha>` on <YYYY-MM-DD>

Likely relevant:

- `path/to/file.py`: why it matters
- `path/to/component.tsx`: why it matters

Similar existing behavior to copy: `<name or path>`

Before implementing, run:
`git diff <short-sha>..HEAD --stat -- <paths above>`
If any listed file changed, re-verify these notes. The spec above still holds either way.
```

Repeat the "Gathered at" line for each repo explored.
