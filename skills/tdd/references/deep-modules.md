# Designing for Testability with Deep Modules

## What is a deep module?

A deep module has a **simple interface** and a **complex implementation**. The interface is small relative to the functionality it provides. Callers get a lot of leverage from a little knowledge.

A shallow module has an interface nearly as complex as its implementation. It provides little leverage — you have to understand almost as much to use it as to implement it.

Depth is the property that makes code testable. A deep module:
- Has few entry points to test through
- Hides all the complexity behind those entry points
- Lets you verify a lot of behavior with a few well-chosen tests

## The deletion test

Before building or keeping a module, apply the deletion test: if you deleted this module, would the complexity disappear or would it reappear scattered across its callers?

- **Complexity disappears**: the module was a pass-through. It had no depth. It was a thin wrapper that added indirection without adding leverage. Consider consolidating.
- **Complexity reappears in N callers**: the module was earning its keep. Every caller would have to replicate the logic. The module is deep — it is centralizing complexity that belongs in one place.

## One seam = hypothetical. Two seams = real.

A seam is a place in the design where behavior can be changed without editing code in place. If only one implementation of an interface exists, the seam is hypothetical — useful for testing, but the abstraction may be premature. If two real implementations exist (or are clearly needed), the seam is real — the abstraction is earning its keep.

Don't introduce abstractions speculatively to create testability. Design the module to be deep, and testability will follow naturally from the fact that there is a meaningful interface to test through.

## Designing for testability

When designing a module:

1. Identify what callers need to know (interface) vs. what they should not know (implementation)
2. Push as much as possible into the implementation
3. Make the interface express what the module does, not how it does it
4. The interface should be stable even as the implementation evolves

A module designed this way is testable because:
- There are few entry points to test through
- The entry points represent real behaviors worth testing
- Internal changes don't break the tests
