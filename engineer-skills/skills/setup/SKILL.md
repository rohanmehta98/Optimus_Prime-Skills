---
name: setup
description: One-time project initialization. Scans the codebase, creates CONTEXT.md with a domain glossary, and sets up the docs/adr/ directory. Run this before any other skill in a new project. If user says "set up this project", "initialize", or starts a new codebase, run this first.
---

Run this once at the start of a new project or the first time working in an existing one.

## Steps

### 1. Scan the codebase

Read the project structure, key files (`package.json`, `pyproject.toml`, `Makefile`, existing READMEs, etc.), and any existing documentation. Don't ask questions you can answer by looking.

### 2. Ask these questions — one at a time

For each question, give your best guess based on what you've read, then ask to confirm:

1. **What is this project?** (one sentence — what it does, for whom)
2. **Tech stack** — languages, frameworks, key libraries, how it's deployed
3. **Domain terms** — any jargon, abbreviations, or concepts I need to know before working here
4. **Docs location** — where should generated docs be saved? (default: `docs/`)
5. **Issue tracker** — GitHub Issues, Linear, local files, or none?

### 3. Create `CONTEXT.md`

Create at the project root using this format:

```markdown
# Project Context

## What this is
[One paragraph. What it does, who uses it, what problem it solves.]

## Tech Stack
| Layer | Technology | Notes |
|---|---|---|
| Language | | |
| Framework | | |
| Database | | |
| Key libraries | | |

## Domain Glossary
| Term | Definition |
|---|---|
| [Term] | [Precise definition as used in this project — not the general meaning] |

## Key Conventions
[Non-obvious rules: naming patterns, file structure decisions, anything a new dev would get wrong.]

## Out of Scope
[Things this project explicitly does NOT do. Prevents scope creep.]
```

### 4. Create `docs/adr/`

If it doesn't exist:
- Create the directory
- Add `README.md` inside: *"Architecture Decision Records. Created when decisions are hard to reverse, surprising without context, and the result of a real tradeoff."*

### 5. Confirm

Summarize what you set up. List 3 things you're still uncertain about and ask for corrections before we proceed.

---

After setup, every other skill reads `CONTEXT.md` automatically. The time you invest here pays off in every future session.
