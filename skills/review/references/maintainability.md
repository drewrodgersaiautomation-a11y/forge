# Maintainability Review Checklist

## Module design

- [ ] New modules are deep: simple interface, complex implementation
- [ ] No shallow pass-throughs introduced: modules where the interface is as complex as the implementation
- [ ] Deletion test applied to new modules: would deleting this concentrate complexity or scatter it?
- [ ] No unnecessary indirection: abstractions earn their keep through two real use cases, not speculative reuse

## Domain language

- [ ] New terms introduced in the diff are documented in `CONTEXT.md`
- [ ] Existing terms from `CONTEXT.md` are used consistently — no synonyms, no paraphrasing
- [ ] File names, function names, and variable names use `CONTEXT.md` vocabulary
- [ ] No "avoid" terms (from `CONTEXT.md`) appear in the new code

## Architecture decisions

- [ ] Significant decisions made during this change are recorded in `docs/adr/`
- [ ] No ADRs are silently contradicted — if the decision is being revisited, the ADR is updated
- [ ] Changes that future developers might question have reasoning documented

## Code organization

- [ ] Related functionality is co-located — no complexity scattered across unrelated files
- [ ] Functions and modules have a single clear responsibility
- [ ] Magic numbers and strings are named constants with clear meaning
- [ ] Error handling is explicit and consistent with the rest of the codebase

## Testability

- [ ] New code can be tested through its public interface without mocking internal collaborators
- [ ] Tests were written for new behaviors (check with the Test Coverage specialist)
- [ ] No test-only code paths in production code

## Debt

- [ ] No TODOs, HACKs, or FIXMEs left without a linked issue
- [ ] No commented-out code committed
- [ ] Dependencies introduced are intentional and maintained
