# 🛠️ Engineer Skills

> The complete AI skill kit for engineers who work across fullstack, Python, agents, and research — in one place.

Built by combining the best ideas from [Andrej Karpathy's LLM coding guidelines](https://x.com/karpathy/status/2015883857489522876) and [Matt Pocock's engineer skills](https://github.com/mattpocock/skills), then extended specifically for AI engineers working across multiple domains.

**The problem these solve:**

- 🤯 Agent doesn't do what you wanted → run `/grill` first, every time
- 💩 Code works but it's becoming a mess → `/architect` to find and fix it
- 🐛 Bug that won't yield → `/diagnose` for a disciplined loop
- 🤖 Building an AI agent → `/agent-design` before you write a tool
- 🔬 Research task → `/explore` + `/synthesize`
- 🔄 Context window filling up → `/handoff` to continue seamlessly

---

## Install

```bash
npx skills@latest add your-username/engineer-skills
```

**Or** drop `CLAUDE.md` into any project root to get the behavioral rules alone — no setup required.

---

## Which skills do I need?

Pick your current situation:

### 🌐 Building a Fullstack / Web App
```
1. /setup          ← run once per project
2. /grill          ← before every non-trivial feature
3. /tdd            ← while building
4. /diagnose       ← when something breaks
5. /architect      ← once a week, keep the codebase clean
```

### 🐍 Python / Backend Service
```
1. /setup
2. /grill
3. /plan           ← for features touching multiple files
4. /tdd
5. /diagnose
```

### 🤖 Building an AI Agent or LLM Workflow
```
1. /agent-design   ← design the system before writing code
2. /grill          ← stress-test your design
3. /prompt-craft   ← write reliable prompts
4. /tdd            ← build with tests
5. /eval           ← build an eval harness before shipping
6. /diagnose       ← when the agent misbehaves
```

### 🔬 Research / Technical Investigation
```
1. /explore        ← research the topic systematically
2. /synthesize     ← turn findings into a shareable document
3. /grill          ← stress-test your conclusions
```

### 🔄 Any situation — session continuity
```
/handoff           ← before ending any session
/zoom-out          ← when you're lost in the details
```

---

## Skill Reference

### 🔧 Setup
| Skill | When to use |
|---|---|
| [`/setup`](./skills/setup/SKILL.md) | Once per project. Scans codebase, creates `CONTEXT.md`, prepares `docs/adr/` |

### 🎯 Core — Use Every Day
| Skill | When to use |
|---|---|
| [`/grill`](./skills/core/grill/SKILL.md) | Before building anything non-trivial. Forces alignment before a line is written |
| [`/tdd`](./skills/core/tdd/SKILL.md) | Red-green-refactor loop. One vertical slice at a time |
| [`/diagnose`](./skills/core/diagnose/SKILL.md) | Hard bugs. Reproduce → minimise → hypothesize → instrument → fix |
| [`/handoff`](./skills/core/handoff/SKILL.md) | End of session. Compresses context so next session continues cleanly |
| [`/zoom-out`](./skills/core/zoom-out/SKILL.md) | When you're lost in details. Explains code in the full system context |

### 🌐 Fullstack
| Skill | When to use |
|---|---|
| [`/plan`](./skills/fullstack/plan/SKILL.md) | Turns a vague feature into a PRD with vertical-slice tasks |
| [`/architect`](./skills/fullstack/architect/SKILL.md) | Finds architecture problems. Run weekly |

### 🤖 Agents & AI
| Skill | When to use |
|---|---|
| [`/agent-design`](./skills/agents/agent-design/SKILL.md) | Design a new agent system — goal, tools, loop, evals |
| [`/prompt-craft`](./skills/agents/prompt-craft/SKILL.md) | Write and stress-test a prompt with examples and adversarial inputs |
| [`/eval`](./skills/agents/eval/SKILL.md) | Build a repeatable eval harness before shipping |

### 🔬 Research
| Skill | When to use |
|---|---|
| [`/explore`](./skills/research/explore/SKILL.md) | Research a topic — map known/unknown, find best options |
| [`/synthesize`](./skills/research/synthesize/SKILL.md) | Turn research findings into a structured, shareable document |

---

## The Behavioral Backbone — `CLAUDE.md`

Every skill in this repo builds on top of `CLAUDE.md`. It's always active and contains five rules that address the most common AI engineering failure modes:

1. **Think Before Touching Anything** — state assumptions, surface tradeoffs, ask when confused
2. **Minimum Viable Code** — nothing speculative, nothing you didn't ask for
3. **Surgical Changes Only** — touch only what the task requires
4. **Define Done Before You Start** — verifiable goals, not vague instructions
5. **Use the Project's Language** — `CONTEXT.md` is the shared glossary; use it

These are distilled from Karpathy's observations on LLM coding pitfalls and Pocock's shared-language techniques.

---

## Templates

- [`templates/CONTEXT.md`](./templates/CONTEXT.md) — project glossary template (copy to project root)
- [`templates/ADR.md`](./templates/ADR.md) — architecture decision record template

---

## Philosophy

**From Andrej Karpathy:**
> "LLMs are exceptionally good at looping until they meet specific goals. Don't tell them what to do — give them success criteria and watch them go."

**From Matt Pocock:**
> "A shared language pays off session after session: variables and files are named consistently, the codebase is easier to navigate, and the agent spends fewer tokens on thinking."

The best insight from both: **the way you set up the agent matters more than the agent itself.** These skills are the setup.

---

## Contributing

These skills are designed to be hacked. Each skill is a single `SKILL.md` file — fork it, adapt it, improve it. PRs welcome.

If you build a skill for a specific domain (mobile, data engineering, DevOps), open a PR and we'll add it.

---

MIT License
