# Quality Gates: Python

## Install dependencies

```bash
pip install pre-commit ruff mypy pytest
```

Or if using `pyproject.toml`:
```bash
pip install pre-commit ruff mypy pytest --break-system-packages
```

Add to `pyproject.toml` dev dependencies if using one.

## Create `.pre-commit-config.yaml`

```yaml
repos:
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.4.0
    hooks:
      - id: ruff
        args: [--fix]
      - id: ruff-format

  - repo: local
    hooks:
      - id: mypy
        name: mypy
        entry: mypy
        language: system
        types: [python]
        args: [--ignore-missing-imports]

      - id: pytest
        name: pytest
        entry: pytest
        language: system
        pass_filenames: false
        always_run: true
```

## Initialize pre-commit

```bash
pre-commit install
```

## Create `pyproject.toml` sections (if missing)

```toml
[tool.ruff]
line-length = 88
select = ["E", "F", "I", "N", "W"]

[tool.mypy]
python_version = "3.11"
strict = false
ignore_missing_imports = true

[tool.pytest.ini_options]
testpaths = ["tests"]
```

## Verify

```bash
pre-commit run --all-files
```
