---
name: architect
description: Review the current codebase architecture, identify structural problems, and propose concrete improvements. Run once a week or whenever the codebase feels hard to change. Informed by CONTEXT.md and ADRs. Never refactors without confirmation.
---

# Architect

Perform an architectural review. Find the problems. Propose the fixes. Do not change anything without explicit confirmation.

---

## Step 1 — Read the domain model

If `CONTEXT.md` exists, read it. If `docs/adr/` exists, read any recent ADRs. Understand the *intended* design before evaluating the *actual* one. Note any gaps between the two.

---

## Step 2 — Map the structure

Walk the codebase and build a system map:
- What are the major modules, layers, or services?
- What are the main data flows?
- Where are the system boundaries?
- What are the key interfaces between parts?

Summarize this as a short text map — not a diagram, just a clear description. Confirm it's accurate before proceeding.

---

## Step 3 — Find the problems

Look specifically for:

**🪨 Ball of mud** — modules doing too many things. Files over ~300 lines where responsibilities are mixed. Functions that take many parameters and do unrelated things.

**🪟 Shallow modules** — complex interfaces that don't hide much. The ideal is the opposite: a simple interface with deep implementation (hides complexity, easy to use).

**🗣️ Inconsistent language** — names that conflict with `CONTEXT.md`, or the same concept called different things in different places. This confuses both humans and agents.

**🕸️ Hidden dependencies** — code that reaches across module boundaries without going through the public interface. Global state. Implicit coupling that makes changes unpredictable.

**💀 Dead code** — unused functions, imports, commented-out blocks that have been there long enough to become noise.

**📋 Missing abstractions** — the same pattern copy-pasted in three places, waiting to be extracted into a shared function.

**🚪 Wrong boundaries** — a module that knows too much about another module's internals. Logic that clearly belongs somewhere else.

---

## Step 4 — Prioritize

Rank findings by: *how much does this make the codebase harder to change?*

Not aesthetics. Not style preferences. Actual friction — things that have caused or will cause bugs, confusion, or slow development.

Label each finding:
- **High** — actively causing problems or will soon
- **Medium** — worth fixing, not urgent
- **Low** — nice to clean up eventually

---

## Step 5 — Propose

For each significant finding, provide:
1. **What the problem is** — specifically, not "it's messy"
2. **Why it matters** — the actual consequence
3. **Concrete steps to fix it** — ordered, actionable
4. **Whether it warrants an ADR** — if yes, offer to write one

**Do not touch any code in this step.** Present all findings first, get confirmation on what to fix and in what order, then proceed.

---

## After the review

Ask: *"Which of these do you want to address first?"*

Then use `/tdd` to make changes safely with tests before and after.
