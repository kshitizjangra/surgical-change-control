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
- Confident claims based on unverified assumptions

Instead, it enforces:

- Surgical, localized edits with exact placement guidance
- User confirmation before touching multiple locations
- A protected-by-default policy for everything not explicitly in scope
- Clear reporting of what was changed, where, and why
- **Verification before confidence** — no assumption is treated as fact

---

## Files in This Repo

| File | Description |
|---|---|
| [`skill.md`](./skill.md) | Original skill definition with core surgical change control rules |
| [`updated_skill.md`](./updated_skill.md) | **Latest version** — includes all original rules + new Verification Before Confidence layer |
| [`README.md`](./README.md) | This file |
| [`LICENSE`](./LICENSE) | MIT License |

> Use `skill.md` for the most complete and up-to-date version of this skill.

---

## How to Use This Skill File

You can drop `updated_skill.md` directly into any AI agent, MCP server, or prompt system that supports skill/instruction files.

### In Claude (via MCP or system prompt)

Paste the contents of `updated_skill.md` into your system prompt or MCP skill loader:

```
https://raw.githubusercontent.com/kshitizjangra/surgical-change-control/main/updated_skill.md
```

### In n8n / automation workflows

Fetch the raw file at workflow start and inject it as a system instruction into your LLM node:

```
GET https://raw.githubusercontent.com/kshitizjangra/surgical-change-control/main/updated_skill.md
```

### In any MCP-compatible server

Load `updated_skill.md` as a skill resource. The frontmatter metadata block at the top of the file is already formatted for MCP skill ingestion:

```yaml
name: surgical-change-control
version: 1.0.0
description: Use this skill when making fixes, edits, updates, or modifications...
```

### In Perplexity / Comet

Paste the raw contents of `updated_skill.md` into your assistant's instruction context or use it as a connector skill payload.

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
- The agent must not guess or assume platform/tool behavior

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

## Verification Before Confidence (New in `updated_skill.md`)

This is the key new layer added in `updated_skill.md`. The skill now enforces that **no uncertain information is presented as confirmed fact**.

### Confidence Classification

Before making a claim or recommendation, the agent must classify it:

| Level | Meaning |
|---|---|
| **Verified** | Directly confirmed from reliable context or evidence |
| **Likely** | Strongly inferred but not directly confirmed |
| **Unverified** | Plausible but not confirmed |
| **Unknown** | Not enough information available |

Only **Verified** information is presented as definitive. Everything else must be clearly labelled.

### Assumption Check Rule

Before making or recommending a change, the agent checks if the change depends on any assumption — such as:

- Assuming a platform supports a feature
- Assuming a file is the correct source of truth
- Assuming a setting controls behavior globally
- Assuming repeated content should all be updated consistently

If yes — the assumption is validated first, or clearly stated before proceeding.

### Double-Check Trigger

An extra verification step is automatically triggered when:

- The answer includes platform capabilities, limitations, or behavior
- The scope decision depends on how a tool or system actually behaves
- The recommendation could become wrong if one factual detail is incorrect
- The agent feels confident but has not actually verified the critical point

### Communication Rule for Uncertainty

Good:
- _"This appears to be supported, but I have not verified it yet."_
- _"I believe this is correct, but this should be confirmed before applying the change."_

Bad:
- _"This definitely works like this"_ — when not verified
- _"All of these should be changed"_ — without confirming the dependency

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
- Labelling uncertain claims before presenting them

### Disallowed
- Rewriting a whole system for a small requested change
- Updating all similar occurrences automatically
- Changing nearby content "for consistency" without approval
- Presenting inferred information as confirmed fact
- Silently expanding from one approved location to multiple locations

---

## Scope Confirmation Format

When a change could apply to multiple locations, the skill pauses and presents:

```
Requested change:
- [brief statement of the requested update]

Candidates:
- Candidate 1: [file] — [section/block/step]
  - Why relevant: [brief reason]
  - Change type: direct / related / optional

Recommended minimum scope:
- [the smallest likely safe scope]

Please confirm which candidates should be changed.
```

---

## Anti-Patterns This Skill Prevents

- `"I updated all similar occurrences."`
- `"I also cleaned up a few nearby things."`
- `"I refactored it while I was there."`
- `"Here is the new content"` — without placement details
- `"This definitely works like this"` — when not verified
- `"I assumed all matching templates needed the same update."`

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

## License

MIT License. See [LICENSE](./LICENSE) for details.
