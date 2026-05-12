# Engineering Craft — Agent Instructions

This file is the Codex / OpenAI agent equivalent of CLAUDE.md. Load these principles at the start of every session.

---

## Boil the Lake

AI-assisted coding makes the marginal cost of completeness near-zero. When the complete implementation costs minutes more than the shortcut — do the complete thing. Every time.

A "lake" is boilable: 100% test coverage for a module, full feature implementation, all edge cases handled, complete error paths. An "ocean" is not: rewriting an entire platform from scratch, multi-month migrations. Boil lakes. Flag oceans as out of scope.

When evaluating two approaches where A is complete and B covers 90% — choose A. The delta costs seconds with AI. "Ship the shortcut" is legacy thinking from when human time was the bottleneck.

**Anti-patterns:**
- "Choose B — it covers 90% with less code." (If A is 70 lines more, choose A.)
- "Let's defer tests to a follow-up." (Tests are the cheapest lake to boil.)
- "This is too complex." (Say what it would take, then do it.)

---

## Search Before Building

Before building anything involving unfamiliar patterns, infrastructure, or runtime capabilities — stop and search first. The cost of checking is near-zero. The cost of not checking is reinventing something worse.

Three knowledge layers, in order:

1. **Tried and true** — Standard patterns, battle-tested approaches. Check anyway.
2. **New and popular** — Current best practices. Search. Scrutinize. The crowd can be wrong.
3. **First principles** — Original reasoning derived from this specific problem. Prize these above all.

---

## User Sovereignty

Models recommend. Users decide. Generate a recommendation, explain the reasoning, state what context might be missing, then ask. Never act unilaterally on something that changes the user's stated direction.

---

## Deep Modules

Prefer modules with simple interfaces and complex implementations over shallow pass-throughs. Apply the deletion test: if deleting this module concentrates complexity rather than moving it, it's earning its keep.

---

## Test Behavior, Not Implementation

Tests verify what the system does through public interfaces. A test that breaks when you rename an internal function — but behavior hasn't changed — is a bad test. Build vertically: one test → one implementation → repeat.

---

## Skills Reference

This repo includes skills for the following workflows. Invoke by name when the context matches:

| Skill | When to use |
|-------|-------------|
| `init-project` | Starting a new repo — sets up CONTEXT.md, ADRs, issue tracker, git guardrails |
| `plan` | Before writing any feature code — produces a PRD and issue breakdown |
| `tdd` | Building features or fixing bugs — red-green-refactor with vertical slices |
| `architecture` | Reviewing an existing codebase for deep module opportunities |
| `investigate` | Before building anything non-trivial — search the 3 knowledge layers |
| `review` | Before merging — multi-specialist analysis of the diff |
| `handoff` | When context is getting heavy — compact and transfer to a fresh session |
| `zoom-out` | When lost in code — get a module map using domain vocabulary |
| `diagnose` | Debugging — hypothesis-first, human in the loop |
| `ship` | Final pre-merge checklist |
