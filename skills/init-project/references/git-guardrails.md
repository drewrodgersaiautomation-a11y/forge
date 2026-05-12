# Git Guardrails Script

Create this file at `.claude/hooks/block-dangerous-git.sh` and make it executable with `chmod +x`.

```bash
#!/usr/bin/env bash
# block-dangerous-git.sh
# Blocks destructive git commands from running inside Claude Code.
# Hooked via PreToolUse on Bash tool calls.

set -euo pipefail

INPUT=$(cat)
COMMAND=$(echo "$INPUT" | python3 -c "import sys,json; d=json.load(sys.stdin); print(d.get('tool_input',{}).get('command',''))" 2>/dev/null || true)

BLOCKED_PATTERNS=(
  "git push"
  "git reset --hard"
  "git reset --soft HEAD~"
  "git clean -f"
  "git clean -fd"
  "git clean -dfx"
  "git branch -D"
  "git checkout \."
  "git restore \."
  "git rebase -i"
)

for PATTERN in "${BLOCKED_PATTERNS[@]}"; do
  if echo "$COMMAND" | grep -qE "$PATTERN"; then
    echo "BLOCKED: '$COMMAND' matches blocked pattern '$PATTERN'" >&2
    echo "The agent does not have authority to run destructive git commands." >&2
    echo "Ask the user to run this command manually if it is intentional." >&2
    exit 2
  fi
done

exit 0
```

## Adding or removing patterns

Edit the `BLOCKED_PATTERNS` array. Each entry is a grep `-E` regex, so special characters need escaping.

## Testing

```bash
echo '{"tool_input":{"command":"git push origin main"}}' | .claude/hooks/block-dangerous-git.sh
# Should exit 2 and print BLOCKED message
```
