---
name: eval
description: Build a repeatable evaluation harness for any agent or LLM-powered feature. Defines what good output looks like, creates a labeled test set, and sets up automated scoring. Use before shipping any agent or AI feature to production.
---

# Eval

You cannot improve what you cannot measure. Before shipping, build an eval.

"It looks good in testing" is not an eval. An eval is a repeatable process with a score.

---

## Step 1 — Define what good looks like

For this agent or feature, write:

**5 ideal outputs** — the gold standard. What you'd be proud to ship.

**5 acceptable outputs** — good enough, but not perfect. You'd ship these.

**5 unacceptable outputs** — would fail. You would not ship these. Would embarrass you.

This forces precision about your actual standard. If you can't produce 15 examples, you don't know your standard yet — go back to `/agent-design`.

---

## Step 2 — Choose an eval strategy

| Type | Use when |
|---|---|
| **Exact match** | Output is deterministic: parsing, extraction, formatting, classification |
| **Rubric scoring** | Output requires human judgment: tone, quality, completeness, helpfulness |
| **LLM-as-judge** | Too many outputs to score manually; deterministic criteria are clear |
| **Functional test** | Output is code, a query, or a structured artifact that can be executed |

Most production agents need more than one type. State which you'll use and why.

---

## Step 3 — Build the test set

Create a labeled dataset of inputs with expected outputs (or rubric criteria).

Minimum structure:
```
evals/
├── README.md       ← what this eval tests and how to interpret scores
├── cases.json      ← the test cases
└── run_eval.py     ← the scoring script
```

Minimum distribution:
- **10 easy cases** — should always pass. If these fail, something is broken.
- **10 medium cases** — current capability should handle these. Track regression here.
- **5 hard cases** — likely to fail for now. These are your improvement target.

Format for `cases.json`:
```json
[
  {
    "id": "case-001",
    "category": "easy",
    "input": { ... },
    "expected": "...",
    "notes": "Why this case is included"
  }
]
```

---

## Step 4 — Build the scoring script

Write a script that:
1. Loads the test set
2. Runs the agent on each input
3. Scores each output against the expected result or rubric
4. Reports: overall pass rate, per-category pass rate, individual failures with reasons

Even a 50-line Python script counts. The goal is repeatability — run it in under 60 seconds, get a clear score.

```python
# Minimum structure for run_eval.py
def run_eval(cases, agent_fn, score_fn):
    results = []
    for case in cases:
        output = agent_fn(case["input"])
        score = score_fn(output, case["expected"])
        results.append({
            "id": case["id"],
            "passed": score["passed"],
            "score": score["value"],
            "output": output,
            "reason": score.get("reason")
        })
    
    passed = sum(1 for r in results if r["passed"])
    print(f"Pass rate: {passed}/{len(results)} ({passed/len(results):.0%})")
    
    failures = [r for r in results if not r["passed"]]
    for f in failures:
        print(f"FAIL {f['id']}: {f['reason']}")
    
    return results
```

---

## Step 5 — Set a baseline and document it

Run the harness now. Record:

```markdown
## Eval Baseline — [Date]

**Model:** [model name and version]
**Pass rate:** [X/N (Y%)]
**Easy cases:** [X/10]
**Medium cases:** [X/10]
**Hard cases:** [X/5]

**Known gaps in test set:**
- [What's not covered yet]

**Agreement:** No change to this agent may be shipped that regresses below this baseline without explicit discussion.
```

Every future change to the agent or prompt should be run against this harness before merging.
