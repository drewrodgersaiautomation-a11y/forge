---
name: init-project
description: Initialize a new project with forge scaffolding. Creates CONTEXT.md domain glossary, docs/adr/ architecture decision records, .scratch/ local issue tracker, and git guardrails. Use when starting a new repo, onboarding onto an existing codebase, or setting up engineering discipline in a project that lacks it.
---

# Initialize Project

Set up the scaffolding that makes engineering discipline possible. Run once per repo, at the start.

## What Gets Created

- `CONTEXT.md` — domain glossary. The shared language between you and the agent.
- `docs/adr/` — architecture decision records. Decisions that were made and why.
- `.scratch/` — local issue tracker for tasks not worth a full GitHub issue.
- `.claude/settings.json` — git guardrails to block destructive operations.
- `CLAUDE.md` (if absent) — ethos preamble loaded at every session start.

## Process

### Step 1: Discover the domain

If this is an existing codebase, explore it first. Read the main entry points, key modules, and any existing documentation. Identify the nouns and verbs that the codebase already uses — function names, variable names, comments, existing docs. These are the raw material for the domain glossary.

If this is a greenfield project, ask the user: "What is this project? What are the 5–10 core concepts a new developer would need to understand to work on it?"

### Step 2: Write CONTEXT.md

Create `CONTEXT.md` at the repo root using this structure:

```markdown
# [Project Name] — Domain Glossary

> The shared language for this project. Keep terms here precise and consistent.
> Update this file whenever a term is introduced, renamed, or redefined.

## Terms

**[Term]**
Definition. What it is, what it is not, and any important disambiguation from similar terms.
_Avoid_: [alternative terms that mean the same thing — pick one and stick to it]

## Relationships

[How the core terms relate to each other. One sentence per relationship.]

## Flagged Ambiguities

[Terms that were previously ambiguous and have since been resolved.]
```

Write at least 5 terms that actually matter for this project. No filler.

### Step 3: Create docs/adr/

Create `docs/adr/` with a `README.md` explaining the ADR format:

```markdown
# Architecture Decision Records

Each file documents a significant architectural decision: the context, the options considered, and what was chosen and why.

**Format**: `NNNN-short-title.md`
**When to write one**: Any decision that a future developer might question and be tempted to reverse — without knowing why it was made this way.

## Index

(No decisions recorded yet.)
```

### Step 4: Create .scratch/

Create `.scratch/README.md`:

```markdown
# .scratch — Local Issue Tracker

Small tasks, bugs, and notes that don't warrant a GitHub issue. One file per item.

**Format**: `NNNN-short-title.md`
**Status prefix**: `[open]`, `[in-progress]`, `[done]`
```

Add `.scratch/` to `.gitignore` if the user wants these to stay local. Ask first.

### Step 5: Git guardrails

Ask the user: "Do you want git guardrails installed? These block the agent from running destructive git commands (push, reset --hard, clean, branch -D) without your explicit approval."

If yes, create `.claude/settings.json`:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/hooks/block-dangerous-git.sh"
          }
        ]
      }
    ]
  }
}
```

Create `.claude/hooks/block-dangerous-git.sh` — see [references/git-guardrails.md](references/git-guardrails.md).

### Step 6: CLAUDE.md

Check if `CLAUDE.md` exists at the repo root. If it does, append a project-specific section pointing to `CONTEXT.md` and `docs/adr/`. If it does not exist, copy the ethos preamble from the plugin's `CLAUDE.md` and append a project-specific section.

### Step 7: Confirm

List what was created. Ask: "Anything to add to CONTEXT.md before we start building?"
