---
name: handoff
description: Compact the current conversation into a transferable document for a fresh agent session. Use when context is getting heavy, a project phase is complete, or the user is about to start a new phase of work. Trigger phrases: "handoff", "new session", "context is getting big", "wrap this up", "start fresh".
argument-hint: "What will the next session focus on?"
---

# Handoff

Compact this session into a document that a fresh agent can pick up without needing conversation history.

## Why this matters

A bloated context degrades the agent. After a long session — exploring, planning, debugging, building — the context window carries a lot of noise: failed attempts, superseded ideas, redundant explanations. A fresh session with a clean handoff document starts faster and thinks more clearly.

Handoff is not a summary. It is a transfer document: everything the next agent needs, nothing it doesn't.

## Process

### Step 1: Determine scope

If the user passed arguments, use them to determine what the next session will focus on and tailor the document accordingly.

If no arguments, ask: "What is the next session for?"

### Step 2: Identify what NOT to include

Do not duplicate content already captured in persistent artifacts:
- PRDs → reference by path or issue number
- ADRs → reference by path
- Committed code → reference by file path or commit
- CONTEXT.md updates → already persisted
- Open issues in `.scratch/` → already persisted

Reference these by path or ID. Do not restate their content.

### Step 3: Write the handoff document

Save to a temp file: `mktemp -t handoff-XXXXXX.md` (read the file before writing to it).

Use this structure:

```markdown
# Handoff: [Date] — [Focus of next session]

## State

[One paragraph: where things stand right now. What was built, what was decided, what is working, what is not.]

## What was decided (not yet in ADRs)

[Decisions made in this session that haven't been written to docs/adr/ yet. Include the reasoning.]

## Open questions

[Questions that need answering before or during the next session. Be specific.]

## Next actions

[The concrete things to do in the next session, in order. Each action should be completable in one work unit.]

## Skills to use

[Which skills from forge are relevant for the next session's focus:]
- /plan — if a feature needs to be specced before building
- /tdd — if building new functionality
- /architecture — if refactoring or reviewing existing code
- /investigate — if a key decision needs research
- /review — if code is ready to merge
- /ship — if the release is ready

## Persistent artifacts (do not restate, just reference)

| Artifact | Path / Reference |
|---|---|
| PRD | [path or issue #] |
| ADRs | [paths] |
| Open issues | .scratch/ |
| CONTEXT.md | ./CONTEXT.md |
```

### Step 4: Confirm and instruct

After writing the document, tell the user:

1. Where the handoff file was saved
2. How to resume: "Open a fresh session, load the forge plugin, and paste the contents of this handoff file as your first message."
