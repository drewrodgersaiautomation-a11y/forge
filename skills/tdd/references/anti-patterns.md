# TDD Anti-Patterns

## Horizontal slicing

Writing all tests first, then all code.

Why it fails: tests written before implementation verify *imagined* behavior. The structure commits to a design before you understand the problem. When reality differs from imagination, you bend the code to fit tests that are already wrong, or you change the tests (making them post-hoc, not test-first).

The fix: vertical slices. One test → one implementation → repeat.

## Testing implementation, not behavior

Tests that assert on: internal function call counts, private method return values, internal state accessed directly, mock call order.

Why it fails: any refactor breaks the tests, even when behavior is unchanged. Developers learn to fear refactoring. The codebase stiffens.

The fix: tests use only the public interface. Assert on observable outcomes — return values, state changes visible through the interface, side effects visible to callers.

## Over-mocking

Mocking internal collaborators, mocking things that are fast and deterministic, creating extensive mock setups that mirror the real implementation.

Why it fails: the mock becomes a duplicate of the real code. The test verifies that the mock works, not that the system works. When the real implementation changes, the mock doesn't — tests pass but production breaks.

The fix: mock only at seams (external dependencies: database, network, clock). Hand-roll fakes for complex external dependencies. Assert on outcomes, not on how the mock was called.

## Premature abstraction in tests

Introducing test helpers, base classes, or factory abstractions before the duplication clearly exists.

Why it fails: test infrastructure becomes as complex as the production code. Tests are harder to read because you have to understand the abstraction to understand the test.

The fix: duplicate in tests before you abstract. The rule of three: abstract only when you see the same thing three times and the abstraction is obvious.

## Testing multiple behaviors per test

One test verifying three different behaviors, with multiple asserts that each test a different concern.

Why it fails: when the test fails, you don't know which behavior failed. The test becomes hard to name meaningfully.

The fix: one behavior per test, one clear assertion per behavior. The test name IS the specification.

## Writing tests after the fact to hit coverage targets

Tests written after implementation that trace the code path rather than specify behavior.

Why it fails: these tests verify that the code does what the code does, not that the code does what it should. They have no power to catch regressions because they will change whenever the implementation changes.

The fix: coverage is a metric, not a goal. Tests that specify behavior provide coverage as a side effect.
