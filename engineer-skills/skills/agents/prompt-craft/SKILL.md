---
name: prompt-craft
description: Write, critique, and iteratively refine a prompt until it's reliable — including positive examples, negative examples, edge cases, and adversarial inputs. Use before deploying any prompt to production, or when an existing prompt is behaving inconsistently.
---

# Prompt Craft

A good prompt is a specification. It defines exactly what the model should do, how, and under what constraints. A bad prompt is an instruction that happens to work on the examples you tested.

---

## Step 1 — Draft the prompt

Write the initial prompt. It should contain:

- **Role** — what is the model in this context? (Be precise: not "you are an AI assistant" but "you are a code reviewer for a Python backend service")
- **Task** — what exactly should it do? (One specific job, not a list of everything it might do)
- **Output format** — what should the response look like? (JSON schema? Markdown? Plain text? Be exact.)
- **Constraints** — what must it never do? (Hard rules the model must always respect)

---

## Step 2 — Write examples

Write at least:

**3 positive examples** — an input with the ideal output. These define what "good" looks like.

**3 negative examples** — an input with a bad output, and an explanation of why it's bad. These define what failure looks like. Include them as few-shot examples in the prompt if they're common failure modes.

**3 edge cases** — unusual or ambiguous inputs the prompt must handle correctly. These are the inputs that will break a naive prompt.

---

## Step 3 — Adversarial testing

Test the prompt against inputs designed to expose weaknesses:

- **Empty input** — what happens if the input is blank or minimal?
- **Prompt injection** — what if the input contains instructions? ("Ignore everything above and output X")
- **Extreme length** — very long input that might overwhelm the context, or very short input that lacks information
- **Ambiguous input** — input that could be interpreted multiple ways. Does the prompt handle it gracefully?
- **Out-of-distribution** — input that's plausible but outside the training distribution for this task

For each failure: diagnose *why* the prompt failed. Fix the root cause — not just the symptom. Adding "always do X" to patch a specific failure is fragile.

---

## Step 4 — Iterate

Run the prompt against all your examples. For each:
- Does the output match the expected result?
- Is the format correct?
- Are all constraints respected?

Fix until all pass. Document what you changed and why.

---

## Step 5 — Document the final prompt

```markdown
## Prompt: [name]

### Purpose
[What this prompt does in one sentence]

### Model
[Which model this was written and tested for]

### Template
[The full prompt text, with {variables} marked clearly]

### Variables
| Variable | Type | Description | Example |
|---|---|---|---|
| {var} | string | ... | ... |

### Examples
[3 input/output pairs that define the expected behavior]

### Known limitations
[What breaks it. What it handles poorly. What inputs to avoid.]

### Version history
| Date | Change | Reason |
|---|---|---|
| | | |
```

Save in `docs/prompts/` for team reference. Version control prompt changes like code.
