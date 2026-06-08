---
name: synthesize
description: Turn a pile of notes, research findings, or long conversation into a structured, shareable document. Use after /explore, after a long research session, or any time you need to make findings legible to others.
---

# Synthesize

Turn everything we've discussed and researched into a clean, structured document that someone else can read and act on.

---

## Output format

```markdown
# [Topic or Question]

## Summary
[3-5 sentences. What did we find? What should someone know if they only read this section?
The summary should be self-contained — it's the only thing many people will read.]

## Background
[Why this question matters. What triggered this research? What problem does this answer solve?
Keep it brief — 1-2 paragraphs.]

## Findings

### [Finding 1 — give it a descriptive title]
[The finding in plain language. The evidence. The sources. Any important caveats.]

### [Finding 2]
[...]

## Options and tradeoffs
[If this is a decision document, compare the alternatives here.]

| Option | Strengths | Weaknesses | Best when |
|---|---|---|---|
| [A] | | | |
| [B] | | | |

[A short paragraph explaining any tradeoffs that the table doesn't capture.]

## Recommendation
[The recommended path, with clear reasoning. State it directly.
If there's no clear winner, say so explicitly and explain why — don't hedge everything.]

## Open questions
[What we still don't know. What evidence is missing. What would change this recommendation.]

## Sources
[Key sources, with one line describing what each covers and how authoritative it is.]
```

---

## Rules

**Don't pad.** If 3 sentences cover it, use 3 sentences. Longer is not more thorough — it's less useful.

**Don't hedge everything.** State what you actually believe. Note uncertainty where it genuinely exists, not as a reflex.

**Use the project's language.** If `CONTEXT.md` exists, use its terminology throughout.

**Every claim needs grounding.** Either a source, a direct observation, or a clear label of "inference."

**The recommendation must be actionable.** "It depends" is not a recommendation. "We recommend X for our use case because Y, with the caveat that if Z changes, reconsider" is.

---

## Where to save it

- `docs/research/[topic].md` for technical investigations
- `docs/decisions/[topic].md` for decision documents
- `HANDOFF.md` if this is a session summary

After saving, ask: *"Is there anything in the findings that should update `CONTEXT.md` or trigger a new ADR?"*
