---
name: grill
description: Relentless clarifying interview before any work starts. Forces alignment before a single line of code is written. Use before every non-trivial task — feature, refactor, system design, or major decision. Trigger when user says "grill me", "stress-test this plan", "I want to build X", or starts describing something to build.
---

Interview me relentlessly about every aspect of this plan until we reach complete shared understanding. Walk down each branch of the decision tree, resolving one dependency at a time.

For each question:
1. Give your recommended answer first, based on what you know.
2. Ask me to confirm, correct, or build on it.
3. Wait for my response before moving to the next question.

Never ask more than one question at a time. Never batch questions.

If any question can be answered by exploring the codebase, explore it instead of asking.

---

## Domain awareness

If `CONTEXT.md` exists at the project root, read it before we start.

**Challenge conflicting terms.** When I use a term that conflicts with the glossary, call it out immediately:
> "Your glossary defines 'cancellation' as X, but you seem to mean Y — which is right?"

**Sharpen fuzzy language.** When I use vague or overloaded words, propose a precise canonical name:
> "You said 'account' — do you mean Customer or User? Those are different things in your domain."

**Stress-test with concrete scenarios.** Don't let abstract plans stay abstract. Invent specific edge cases to force precision:
> "What happens if the user is offline when this fires?"
> "What if two users trigger this simultaneously?"
> "What's the correct behavior when the input is empty?"

**Cross-reference with the code.** When I describe how something works, check whether the codebase agrees. Surface contradictions immediately:
> "You said partial cancellation is possible, but the code only cancels entire Orders — which should win?"

**Update `CONTEXT.md` live.** When we agree on a new term or refine an existing one, update `CONTEXT.md` right then. Don't batch updates. Capture decisions as they're made.

**Offer ADRs for hard decisions.** If we make a decision that is hard to reverse, surprising without context, and the result of a real tradeoff — offer to write an ADR. Don't offer for every decision.

---

## End of session

Before stopping:
1. Write a one-paragraph summary of every significant decision we made.
2. List any open questions that still need an answer.
3. Ask: *"Ready to build?"*

Only proceed after I confirm.
