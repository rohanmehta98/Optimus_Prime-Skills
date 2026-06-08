---
name: handoff
description: Compress the current session into a structured handoff document so another agent (or a future session) can continue without losing context. Use before ending any session, when hitting a context limit, or when switching between tools.
---

Create a handoff document for this session. It must be self-contained — someone with zero context should be able to read it and pick up exactly where we left off.

## Document format

```markdown
# Handoff — [Project Name] / [Date]

## What we were doing
[One paragraph. The goal of this session. Why we started it. What we were trying to achieve.]

## What we decided
[Every significant decision made this session. Include the reasoning — not just the conclusion.
Format: "We decided to [X] because [Y]. We rejected [Z] because [W]."]

## What we built or changed
[Every file created or modified, with a one-line description of the change.]

| File | Change |
|---|---|
| path/to/file | What was done and why |

## Current state
[Is it working? Partially working? Broken? What is the exact state of the code right now?
Be specific — "the tests pass but the UI integration isn't done" is useful. "In progress" is not.]

## Next steps
[Ordered list. What should be done next, in priority order. Each item should be independently actionable.]

1. [Most important next action]
2. [...]

## Blockers and open questions
[Anything unresolved that the next session needs to address before moving forward.]

## Context and watch-outs
[Non-obvious context: quirks of this codebase, temporary decisions that will need revisiting, things to be careful about, anything a fresh agent would get wrong.]
```

## Where to save it

- `HANDOFF.md` at the project root (good for single active handoffs)
- `docs/handoffs/YYYY-MM-DD.md` (good if you want to keep a history)

## After saving

Tell me the full path and confirm: *"Ready to continue in a new session."*
