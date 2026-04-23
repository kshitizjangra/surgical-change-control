---
name: surgical-change-control
version: 1.0.0
description: Use this skill when making fixes, edits, updates, or modifications to an existing system, file, workflow, document, configuration, prompt, automation, interface, or structured asset where unrelated working parts must remain unchanged. This skill enforces minimal, targeted changes, explicit scope control, user confirmation for ambiguous or multi-location edits, and precise placement guidance for every proposed modification.
---

# Surgical Change Control

## Purpose

This skill ensures that when a user asks for a change, only the necessary parts are modified.

Its goal is to prevent:
- unnecessary rewrites
- accidental breakage
- regressions in working areas
- over-application of similar changes
- vague outputs that do not clearly say where the change belongs

This skill treats already-working areas as protected by default.

## Core Principle

Change only what is necessary.  
Protect everything else unless the user explicitly approves a wider scope.

Do not assume that every similar section, repeated pattern, or related file should also be changed.

Do not convert a targeted change into a broad rewrite.

## When to Use

Use this skill when the task involves changing an existing thing rather than creating something entirely from scratch.

Examples:
- fixing a bug
- updating a prompt
- changing workflow logic
- editing an automation
- modifying a configuration
- revising a document section
- changing UI text in selected places
- updating multiple related files with controlled scope
- patching a process without redesigning the whole system

Use this especially when:
- most of the system already works
- only part of it should change
- there are repeated or similar sections
- there is risk of touching the wrong place
- the user wants reviewable, controlled changes

## Protected-by-Default Rule

Anything not clearly required for the requested change is out of scope.

Treat these as protected unless explicitly approved:
- working functionality
- unrelated sections
- adjacent logic
- neighboring text
- formatting not relevant to the task
- naming conventions
- file structure
- workflow steps outside the requested change
- existing outputs that still satisfy the requirement

If something appears old, messy, repetitive, or non-ideal but is not part of the requested change, leave it alone unless the user asks for cleanup.

## Required Operating Mindset

Act like a careful maintainer, not an eager rewriter.

Priorities:
1. accuracy of the requested change
2. minimal blast radius
3. preservation of working behavior
4. clear change boundaries
5. explicit user approval before expanding scope

Optimize for stability and control over elegance and over-improvement.

## Required Workflow

### 1. Understand the requested change

First identify:
- what the user wants changed
- what should remain unchanged
- what is currently working
- what success looks like
- whether the request is narrow or broad

Do not begin changing things until the requested scope is understood.

### 2. Define the change boundary

Determine the smallest valid scope needed to complete the request.

Possible boundaries may include:
- one sentence
- one paragraph
- one section
- one prompt block
- one config field
- one step in a workflow
- one function
- one component
- one file
- a user-approved list of locations across multiple files or systems

Clearly distinguish:
- in-scope areas
- out-of-scope areas
- uncertain areas that require confirmation

### 3. Inspect before changing

Review the relevant locations first.

Before making a change, identify:
- what is actually wrong or needs updating
- the likely root cause or reason for the mismatch
- the smallest effective modification
- whether the same requested change appears in multiple places

Do not perform a rewrite before understanding the local context.

### 4. Detect repeated or multi-location impact

If the requested change appears to affect:
- multiple places in one file
- multiple sections in one document
- repeated steps in one workflow
- multiple files
- multiple prompts
- several similar components
- several possible candidate locations

then stop and identify the candidate change points before proceeding.

Do not automatically change all matching or similar-looking occurrences.

### 5. Ask for scope confirmation when needed

If more than one plausible target exists, ask the user to confirm the exact locations that should be changed.

For each candidate location, specify:
- item name or file name
- section, block, function, step, component, or heading
- why it appears relevant
- whether it seems required, optional, or related but not certain

**Do not proceed until the user confirms scope.**

Proceed only within the user-approved scope.

### 6. Apply the smallest effective change

Once the scope is confirmed, make only the minimum necessary change.

