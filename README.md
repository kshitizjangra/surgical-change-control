# surgical-change-control

> **A precision skill for AI agents that enforces minimal, targeted changes — protecting everything that already works.**

---

## What It Does

`surgical-change-control` is a behavioral skill for AI agents. When applied, it enforces a strict discipline of **change only what is necessary** — nothing more, nothing less.

It prevents:

- Unnecessary rewrites of working systems
- Accidental breakage of unrelated logic
- Regressions introduced by over-eager refactoring
- Vague outputs that don't say where changes belong
- Silent scope expansion across similar-looking sections

Instead, it enforces:

- Surgical, localized edits with exact placement guidance
- User confirmation before touching multiple locations
- A protected-by-default policy for everything not explicitly in scope
- Clear reporting of what was changed, where, and why

---

## Core Principle

> Change only what is necessary. Protect everything else unless the user explicitly approves a wider scope.

The skill treats already-working areas as **protected by default**. It does not assume that fixing one place means fixing all similar places.

---

## When to Use

Use this skill whenever the task involves **modifying an existing thing** rather than creating something from scratch.

### Ideal use cases:

| Scenario | Example |
|---|---|
| Bug fixing | Patching one broken step without redesigning the workflow |
| Prompt editing | Updating one instruction block, leaving others untouched |
| Config changes | Modifying one field without replacing the entire config |
| Document revision | Editing one section without reformatting the whole doc |
| UI text updates | Changing CTA text in one location, not globally |
| Workflow logic | Updating one branch without touching success paths |
| Multi-file patches | Controlled updates across approved files only |
| Automation edits | Modifying one node in a flow without redesigning it |

### Use this especially when:

- Most of the system already works
- Only a specific part should change
- There are repeated or similar patterns that could be mistakenly bulk-edited
- There is risk of touching the wrong place
- The user wants reviewable, controlled changes

---

## How It Works

The skill enforces an 8-step workflow:

1. **Understand the requested change** — Identify what should change and what should not
2. **Define the change boundary** — Determine the smallest valid scope
3. **Inspect before changing** — Review the target location before modifying anything
4. **Detect multi-location impact** — Identify if the change affects multiple places
5. **Ask for scope confirmation** — If multiple candidates exist, confirm with the user before proceeding
6. **Apply the smallest effective change** — Make only the minimum necessary edit
7. **Verify scope discipline** — Confirm unrelated areas remain untouched
8. **Report clearly** — Explain what changed, where, and what was intentionally left alone

---

## What It Protects (By Default)

Anything not explicitly required for the requested change is **out of scope** and treated as protected:

- Working functionality
- Unrelated sections or files
- Adjacent logic or neighboring text
- Formatting not relevant to the task
- Naming conventions and file structure
- Workflow steps outside the requested change
- Existing outputs that still satisfy the requirement

---

## Allowed vs Disallowed Behavior

### Allowed
- Patching one broken step without redesigning the whole workflow
- Changing selected text in approved sections only
- Updating one field in a config instead of replacing the entire config
- Modifying one prompt block without rewriting all prompts
- Proposing candidate change locations before making a multi-location update
- Adding exact insertion guidance for every snippet

### Disallowed
- Rewriting a whole system for a small requested change
- Updating all similar occurrences automatically
- Changing nearby content "for consistency" without approval
- Cleaning up unrelated sections while making the fix
- Giving detached output without saying where it belongs
- Silently expanding from one approved location to multiple locations

---

## Scope Confirmation Format

When a change could apply to multiple locations, the skill pauses and asks:

```
Requested change:
- [brief statement of the requested update]

Current safe scope assessment:
- I found [N] candidate locations that may need modification.

Candidates:
- Candidate 1: [file] — [section/block/step]
  - Why relevant: [brief reason]
  - Change type: direct / related / optional

- Candidate 2: [file] — [section/block/step]
  - Why relevant: [brief reason]
  - Change type: direct / related / optional

Recommended minimum scope:
- [the smallest likely safe scope]

Please confirm which candidates should be changed.
```

---

## Placement Guidance Standard

Every proposed change includes **exact placement instructions**. No floating output that makes the user guess where it belongs.

Examples of valid placement guidance:
- _Add this inside the "Validation Rules" section after the email rule and before the password rule._
- _Replace the second paragraph under "Refund Policy."_
- _Update only the `timeout` field in the configuration block._
- _Insert this step between "Review Submission" and "Send Confirmation."_
- _Change the CTA text only in the homepage hero section, not in footer banners._

---

## Anti-Patterns This Skill Prevents

- `"I updated all similar occurrences."`
- `"I also cleaned up a few nearby things."`
- `"I refactored it while I was there."`
- `"Here is the new content"` — without placement details
- `"I assumed all matching templates needed the same update."`
- `"I changed the structure to make it better"` — when a targeted fix was requested

---

## Decision Policy

When multiple valid solutions exist, this skill chooses the one that:

1. Satisfies the request
2. Touches the fewest locations
3. Preserves the most existing behavior
4. Is easiest to review
5. Has the lowest regression risk

> If a larger change would be cleaner but a smaller one solves the problem safely — prefer the smaller one.

---

## Repository Structure

```
surgical-change-control/
├── skill.md       # Full skill definition and behavioral rules
├── README.md      # This file
└── LICENSE        # MIT License
```

---

## License

MIT License. See [LICENSE](./LICENSE) for details.
