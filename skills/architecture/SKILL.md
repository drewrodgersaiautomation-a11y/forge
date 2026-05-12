---
name: architecture
description: Find deep module opportunities in an existing codebase. Identifies shallow modules, tightly coupled seams, and untestable interfaces, then proposes concrete refactors. Use when the user wants to improve architecture, reduce coupling, make code more testable, or understand how a codebase fits together.
---

# Architecture Review

Surface architectural friction and propose deepening opportunities — refactors that turn shallow modules into deep ones. The goal is a codebase where complexity is concentrated, interfaces are stable, and tests verify behavior without knowing internals.

## Vocabulary

Use these terms precisely. Inconsistent language is the enemy of good architecture.

- **Module** — anything with an interface and an implementation (function, class, package, file)
- **Interface** — everything a caller must know: types, invariants, error modes, ordering, config
- **Implementation** — the code inside
- **Depth** — leverage at the interface: large behavior behind a small interface
- **Seam** — where an interface lives; where behavior can be changed without editing in place
- **Deletion test** — would deleting this module concentrate complexity or scatter it across callers?
- **Locality** — change, bugs, and knowledge concentrated in one place

Use `CONTEXT.md` vocabulary for domain terms. Use the above vocabulary for architecture.

## Process

### 1. Read domain context

Read `CONTEXT.md` and any `docs/adr/` files before exploring the codebase. The domain language names good seams. ADRs record decisions not to re-litigate.

### 2. Explore for friction

Walk the codebase with an eye for these signals:

- **Shallow modules**: interface nearly as complex as implementation. Little leverage. Often recognizable as thin wrappers, pure delegation, or classes with 1:1 method-to-line ratios.
- **Scattered complexity**: understanding one concept requires bouncing between many small files. Complexity is spread across callers instead of concentrated in a module.
- **Leaky seams**: modules that expose internal details. Callers know too much about how something works.
- **Untestable interfaces**: testing this module requires mocking many internal collaborators, or the public interface is so thin that there's nothing meaningful to test through it.
- **Naming drift**: the same concept is called different things in different parts of the codebase. This is a signal of missing domain language, not just style inconsistency.

Apply the **deletion test** to anything suspicious: would deleting it concentrate complexity, or just move it?

### 3. Present candidates

Present a numbered list. For each candidate:

- **Files involved**
- **Problem**: why is this causing friction?
- **Solution**: plain English — what would change?
- **Benefits**: in terms of locality, leverage, and testability
- **ADR conflict**: if this contradicts an existing ADR, flag it clearly

Do NOT propose interfaces yet. Ask: "Which of these would you like to explore?"

### 4. Design the refactor

Once the user picks a candidate, work through the design:

- What is the new interface? What does a caller need to know?
- What moves into the implementation?
- What tests become possible through this interface that weren't before?
- What tests become unnecessary (implementation details that no longer need testing)?

Side effects as decisions are made:
- **New domain concept?** Add it to `CONTEXT.md`
- **Rejected candidate with a load-bearing reason?** Offer to write an ADR so future reviews don't re-suggest it
- **Two+ real implementations needed?** The seam is real. Otherwise, keep it hypothetical.

### 5. Confirm before implementation

Present the proposed interface and ask for explicit sign-off before writing any code. Architecture decisions made during this skill should be recorded in `docs/adr/`.
