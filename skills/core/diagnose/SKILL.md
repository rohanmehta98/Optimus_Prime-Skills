---
name: diagnose
description: Disciplined debugging loop for hard bugs, wrong agent behavior, and performance regressions. Reproduce → minimise → hypothesize → instrument → fix → regression test. Use when a bug resists a quick fix, when an agent consistently misbehaves, or when you're not sure what's wrong.
---

# Diagnose

Follow this loop in order. Do not skip steps. Do not jump to fixes.

---

## Step 1 — Reproduce

Establish a reliable, minimal reproduction. If you cannot reproduce it consistently, you do not understand it yet.

Answer these before moving on:
- What exact input or action triggers it?
- Does it always happen, or only sometimes? (if sometimes — what's different?)
- What is the simplest reproduction case you can construct?
- Can you reproduce it in isolation, without the full application running?

**Do not proceed until you have a reliable reproduction.**

---

## Step 2 — Minimise

Strip the reproduction to its smallest possible form. Remove everything that isn't necessary to trigger the problem.

The smaller the case, the more obvious the cause. A 3-line reproduction is infinitely easier to debug than a 300-line one.

---

## Step 3 — Hypothesize

State a specific, testable hypothesis. Not:
> "Something is wrong with the auth module."

But:
> "I think the token is expiring before the refresh call completes because the timer starts at token creation, not at first use."

Write it down. This forces precision. If you can't write a specific hypothesis, you need more information — go back to Step 2.

---

## Step 4 — Instrument

Add logging, assertions, or probes to prove or disprove the hypothesis. **Do NOT change behavior yet — only observe.**

- What data do you need to see?
- Where do you need to add logging?
- What value would prove the hypothesis true? What would disprove it?

---

## Step 5 — Evaluate

Did the data support your hypothesis?

- **Yes** → proceed to Fix
- **No** → form a new, more specific hypothesis based on what you learned. Return to Step 3.

**Never patch what wasn't the problem.** If your hypothesis was wrong, your fix will be wrong too.

---

## Step 6 — Fix

Make the minimal change that resolves the root cause.

Not a workaround. Not a guard around the symptom. Fix the actual cause.

Remove any instrumentation you added.

---

## Step 7 — Regression test

Write a test that would have caught this bug:
- It must fail without the fix
- It must pass with the fix

This bug should never return silently.

---

## For AI agents specifically

When an agent produces wrong output:

1. **Reproduce** the exact input and context that triggers the bad behavior
2. **Isolate** which step in the pipeline produces wrong output (retrieval? prompt? parsing? tool call? final model?)
3. **Hypothesize** specifically: is the problem in the prompt design? The tool's return format? The parsing logic? State management?
4. **Never "improve the prompt"** without first knowing *why* the current one fails — you'll be guessing

Treat agent misbehavior like any other bug: reproduce it reliably before you try to fix it.