Prefer:
- localized edits
- direct replacements
- narrow insertions
- small patches
- preserving surrounding structure

Avoid:
- broad rewrites
- opportunistic refactoring
- style cleanup not requested
- changing all similar patterns by default
- restructuring content or systems unless required

### 7. Verify scope discipline

After making the change, confirm:
- the requested issue is addressed
- unrelated working areas remain unchanged
- no extra locations were modified without approval
- no nearby content was unnecessarily rewritten
- the result matches the user-approved scope

### 8. Report clearly

When presenting the output, explain:
- what was changed
- where it was changed
- why that location was chosen
- what was intentionally left unchanged
- whether any additional related locations were detected but not modified

## Change Scope Confirmation

When the requested fix, edit, or update may apply to multiple plausible locations, do not proceed silently.

You must first present the possible change targets and ask for confirmation.

This applies to:
- one file with multiple matching sections
- one document with repeated phrases or policies
- one workflow with repeated steps
- multiple files with related logic or content
- several prompts with similar instructions
- config values repeated in more than one place
- templates reused across systems
- any situation where “all matches” might be unsafe

### Confirmation format

Use this default format whenever scope confirmation is needed:

- Candidate 1: `item or file name` — `exact section/block/step`
  - Why relevant: brief reason
  - Change type: direct / related / optional

- Candidate 2: `item or file name` — `exact section/block/step`
  - Why relevant: brief reason
  - Change type: direct / related / optional

Then ask:

Please confirm which candidates should be changed.  
If you want, I can proceed with only the explicitly approved locations.

### Default rule

If the scope is ambiguous:
- ask first
- do not assume
- do not bulk-edit by similarity
- do not expand from one approved location to several unapproved ones

## Scope Expansion Rule

If a new location is discovered during implementation and it was not part of the approved scope, stop before changing it.

Explain:
- what additional location was found
- why it may also need a change
- what could happen if it is left unchanged
- whether it is required or optional

Then ask for confirmation before proceeding.

## Exact Placement Rule

Every proposed change must include precise placement guidance.

Do not give floating output that forces the user to guess where it belongs.

For each modification, specify:
- the target item or file
- the exact section, block, heading, field, step, component, function, paragraph, or area
- the change type: add, replace, remove, update, move, or insert
- the placement instruction:
  - before what
  - after what
  - inside what
  - between which two existing parts
  - replacing which exact existing part

### Examples of acceptable placement guidance

- Add this inside the “Validation Rules” section after the email rule and before the password rule.
- Replace the second paragraph under “Refund Policy.”
- Update only the `timeout` field in the configuration block.
- Insert this step between “Review Submission” and “Send Confirmation.”
- Add this note at the end of the onboarding checklist.
- Change the CTA text only in the homepage hero section, not in footer banners.
- Update the repeated instruction only in the user-facing prompt, not in the internal system prompt.
- Add this under the “Constraints” heading as a new bullet.
- Replace the branch that handles failed approval status and leave all success branches untouched.

### If output is separated into multiple snippets

If the output is split into multiple parts, label each part clearly with:
- where it belongs
- whether it is required or optional
- whether it replaces existing content or is inserted newly
- the exact local context for placement

### If placement is unclear

If exact placement cannot be determined confidently:
- do not invent a location
- do not present vague instructions as if they are precise
- show the most likely candidate insertion points
- ask the user to confirm the intended one

## Minimal Change Standard

Before making any change, test it against these questions:

- Is this directly required for the user’s requested change?
- Is there a smaller change that would work?
- Am I touching something that currently works?
- Am I changing this because it is necessary, or because I think it looks better?
- Would this still be valid if the user wanted the narrowest possible edit?
- Did the user explicitly approve this location?

If the answer creates doubt, reduce scope or ask before proceeding.

## Allowed vs Disallowed Behavior

### Allowed behavior

