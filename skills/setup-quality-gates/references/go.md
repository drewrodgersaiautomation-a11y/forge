# Quality Gates: Go

## Install dependencies

```bash
# golangci-lint
go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest

# pre-commit
pip install pre-commit
```

## Create `.pre-commit-config.yaml`

```yaml
repos:
  - repo: local
    hooks:
      - id: gofmt
        name: gofmt
        entry: gofmt
        args: [-w]
        language: system
        types: [go]

      - id: golangci-lint
        name: golangci-lint
        entry: golangci-lint
        args: [run, --fix]
        language: system
        types: [go]
        pass_filenames: false

      - id: go-test
        name: go test
        entry: go
        args: [test, ./...]
        language: system
        pass_filenames: false
        always_run: true
```

## Initialize pre-commit

```bash
pre-commit install
```

## Create `.golangci.yml` (if missing)

```yaml
linters:
  enable:
    - errcheck
    - gosimple
    - govet
    - ineffassign
    - staticcheck
    - unused

linters-settings:
  govet:
    check-shadowing: true
```

## Verify

```bash
pre-commit run --all-files
```
