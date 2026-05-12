# Quality Gates: Rust

Rust's toolchain includes everything needed. No external tools required.

## Create `.cargo/config.toml` (if missing)

```toml
[build]
rustflags = ["-D", "warnings"]
```

This treats all warnings as errors during builds — enforces clean code at the compiler level.

## Create `.pre-commit-config.yaml`

```yaml
repos:
  - repo: local
    hooks:
      - id: rustfmt
        name: rustfmt
        entry: cargo
        args: [fmt, --all, --, --check]
        language: system
        pass_filenames: false

      - id: clippy
        name: clippy
        entry: cargo
        args: [clippy, --, -D, warnings]
        language: system
        pass_filenames: false

      - id: cargo-test
        name: cargo test
        entry: cargo
        args: [test]
        language: system
        pass_filenames: false
        always_run: true
```

## Install pre-commit

```bash
pip install pre-commit
pre-commit install
```

## Create `rustfmt.toml` (if missing)

```toml
edition = "2021"
max_width = 100
use_small_heuristics = "Default"
```

## Verify

```bash
pre-commit run --all-files
```
