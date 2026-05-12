---
name: tdd
description: Test-driven development with red-green-refactor loop and vertical slices. Use when building features, fixing bugs, or when the user mentions TDD, red-green-refactor, test-first, or wants integration tests. Do not use for exploratory prototyping.
---

# Test-Driven Development

## Core Principle

Tests verify behavior through public interfaces. The code can change entirely. The tests should not. A test that breaks when you rename an internal function — but behavior hasn't changed — is a bad test.

See [references/philosophy.md](references/philosophy.md) for the full rationale.

## The Only Loop

```
RED:   Write a test for one behavior → it fails
GREEN: Write minimal code to make it pass
REFACTOR: Clean up. Never while RED.
Repeat.
```

This is a vertical slice. One behavior at a time, end to end.

**Do not write all tests first, then all code.** That is horizontal slicing. It produces tests that verify imagined behavior, not actual behavior — because you wrote the tests before you understood the implementation. See [references/anti-patterns.md](references/anti-patterns.md).

## Workflow

### 1. Plan the behaviors

Before writing the first test:

- Confirm with the user what interface changes are needed
- List the behaviors to test — describe them as observable outcomes, not implementation steps
- Identify [deep module](references/deep-modules.md) opportunities: what complexity can be hidden behind a simple interface?
- Get user approval on the list

Ask: "Which behaviors are most important to test? What should the public interface look like?"

You can't test everything. Prioritize critical paths and complex logic over every edge case.

### 2. Tracer bullet

Write ONE test that confirms ONE thing about the system. This proves the test path works end to end before you build out the full suite.

```
RED:   Write test for first behavior → fails
GREEN: Write minimal code → passes
```

### 3. Incremental loop

For each remaining behavior:

```
RED:   Write next test → fails
GREEN: Minimal code to pass → passes
```

Rules:
- One test at a time
- Only enough code to pass the current test
- Do not anticipate future tests
- Tests use public interfaces only — no direct database queries, no private method access, no mocking of internal collaborators

### 4. Refactor

After all tests pass, look for refactor candidates:
- Extract duplication
- Deepen modules: move complexity behind simpler interfaces
- Apply SOLID where it fits naturally — not as a checklist
- Update `CONTEXT.md` if new domain terms emerged during implementation
- Run tests after each refactor step

Never refactor while RED.

## Checklist Per Cycle

```
[ ] Test describes behavior, not implementation
[ ] Test uses public interface only
[ ] Test would survive an internal refactor
[ ] Code is minimal for this test only
[ ] No speculative features added
```

## References

- [Philosophy](references/philosophy.md) — why tests verify behavior, not implementation
- [Mocking](references/mocking.md) — when to mock and when not to
- [Anti-patterns](references/anti-patterns.md) — horizontal slicing, over-mocking, test pollution
- [Deep Modules](references/deep-modules.md) — designing for testability
