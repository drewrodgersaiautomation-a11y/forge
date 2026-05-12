---
name: grill
description: Deep clarification session before building. Asks targeted questions to surface misalignment, unclear requirements, and hidden complexity before any code is written. Use when the user has a vague idea, wants to think something through, or says "I want to build X" without a clear spec. Do not use after /plan has already been run.
---

# Grill

Ask the questions that would change what gets built. Nothing else.

## Rules

- Maximum 30 questions total. No exceptions.
- Only ask a question if the answer would materially change the design, scope, or implementation approach.
- Do not ask questions whose answers are obvious from context.
- Do not ask questions out of thoroughness — ask out of genuine uncertainty.
- Group related questions together. Never ask one question per message — batch them.
- Stop when you have enough to hand off to `/plan`. That is the exit condition.

## What makes a good grill question

A good question surfaces something that, if left unasked, would cause the wrong thing to get built. Examples:

- "Who is the user — a developer or an end user? This changes the entire interface design."
- "Does this need to work offline? That rules out approach A entirely."
- "Is this a one-time migration or an ongoing sync? The architecture is completely different."
- "What does failure look like — silent, logged, or user-visible?"

A bad question is one where any reasonable answer leads to the same design:
- "Do you want the button to be blue or green?" (irrelevant to architecture)
- "Should we use tabs or spaces?" (pre-commit handles this)
- "Would you like good error messages?" (obviously yes)

## Process

### Step 1: Orient

Read `CONTEXT.md` if it exists. Explore the codebase briefly if this is an existing project. The goal is to understand what is already decided so you don't ask about it.

### Step 2: Identify genuine unknowns

Before asking anything, identify the decisions that are actually open. Think through:

- **Users** — who uses this, in what context, with what expectations?
- **Scope** — what is explicitly in and out?
- **Failure modes** — what happens when things go wrong?
- **Scale** — does volume or frequency change the approach?
- **Integration** — what does this touch, and what are those systems' constraints?
- **Success** — how will we know this worked?

From this list, select only the questions where the answer changes the design. Discard the rest.

### Step 3: Ask in batches

Group questions by theme and ask them together. A session should have 2–4 rounds of questions at most, not 30 individual messages.

Present questions clearly numbered so the user can answer by number.

### Step 4: Synthesize

After each round, summarize what you now know and what is still open. When you have enough clarity to write a solid PRD, say so and offer to run `/plan`.

Do not keep asking questions past the point of diminishing returns. If you've asked 20 questions and the remaining unknowns are low-stakes, make a reasonable assumption, state it explicitly, and move on.

## Hard limit

If you reach 30 questions without hitting the exit condition, stop. State what assumptions you are making for the remaining unknowns and hand off to `/plan` with those assumptions documented.
