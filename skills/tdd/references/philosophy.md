# TDD Philosophy

## Why tests verify behavior, not implementation

The test suite is a specification, not a mirror of the code. A spec describes what the system does. It does not describe how.

When tests are coupled to implementation — mocking internal collaborators, testing private methods, asserting on specific call counts of internal functions — they create a maintenance trap. Every refactor breaks tests even though nothing externally changed. Developers start dreading refactors. The codebase stiffens.

The fix is simple: tests should only know about the public interface. If you can refactor the entire interior of a module and the tests still pass, those are good tests. If renaming a private function breaks tests, those are bad tests.

**The test reads like a specification:**

Good: `"user can complete checkout with valid cart and payment method"`
Bad: `"PaymentProcessor.validateCard() is called with card number and CVV"`

The good test tells you what the system does. The bad test tells you how it does it — and will break the moment you rename `validateCard`.

## Why vertical slices beat horizontal slices

Horizontal slicing — write all tests, then all code — feels disciplined but produces worse tests. Here's why:

When you write a test before writing the implementation, you are testing *imagined* behavior. You don't yet know what the implementation will look like, what edge cases will emerge, or what the natural interface boundaries are. The tests get committed to a structure that may not match reality.

Then you implement. The reality differs from the imagination. You either change the tests (now they're not really test-first) or you bend the implementation to fit the tests (now the code is worse).

Vertical slicing solves this: you write one test, then the minimal implementation, then the next test. Each test responds to what you just learned. Because you wrote the code, you understand what behavior actually matters. The tests grow organically from real understanding.

The tracer bullet proves the path works. Each subsequent cycle deepens and extends what you know is real.
