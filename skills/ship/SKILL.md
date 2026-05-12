---
name: ship
description: Final pre-merge checklist. Verifies tests pass, review is complete, documentation is current, no shortcuts are left open, and the PR is clean. Use when the user is ready to merge, says "ship this", "ready to merge", or "let's ship".
---

# Ship

Run the pre-merge checklist. Nothing ships until every item is addressed or explicitly deferred with a linked issue.

## Checklist

### Code

- [ ] All tests pass (`npm test`, `pytest`, `cargo test`, or equivalent)
- [ ] No new linting errors or type errors introduced
- [ ] No TODO, HACK, or FIXME comments committed without a linked issue
- [ ] No commented-out code
- [ ] No hardcoded credentials, tokens, or local paths

### Tests

- [ ] New behaviors introduced in this change have tests
- [ ] Tests verify behavior through public interfaces — not implementation details
- [ ] Regression test exists for any bug being fixed
- [ ] Test names describe behaviors, not implementation ("user can checkout" not "PaymentService.charge is called")

### Documentation

- [ ] New domain terms added to `CONTEXT.md`
- [ ] Significant decisions recorded in `docs/adr/`
- [ ] Public API changes documented (README, changelog, or API docs)
- [ ] `.env.example` updated if new environment variables were added

### Architecture

- [ ] No shallow modules introduced — new modules are deep
- [ ] No existing ADRs silently contradicted
- [ ] `/review` was run on this diff (or will be run now — run it if not)

### Git hygiene

- [ ] Commits are logical units with clear messages (imperative present tense: "Add checkout validation")
- [ ] Branch is rebased or up to date with main
- [ ] No merge commits in the branch history (rebase before merging)
- [ ] PR title matches the format used in this repo

### Open questions

- [ ] All open questions from the PRD are resolved or explicitly deferred to a linked follow-up issue
- [ ] No follow-up work is left undocumented

## Process

Go through the checklist item by item. For each failure:

- **Can be fixed now**: fix it before proceeding
- **Deferred consciously**: create a `.scratch/` issue or GitHub issue, link it, mark the item as deferred with the issue reference
- **Not applicable**: mark with N/A and a brief reason

Present the completed checklist to the user before running any git operations. Ask: "Ready to merge?"

## What ship does NOT do

- Ship does not run `git push` — the user runs that
- Ship does not approve the PR — it surfaces the state; the user decides
- Ship does not squash or rewrite commits without explicit user instruction
