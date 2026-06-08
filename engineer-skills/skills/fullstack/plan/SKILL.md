---
name: plan
description: Turn a vague feature idea into a concrete PRD with independently-buildable vertical-slice tasks. Use before building any feature that touches more than one file or system boundary. Pairs well with /grill (run grill first) and /tdd (run tdd after).
---

# Plan

Turn what we've discussed into a structured plan — a PRD with tasks that can each be built and tested independently.

---

## Step 1 — Clarify scope

Before writing anything, ask these (one at a time, your recommended answer first):

1. **User outcome** — What can a user do after this ships that they couldn't before? (One sentence. If you can't answer this, the feature isn't defined yet.)
2. **Modules touched** — Which parts of the codebase does this change? Be specific: files, services, database tables.
3. **Explicit out-of-scope** — What is this feature deliberately NOT doing?
4. **Acceptance criteria** — How do we know it's done? What can we test or verify?
5. **Dependencies** — What has to exist before we can build this?

Read `CONTEXT.md` if it exists. Use the domain language throughout the PRD.

---

## Step 2 — Write the PRD

```markdown
# PRD: [Feature Name]

## Problem
[What problem does this solve? For whom?]

## Outcome
[What can users do after this ships that they couldn't before?]

## Scope
**In scope:**
- [...]

**Out of scope:**
- [...]

## Acceptance Criteria
- [ ] [Specific, testable criterion — not "works correctly" but "user can create an account with email and password"]
- [ ] [...]

## Modules touched
- [Module / file / service — and what changes]

## Open questions
[Anything that still needs a decision before building starts]
```

---

## Step 3 — Break into vertical slices

Each task must:
- Be independently buildable and testable
- Deliver a usable slice of value end-to-end (not "build the DB schema" — but "user can save a draft")
- Have a clear, specific done criterion

```markdown
## Tasks

### Task 1 — [Slice name]
**Done when:** [specific, testable criterion]
**Touches:** [files or modules]
**Depends on:** [previous task number, if any]

### Task 2 — [Slice name]
**Done when:** [...]
**Touches:** [...]
```

---

## Step 4 — Confirm

Present the PRD and task list. Ask:
- Does this match what you had in mind?
- Are any tasks too big to build in one session? (If yes, split them.)
- Any open questions that would block starting?

Only proceed after confirmation.
