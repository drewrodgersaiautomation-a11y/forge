# Mocking Guidelines

## The rule

Mock at seams, not at internals.

A seam is an interface boundary where behavior can be changed without editing the code in place. Mocking at a seam means substituting a real external dependency (database, HTTP client, filesystem, clock) with a controlled fake. Mocking at an internal means substituting something inside the module under test — a private helper, an internal service, a collaborator that the caller should not know about.

**Mock external dependencies. Do not mock internal collaborators.**

## What counts as an external dependency

- Database / ORM
- HTTP clients (outbound requests)
- File system (when non-trivial)
- Clock / time
- External queues or event buses
- Third-party SDKs

These are the right things to stub or fake in tests because they are slow, non-deterministic, or require infrastructure.

## What does NOT warrant a mock

- Internal functions you wrote that the module under test calls
- Internal classes or services that are part of the same module
- Anything that is not at an interface boundary

If you find yourself mocking something internal, it is a signal that the module is too tightly coupled or that the test is testing implementation rather than behavior. The correct fix is to redesign the module, not to add a mock.

## Fakes over mocks

When you do need to substitute an external dependency, prefer a hand-rolled fake over a mock framework where possible. A fake is a simple, correct implementation of the interface with in-memory state. A mock with `expect().toHaveBeenCalledWith()` assertions is testing implementation (how the code called the dependency), not behavior (what the system did). Fakes let you assert on outcomes.

```typescript
// Prefer this (fake)
class InMemoryUserRepository implements UserRepository {
  private users = new Map<string, User>()
  async findById(id: string) { return this.users.get(id) ?? null }
  async save(user: User) { this.users.set(user.id, user) }
}

// Over this (mock)
const mockRepo = { findById: jest.fn(), save: jest.fn() }
expect(mockRepo.save).toHaveBeenCalledWith(expect.objectContaining({ id: '123' }))
```

The fake tests what happened. The mock tests how it happened.
