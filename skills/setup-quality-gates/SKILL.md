---
name: setup-quality-gates
description: Install automated code quality gates for the current project. Detects the stack (Node, Python, Go, Rust) and installs the appropriate pre-commit hooks for linting, formatting, type checking, and tests. Use when starting a new project, when the user wants pre-commit hooks, or when code quality automation is missing.
---

# Setup Quality Gates

Install automated enforcement at commit time. Catches formatting issues, type errors, and failing tests before they ever get committed. Works across stacks.

## What gets installed

| Stack | Formatter | Linter | Type check | Test gate |
|---|---|---|---|---|
| Node / TypeScript | Prettier | ESLint | `tsc --noEmit` | test script |
| Python | Ruff format | Ruff lint | mypy | pytest |
| Go | gofmt | golangci-lint | built-in | go test |
| Rust | rustfmt | clippy | built-in | cargo test |

All stacks use **pre-commit hooks** that run on staged files only (fast) plus a full type check and test run.

## Process

### Step 1: Detect the stack

Check for these files in order:

- `package.json` → Node / TypeScript
- `pyproject.toml` or `requirements.txt` → Python
- `go.mod` → Go
- `Cargo.toml` → Rust
- Multiple matches → ask the user which stack to configure

### Step 2: Install for detected stack

Follow the instructions for the detected stack in [references/node.md](references/node.md), [references/python.md](references/python.md), [references/go.md](references/go.md), or [references/rust.md](references/rust.md).

### Step 3: Verify

Run the hook against the current staged files (or all files if nothing staged):

```bash
# Node
npx lint-staged

# Python
pre-commit run --all-files

# Go
gofmt -l . && golangci-lint run

# Rust
cargo fmt --check && cargo clippy -- -D warnings
```

Fix any issues before proceeding.

### Step 4: Commit

Stage all config files added and commit:

```
Add quality gates: [formatter] + [linter] + type check + tests
```

This commit runs through the new hooks — a smoke test that everything works.

### Step 5: Confirm

Tell the user:
- What runs on every commit
- How to bypass in an emergency (`git commit --no-verify` — use sparingly)
- That the gates enforce formatting automatically, so they never need to think about it again
