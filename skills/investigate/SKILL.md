---
name: investigate
description: Search before building. Run a 3-layer knowledge check before implementing anything non-trivial. Use when the user is about to build something that involves unfamiliar patterns, infrastructure choices, library decisions, or any question of "how should we do this?". Trigger phrases: "how should I", "what's the best way to", "should I use", "investigate", "research".
---

# Investigate

Stop before building. Search first. The cost of checking is near-zero. The cost of not checking is reinventing something worse.

## The 3 Knowledge Layers

Every investigation covers three layers, in order:

### Layer 1: Tried and true

What is the standard, battle-tested approach to this problem? What do experienced engineers in this ecosystem reach for first?

Search for: official documentation, well-maintained libraries, framework built-ins, established patterns. The goal is to understand the consensus solution and its reasoning — not to copy it, but to understand what problem it solves and how.

**The risk at Layer 1**: assuming the obvious answer is right without questioning its premises. The canonical approach is often correct. But occasionally, the problem at hand has a characteristic that makes the standard solution wrong. Check the premises.

### Layer 2: New and popular

What is the current best practice? What has shifted in the last 1-2 years that might change the Layer 1 answer?

Search for: recent blog posts from authoritative sources, ecosystem trends, new library versions, deprecations, community discussions. Read critically — the crowd can be wrong, especially in fast-moving areas. Distinguish genuine improvements from hype.

**The risk at Layer 2**: mania. New things attract attention disproportionate to their merit. A library with 10k stars this month may have 3 open security issues and an abandoned maintainer. Scrutinize.

### Layer 3: First principles

Given what you now understand about the problem and the existing solutions, what does reasoning from first principles suggest?

This is not "ignore Layers 1 and 2." It is: having understood what everyone is doing and why, what does the specific shape of *this* problem suggest? Is there a reason to zig while everyone else zags? Is the conventional approach solving a slightly different problem than ours?

The best engineering decisions often come from here: "The standard approach assumes X, but our constraints are Y, therefore we should Z." Name these observations when you find them. They are the most valuable output of the investigation.

## Output Format

Produce a report with three sections:

```markdown
## Investigation: [Topic]

### Layer 1: Tried and true
[What is the established approach? What problem does it solve? What are its trade-offs?]

### Layer 2: Current best practices
[What has shifted recently? What do experienced practitioners recommend today? Any meaningful caveats?]

### Layer 3: First-principles observations
[Given our specific constraints, what does this suggest? Any reason to deviate from the standard path?]

### Recommendation
[What should we do and why? Reference the layer(s) that drove the recommendation.]

### What we're NOT doing and why
[Explicit list of reasonable alternatives that were considered and rejected, with brief rationale.]
```

## When to escalate to an ADR

If the investigation reveals a meaningful architectural trade-off — a decision a future developer might question and re-litigate — propose writing an ADR after the recommendation is accepted.

An ADR is not needed for every investigation. It is needed when the reasoning matters as much as the decision.
