---
name: agent-design
description: Design an AI agent system end-to-end before writing a single line of code — defining the goal, tools, loop structure, failure modes, and evaluation criteria. Use before building any agent, LLM workflow, multi-agent system, or AI-powered feature.
---

# Agent Design

Design before you build. A well-designed agent is built around a clear goal, minimal tools, and measurable success criteria. A poorly-designed one is prompts and prayers.

Work through these steps in order. Ask one question at a time. Give your recommended answer first.

---

## Step 1 — Define the goal

Answer these precisely:

1. **What is this agent's job in one sentence?**
   Be specific. "Write emails" is not a goal. "Draft personalized cold outreach emails for a SaaS product given a target company name and a product description" is a goal.

2. **What are the inputs?**
   What does the agent receive at the start? What format? What constraints?

3. **What is the output?**
   What does the agent produce when it's done? What format? What does a good one look like?

4. **How do you know it did a good job?**
   This is your eval. If you cannot answer this, you are not ready to build yet.

---

## Step 2 — Define the tools

For each tool the agent will use:

| Question | Answer |
|---|---|
| What does it do? | (plain language) |
| Inputs | (typed, precise) |
| Outputs | (typed, precise) |
| Failure modes | (what can go wrong) |
| When NOT to use it | (constraints the agent must respect) |

**Rule:** Keep tools as simple functions. If a "tool" itself needs to call an LLM, it might be a sub-agent — name it as one and design it separately.

**Warning sign:** An agent with more than 7-8 tools is usually an agent that should be split into smaller agents with clearer responsibilities.

---

## Step 3 — Choose the loop architecture

Pick the simplest architecture that solves the problem:

| Pattern | When to use |
|---|---|
| **Single pass** | Input → agent → output. No loops. Best for most cases. |
| **ReAct loop** | Agent needs tool results to decide next steps. Think → act → observe → repeat. |
| **Parallel agents** | Multiple independent tasks can run simultaneously |
| **Orchestrator + specialists** | Genuinely different capabilities required. Not just "seems powerful." |

**Justify your choice.** Don't default to multi-agent because it sounds more sophisticated. Complexity has a cost — harder to debug, harder to eval, harder to improve.

---

## Step 4 — Map the failure modes

For each component, ask: *What happens when this goes wrong?*

- What if the LLM refuses or goes off-topic?
- What if a tool returns empty results?
- What if a tool call fails or times out?
- What if the agent loops without making progress?
- What if the output is malformed or unparseable?

Define the intended behavior for each case. *Silent failure is not acceptable.*

---

## Step 5 — Define the eval before building

Before writing a single line of code:

- **3 examples of ideal output** — what you'd be proud to ship
- **3 examples of acceptable output** — good enough, not perfect
- **3 examples of unacceptable output** — would fail, would embarrass

This forces precision about your actual standard. If you can't write these examples, you don't know what you're building yet.

---

## Next steps after design

- `/grill` — stress-test the design with harder questions
- `/prompt-craft` — write and refine the agent's system prompt
- `/tdd` — build the implementation with tests
- `/eval` — build the evaluation harness
