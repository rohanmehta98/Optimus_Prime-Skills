---
name: zoom-out
description: Step back and explain code in the context of the whole system. Use when lost in implementation details, before making a large change, when something "feels wrong" but you can't say why, or when reviewing unfamiliar code.
---

Zoom out. Don't explain this code in isolation — explain it in the context of the whole system.

Cover all of these:

**1. What it is**
The purpose of this code in plain language. What job does it do?

**2. Where it fits**
- What calls this code? (upstream)
- What does this code call? (downstream)
- What other modules depend on it?
- What would break if this were deleted?

**3. Why it exists**
What problem was it solving when it was written? (Infer from context, comments, git history if available, and the domain model in `CONTEXT.md`.)

**4. What's working well**
What about this code is genuinely good? What should be kept and not touched?

**5. What feels wrong**
Anything that looks overly complex, misplaced, inconsistent with the rest of the system, or likely to cause problems. Be specific — not "it's messy" but "this function is doing three unrelated things and the third one belongs in the auth module."

---

After covering all five points, ask:

*"Given this context — does the change you were planning still make sense? Or does seeing the full picture suggest a different approach?"*
