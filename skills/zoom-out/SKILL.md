---
name: zoom-out
description: Get a module map of an unfamiliar area of code using the project's domain vocabulary. Use when the user is lost in a codebase, needs to understand how modules fit together, or says "I don't understand how this works", "show me the big picture", "map this out", or "zoom out".
disable-model-invocation: true
---

I don't know this area well. Stop going deeper. Go up a layer of abstraction.

Give me a map of:
- The relevant modules and what each one does (one sentence, using CONTEXT.md vocabulary)
- The key callers and what they need from each module
- The data flow through this area — what goes in, what comes out, what changes state
- Any seams (interface boundaries) where behavior could be changed without editing code in place
- Any obvious shallow modules (thin pass-throughs that add indirection but no depth)

Use the domain vocabulary from `CONTEXT.md`. If a concept doesn't have a name yet, flag it as a gap in the domain glossary.

Do not write any code. Do not propose changes. Just map what exists.
