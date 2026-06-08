---
name: tdd
description: Test-driven development with a strict red-green-refactor loop. One vertical slice at a time. Use when building features, fixing bugs, or any time you want test-first development. Works for any language or framework.
---

# Test-Driven Development

## Core philosophy

Tests verify behavior — not implementation. A good test survives a complete internal rewrite. A bad test breaks when you rename a private function.

**Good test:** exercises a real code path through the public interface. Reads like a specification. *"User can checkout with a valid cart"* tells you what capability exists. Passes or fails based on observable behavior.

**Bad test:** mocks internal collaborators, tests private methods, or verifies through back-channels (querying a database directly instead of using the API). If your test breaks when you refactor but behavior hasn't changed — it was testing implementation, not behavior.

---

## Never slice horizontally

**Do NOT write all tests first, then all implementation.**

```
WRONG — horizontal slicing:
  RED:   test1  test2  test3  test4  test5
  GREEN: impl1  impl2  impl3  impl4  impl5

RIGHT — vertical slicing:
  RED → GREEN:  test1 → impl1
  RED → GREEN:  test2 → impl2
  RED → GREEN:  test3 → impl3
```

Horizontal slicing produces bad tests. You end up testing the *shape* of imagined code before you understand it. Vertical slicing means each test responds to what you actually learned from the previous cycle.

---

## Workflow

### Step 1 — Plan

Before writing anything:

- If `CONTEXT.md` exists, read it. Test names and interface vocabulary should match the domain language.
- Confirm with user: which behaviors need tests? (You can't test everything — prioritize.)
- Design the public interface for testability first.
- List behaviors to test — not implementation steps.
- Get user approval on the list before writing any code.

Ask: *"What should the public interface look like? Which behaviors are most important to verify?"*

### Step 2 — Tracer bullet

Write ONE test for the most critical, end-to-end behavior. Make it fail. Write the minimum code to make it pass. This is your tracer bullet — it proves the path works.

### Step 3 — Incremental loop

For each remaining behavior:

```
RED:   Write the next test → it must fail
GREEN: Write minimal code to make it pass → it must pass
```

Rules (no exceptions):
- One test at a time. Never batch.
- Only enough code to pass the current test.
- Do not anticipate future tests.
- If you notice something to improve — wait for the Refactor step.

### Step 4 — Refactor

After all tests are green:
- Remove duplication
- Move complexity behind simpler interfaces (deep modules)
- Apply patterns only where they emerge naturally
- Run tests after every individual refactor step

**Never refactor while RED. Get to green first.**

---

## Checklist — per cycle

```
[ ] Test describes behavior, not implementation
[ ] Test uses only the public interface
[ ] Test would survive a full internal refactor
[ ] Code is minimal — just enough to pass this test
[ ] No speculative features or abstractions added
```

---

## Language-specific notes

**Python:** Use `pytest`. Prefer integration tests over unit tests for agent/LLM code.

**TypeScript/JS:** Use `vitest` or `jest`. Test through the public API, not through module internals.

**Any LLM-based feature:** Write a test that captures the input and expected output format *before* writing the prompt. This is your behavioral spec.
