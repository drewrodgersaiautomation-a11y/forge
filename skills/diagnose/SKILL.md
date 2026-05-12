---
name: diagnose
description: Structured debugging with hypothesis-first reasoning and human in the loop. Use when the user is debugging a bug, something is not working, tests are failing unexpectedly, or behavior is wrong. Do not use for building new features. Trigger phrases: "this is broken", "something is wrong", "debug this", "figure out why", "diagnose".
---

# Diagnose

Debug systematically. Do not guess. Do not try random things. Reason about what is happening, form a hypothesis, test it, and update based on evidence.

## Principles

**Hypothesize before acting.** Every change to the code or environment during a debugging session should follow from a hypothesis. "I think X is happening because Y" → "to test this I will Z." Never run a change to "see what happens."

**One variable at a time.** Change one thing, observe the effect, update your model. Changing multiple things simultaneously makes it impossible to know what caused an observed change.

**The bug is in your model.** When behavior is unexpected, it means your mental model of the system is wrong somewhere. The goal is to find where your model is wrong, not to make the symptom go away.

**Human in the loop.** After each diagnostic step, surface the finding and ask before proceeding. The user may know something that shortcuts the investigation.

## Process

### Step 1: Characterize the bug

Before touching anything:

- What is the expected behavior?
- What is the actual behavior?
- Is it deterministic or intermittent?
- When did it start? What changed?
- Is there a minimal reproduction?

If a minimal reproduction does not exist, create one before proceeding. A bug that cannot be reliably reproduced cannot be reliably fixed.

### Step 2: Map the system

Using `CONTEXT.md` vocabulary, trace the code path from the point where the wrong behavior is observed back to its origin. Identify:

- What modules are involved?
- Where are the state changes?
- Where are the external dependencies (database, network, time)?

### Step 3: Form a hypothesis

State the hypothesis explicitly: "I believe the bug is caused by [X] because [Y]. The evidence that would confirm this is [Z]."

Ask the user: "Does this hypothesis seem plausible given what you know? Anything that would rule it out?"

### Step 4: Test the hypothesis

Design the minimal test that would confirm or falsify the hypothesis. This might be:
- Adding a log statement at a specific point
- Writing a unit test that isolates the suspected module
- Checking a specific value in the database
- Running the code with a specific input that should trigger the suspected path

Report the result. Update the hypothesis if it was falsified.

### Step 5: Fix and verify

Once the root cause is confirmed:

1. Fix the root cause — not just the symptom
2. Write a regression test that would have caught this bug (if one doesn't exist)
3. Verify the original reproduction no longer exhibits the bug
4. Check whether the same root cause could exist elsewhere in the codebase

Ask the user: "Should I check for similar patterns elsewhere?"