- patching one broken step without redesigning the whole workflow
- changing selected text in approved sections only
- updating one field in a config instead of replacing the entire config
- modifying one prompt block without rewriting all prompts
- editing one repeated occurrence only after user confirmation
- proposing candidate change locations before making a multi-location update
- adding exact insertion guidance for every snippet

### Disallowed behavior

- rewriting a whole system for a small requested change
- updating all similar occurrences automatically
- changing nearby content “for consistency” without approval
- cleaning up unrelated sections while making the fix
- renaming things that were not part of the request
- changing structure, order, or style without necessity
- giving detached output without saying where it belongs
- silently expanding from one approved location to multiple locations
- assuming repeated content must all be updated the same way

## Decision Policy

When several valid solutions exist, choose the one that:
1. satisfies the request
2. touches the fewest locations
3. preserves the most existing behavior
4. is easiest to review
5. has the lowest regression risk

If a larger change would be cleaner but a smaller one solves the problem safely, prefer the smaller one.

## Communication Requirements

When returning the result, include:
- Requested change: what the user wanted
- Approved scope: what locations were included
- Changes made: exact places modified
- Placement details: where each change belongs
- Unchanged by design: what was intentionally left untouched
- Pending optional locations: any related places found but not changed

If no changes were made because scope was ambiguous, say so clearly and ask for confirmation.

## Default response template

Use this structure when the task requires confirmation before proceeding:

Requested change:
- [brief statement of the requested update]

Current safe scope assessment:
- I found [N] candidate locations that may need modification.

Candidates:
- Candidate 1: [item/file] — [section/block/step]
  - Why relevant: [brief reason]
  - Change type: direct / related / optional

- Candidate 2: [item/file] — [section/block/step]
  - Why relevant: [brief reason]
  - Change type: direct / related / optional

Recommended minimum scope:
- [the smallest likely safe scope]

Please confirm which candidates should be changed.
I will proceed only with the explicitly approved locations.

## Review Checklist

Before finalizing, confirm all of the following:
- The requested change is understood
- The smallest valid scope was chosen
- No unrelated working area was modified
- Multi-location changes were not applied without confirmation
- Every change includes exact placement guidance
- Every separated snippet is labeled with destination and purpose
- Scope was not silently expanded mid-task
- The output is reviewable and easy to apply
- Working parts remain protected

## Example: Bad behavior

The user asks to change one approval message in a workflow.

Bad response:
- updates all approval messages across every workflow
- rewrites related notification text for consistency
- changes naming in nearby steps
- provides one new block without saying where it goes

Why this is bad:
- scope expanded without approval
- unrelated working content changed
- repeated patterns were bulk-edited by assumption
- placement is unclear

## Example: Good behavior

The user asks to change one approval message in a workflow.

Good response:
- identifies that the same message exists in 4 places
- lists all 4 candidate locations
- asks the user which ones should change
- after confirmation, updates only the approved locations
- states exactly where each revised message belongs
- leaves the rest untouched

Why this is good:
- scope is confirmed first
- changes are controlled
- placement is explicit
- working areas are preserved

## Example: Good placement output

- `workflow-approval.yaml` — `Rejected Status Handler`
  - Action: replace
  - Replace the message text inside the rejection notification block only

- `user-guide.md` — `Approval Outcomes` section
  - Action: insert
  - Add the new explanatory note after the paragraph describing rejection reasons

- `Prompt: Reviewer Response Template`
  - Action: update
  - Replace only the final fallback line, leave the rest of the template unchanged

## Anti-Patterns

Avoid these anti-patterns:
- “I updated all similar occurrences.”
- “I also cleaned up a few nearby things.”
- “I refactored it while I was there.”
- “Here is the new content,” without placement details
- “This should probably go somewhere in the validation section.”
- “I assumed all matching templates needed the same update.”
- “I changed the structure to make it better,” when the user asked for a targeted fix

## Summary Rule

Make the smallest approved change that fully solves the request.

Protect what already works.  
Ask before expanding scope.  
Show exactly where every change belongs.
