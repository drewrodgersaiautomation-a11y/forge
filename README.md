# forge

**An opinionated engineering methodology for AI coding agents.**

Works with Claude Code, Codex, Cursor, and any agent that reads `CLAUDE.md` or `AGENTS.md`.

---

Most AI coding plugins tell the agent what to do. This one enforces how you think.

The problem with AI-generated code is not that the agent is unintelligent — it is that the agent has no discipline. It skips planning. It writes tests after the fact, or not at all. It builds shallow wrappers instead of deep modules. It keeps going long after the context window is bloated and degraded. It ships code that works but nobody can maintain.

`forge` is a set of skills that encode real engineering discipline into every project you build with an AI agent. The same discipline that separates code that lasts from code that accrues debt from the moment it ships.

---

## What's inside

Ten slash commands and an ethos preamble that loads at every session start.

| Skill | What it does |
|---|---|
| `/init-project` | Set up a new repo with domain glossary (`CONTEXT.md`), architecture decision records, local issue tracker, and git guardrails |
| `/plan` | Turn an idea into a PRD and issue breakdown before writing any code |
| `/tdd` | Red-green-refactor with vertical slices. Tests verify behavior, not implementation |
| `/architecture` | Find shallow modules and propose concrete deepening refactors |
| `/investigate` | 3-layer knowledge check before building anything non-trivial |
| `/review` | Multi-specialist analysis: security, performance, maintainability, API contracts, test coverage |
| `/handoff` | Compact the session into a transfer document for a fresh agent |
| `/zoom-out` | Get a module map of unfamiliar code using the project's domain vocabulary |
| `/diagnose` | Hypothesis-first debugging with human in the loop |
| `/ship` | Final pre-merge checklist — nothing ships with shortcuts left open |

The `CLAUDE.md` / `AGENTS.md` preamble encodes five principles that apply to every session:

1. **Boil the Lake** — do the complete implementation. With AI, completeness costs minutes. Shortcuts are legacy thinking.
2. **Search Before Building** — check 3 knowledge layers (tried-and-true, current best practices, first principles) before any non-trivial build decision.
3. **User Sovereignty** — models recommend. Users decide. Two models agreeing is a signal, not a mandate.
4. **Deep Modules** — simple interface, complex implementation. Apply the deletion test to every new module.
5. **Test Behavior** — tests verify what the system does through its public interface. A test that breaks on an internal refactor is a bad test.

---

## Install

### Claude Code

```bash
npx skills@latest add drewrodgersaiautomation-a11y/forge
```

Or manually: clone this repo and add the path to your Claude Code config.

### Codex

Copy `AGENTS.md` to your project root. Codex loads this automatically.

For individual skills, add them to your `codex.yaml` or reference them in your `AGENTS.md`.

### Cursor / other agents

Copy `CLAUDE.md` to your project root. Most agents with system prompt injection will pick this up. The skills are plain markdown — copy any `skills/*/SKILL.md` into your agent's context as needed.

### Cowork

Install directly as a plugin: download `forge.plugin` from the [releases page](https://github.com/drewrodgersaiautomation-a11y/forge/releases) and drag it into Cowork.

---

## How to use it

**Starting a new project:**
```
/init-project
```
Sets up CONTEXT.md, ADR folder, issue tracker, and git guardrails in one shot.

**Before writing any code:**
```
/plan
```
Produces a PRD with user stories, module design, and a prioritized issue list. Do this every time.

**Building a feature:**
```
/tdd
```
Red-green-refactor, vertical slices. One behavior at a time.

**Context getting heavy:**
```
/handoff
```
Compacts the session. Open a fresh tab and resume from the handoff doc.

**Before merging:**
```
/review
/ship
```
Five-specialist review, then the pre-merge checklist. Nothing ships with shortcuts.

---

## The project lifecycle

```
New project
  └─ /init-project              (fresh tab)

New feature
  └─ /investigate               (research before building)
  └─ /plan                      (spec before code)
  └─ /tdd                       (build with tests)
      └─ /zoom-out              (when lost)
      └─ /diagnose              (when broken)
      └─ /handoff               (between phases)

Pre-merge
  └─ /review                    (multi-specialist)
  └─ /ship                      (final checklist)
```

---

## Philosophy

This repo is influenced by:

- Matt Pocock's [skills](https://github.com/mattpocock/skills) — deep modules, domain language discipline, and the realization that tests should specify behavior, not mirror code
- Garry Tan's [gstack](https://github.com/garrytan/gstack) — the Boil the Lake ethos, Search Before Building, and User Sovereignty
- John Ousterhout's *A Philosophy of Software Design* — the depth metric, deletion test, and the seam concept
- Kent Beck's *Test Driven Development* — the red-green-refactor loop and the tracer bullet

The core insight that ties it together: **AI coding agents have no native discipline.** They will do exactly what you tell them — no more, no less. If you tell them to build a feature, they build a feature. They don't plan, they don't test properly, they don't think about whether the module they're creating is deep or shallow, and they don't stop when the context window is full. These skills supply that discipline. They are the difference between an AI that writes code and an AI that engineers software.

---

## Contributing

PRs welcome. Each skill should:
- Solve one clearly-defined problem
- Have a SKILL.md under 3,000 words (reference files for depth)
- Use imperative, verb-first language throughout
- Not introduce new dependencies

New skills go in `skills/` with a subdirectory and `SKILL.md`. Update `plugin.json` and this README.

---

## License

MIT
