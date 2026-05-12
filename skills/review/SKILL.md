---
name: review
description: Multi-specialist code review before merging. Runs parallel analysis passes for security, performance, maintainability, API contracts, and test coverage, then aggregates findings by severity. Use before any merge, when the user asks for a code review, or after a significant feature is complete.
---

# Code Review

Run specialist analysis across the diff before it merges. Each specialist looks at one dimension only — no overlap, no gaps.

## Specialists

Five reviewers, each with a single mandate:

| Specialist | Mandate |
|---|---|
| **Security** | Injection vectors, authentication gaps, authorization bypass, secrets in code, input validation failures |
| **Performance** | N+1 queries, missing indexes, unbounded loops, blocking I/O in hot paths, memory leaks |
| **Maintainability** | Shallow modules, scattered complexity, naming drift, missing `CONTEXT.md` terms, skipped ADRs |
| **API Contracts** | Breaking changes, missing error modes, undocumented invariants, inconsistent response shapes |
| **Test Coverage** | Behaviors present in the diff with no corresponding test, tests that test implementation not behavior |

## Process

### Step 1: Identify the diff

If a specific set of files or a PR is not named, identify what changed by examining recent commits or the current working diff.

### Step 2: Run all five specialists in parallel

For each specialist, analyze the diff through that specialist's lens only. Write up findings independently. Do not blend concerns — a security finding is a security finding, not also a maintainability note.

Each finding must include:
- **Severity**: Critical / High / Medium / Low
- **Location**: file and line range
- **Problem**: what is wrong and why it matters
- **Fix**: the concrete change required

### Step 3: Aggregate by severity

Produce a consolidated report:

```markdown
## Review Report

### Critical
[List — must fix before merge]

### High
[List — strong recommendation to fix before merge]

### Medium
[List — should address in a follow-up issue]

### Low
[List — optional polish]

### Passed
[List — specialists that found nothing to flag]
```

### Step 4: Confirm scope

Ask the user: "Critical and High findings need to be resolved before merging. Would you like to address them now, or should I open issues for the Medium and Low items?"

Do not silently apply fixes. Present them first.

## What review does not do

- Review does not rewrite the feature
- Review does not question design decisions already captured in ADRs
- Review does not run tests — that is the user's responsibility
- Review does not approve merges — it surfaces findings. The user decides.

## References

- [Security checklist](references/security.md)
- [Performance checklist](references/performance.md)
- [Maintainability checklist](references/maintainability.md)
