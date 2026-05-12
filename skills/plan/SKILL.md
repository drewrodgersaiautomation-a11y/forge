---
name: plan
description: Turn a feature idea into a PRD and issue breakdown before writing any code. Produces user stories, module design with deep module opportunities, testing decisions, and a prioritized issue list. Use when the user wants to plan a feature, start a new project, turn a conversation into a spec, or write a PRD.
---

# Plan

Produce a PRD and issue breakdown from the current context. No code is written during this skill. Planning is complete when the user has signed off on the spec.

## Rules

- Do NOT interview the user. Synthesize from what is already known.
- Use `CONTEXT.md` vocabulary throughout — if a term isn't in CONTEXT.md yet, propose adding it.
- Respect any ADRs in the area you're touching. Do not re-litigate recorded decisions.
- Identify deep module opportunities in the module design section. A deep module has a simple interface and complex implementation. Shallow pass-throughs are not worth building.

## Process

### Step 1: Orient

Read `CONTEXT.md` and any relevant `docs/adr/` files. If they don't exist, run `/init-project` first.

Explore the existing codebase briefly to understand what already exists in the area being planned. Look for: existing modules that will be modified, naming conventions in use, test patterns already established.

### Step 2: Write the PRD

Produce the PRD inline, then ask the user to confirm before proceeding to issues.

---

**PRD Template:**

```markdown
# PRD: [Feature Name]

## Problem Statement

[The problem from the user's perspective. One paragraph. What breaks, what's missing, what's painful.]

## Solution

[The solution from the user's perspective. One paragraph. What will be true after this ships.]

## User Stories

A numbered list. Each story: "As a [actor], I want [feature], so that [benefit]."
Be exhaustive — cover the happy path, edge cases, error states, and admin/operator needs.
A weak PRD has 5 stories. A strong PRD has 20+.

## Module Design

For each module to build or modify:

- **[Module name]** (from CONTEXT.md vocabulary)
  - Interface: [what callers see — inputs, outputs, error modes]
  - Implementation: [what it hides — complexity, side effects, external dependencies]
  - Depth assessment: [is this a deep module? what is it hiding?]
  - Test surface: [what behaviors to test through this interface]

Actively look for opportunities to consolidate shallow modules into deeper ones.

## Implementation Decisions

A list of decisions made. Include:
- Architectural choices and their rationale
- Schema changes
- API contracts
- What is explicitly NOT being done in this iteration, and why

No file paths. No code snippets unless a type shape or state machine encodes a decision
more precisely than prose can.

## Testing Decisions

- What makes a good test for this feature (behavior, not implementation)
- Which modules get tests
- What prior art exists in the codebase for similar tests

## Out of Scope

Explicit list. For each item: what it is and why it's deferred.

## Open Questions

Anything that needs a decision before or during implementation.
```

---

### Step 3: Issue breakdown

After user approves the PRD, break it into issues. Save to `.scratch/` unless the user has GitHub/Linear/etc. configured.

Each issue:
- Title: imperative verb ("Add checkout validation", not "Checkout validation")
- Scope: one cohesive unit of work that can ship independently
- Blocked by: list dependencies explicitly

Present as a table for review:

| # | Title | Depends on | Notes |
|---|-------|------------|-------|
| 1 | ... | — | ... |

### Step 4: Confirm

Ask: "Does this spec match what you want to build? Any issues to add, remove, or reorder?"

Do not start coding until the user confirms.
