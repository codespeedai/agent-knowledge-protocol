# `.knowledge/`

**The Codespeed Knowledge Protocol is an open standard for structured project knowledge for humans and agents. It's git-native, markdown-first, and tool-agnostic.**

Every AI coding tool starts every session from zero. Your architecture, your decisions, your conventions are lost in each fresh session. This means that the smartest tools on earth can't remember what you told them yesterday, and simply memory files become garbled, stale, or sycophantic.

`.knowledge/` is a directory convention for structured project knowledge. The structure and approach is simple: markdown files that live in your repo and are versioned with your code, making them readable by any AI agent within the context of code development on any part of your codebase.

You can include anything in your knowledge directory — from business context to design systems. Over time, your `.knowledge/` directory compounds into a flywheel of vastly improved code quality and value.

---

## Quick Start

```bash
mkdir .knowledge
```

Create `.knowledge/README.md`:

```markdown
# Project Knowledge

> Institutional memory for [your project].

## What to Read

| Question | Go To |
|----------|-------|
| "What are we building?" | `architecture/overview.md` |
| "Why did we choose this database?" | `decisions/2026-01-15-database-choice.md` |
| "How do we handle errors?" | `conventions/error-handling.md` |

## Key Decisions

- We use TypeScript because [reason]
- We chose [database] because [reason]
- Our API follows [pattern] because [reason]
```

Any AI tool that reads markdown can now consume your project's institutional memory.

---

## Connect It to Your Agent

`.knowledge/` works with any tool that reads markdown. Wire it up so your agent discovers it automatically.

### CLAUDE.md

Add a knowledge router to your `CLAUDE.md`:

```markdown
## Knowledge Router

Read `.knowledge/README.md` first for the full routing table. Load sub-files on demand.

| Question | Go To |
|----------|-------|
| "What are we building?" | `.knowledge/architecture/overview.md` |
| "Why did we choose X?" | `.knowledge/decisions/` |
| "How do we handle Y?" | `.knowledge/conventions/` |
| "What does Z mean?" | `.knowledge/context/` |

**Before proposing architectural changes**, read the relevant decision record.
If a decision exists, do not suggest alternatives without understanding the rationale.
```

### .cursorrules / .windsurfrules

```markdown
## Knowledge Router

This project uses `.knowledge/` for institutional memory. Read `.knowledge/README.md`
for the routing table before answering architecture, convention, or domain questions.

Rules:
- Read the relevant decision record before proposing alternatives to existing patterns
- Check `.knowledge/conventions/` before suggesting style or structural changes
- When a routing table entry exists for your question, follow it — don't guess
```

### Any Agent

The protocol is tool-agnostic. If your agent can read a file, it can consume `.knowledge/`. Point it at `.knowledge/README.md` — the routing table tells it where everything lives. No plugins. No configuration. Just markdown.

---

## The Routing Table

The single most important feature of the protocol.

A lookup table in your README that maps natural-language questions to specific documents. Agents read the table, follow the links, and navigate directly to what they need:

```markdown
| Question | Go To |
|----------|-------|
| "What are we building?" | `architecture/overview.md` |
| "Why did we choose JWT?" | `decisions/2026-02-10-auth-strategy.md` |
| "How do we handle errors?" | `conventions/error-handling.md` |
| "What does 'tenant' mean?" | `context/domain-glossary.md` |
| "What changed recently?" | Check git log for `.knowledge/` |
```

---

## Directory Structure

```
.knowledge/
  README.md              # Routing table -- the index agents read first
  decisions/             # Decision records (ADR-style) -- the "why"
  architecture/          # System design, data models, component maps
  conventions/           # Coding patterns, naming rules, style decisions
  context/               # Domain knowledge, business logic, personas
  api/                   # API contracts, endpoints, auth flows
  archive/               # Superseded docs (never deleted, always traceable)
```

Only `README.md` is required. Everything else is optional. Start with one file. Add structure as knowledge accumulates through development.

---

## What Compounds

Structured knowledge makes AI multiplicative. 

1. Agent reads your conventions, decisions and documented systems and immediately begins building better code.
2. Agent begins to understand why your architecture exists, and what solutions and systems fit best within it for new, wider areas of development. 
3. Agent operates with a senior team member's institutional memory, building and adapting your knowledge layer over time as it learns. 

---

## Optional Frontmatter

Add YAML frontmatter when structure helps. Skip it when it doesn't.

```yaml
---
type: decision
status: active
confidence: high
decision_date: 2026-02-10
tags: [auth, security]
supersedes: auth-strategy-v1
related: [session-management]
---
```

All fields are optional. Tools infer missing values from the filename, directory, and git history. See the [full field reference](./.knowledge/conventions/knowledge-files.md) for details.

---

## Templates

Copy-paste starters for common document types:

| Template | Use For |
|----------|---------|
| [`knowledge-readme.md`](./templates/knowledge-readme.md) | The routing table -- your `.knowledge/` index |
| [`decision-record.md`](./templates/decision-record.md) | Technical decisions and their rationale |
| [`architecture-overview.md`](./templates/architecture-overview.md) | System design and components |
| [`convention.md`](./templates/convention.md) | Coding patterns and team rules |
| [`spec.md`](./templates/spec.md) | Technical specifications with phased implementation |

Each template includes pre-filled frontmatter and inline guidance in HTML comments.

---

## Design Principles

1. **Git-native.** Knowledge lives in the repo, versioned with the code it describes.
2. **Human-readable first.** Markdown files. No proprietary formats. No databases.
3. **AI-consumable.** Optional frontmatter provides structure agents can query.
4. **Convention over configuration.** Sensible defaults. Zero config to start.
5. **Tool-agnostic.** Any tool that reads markdown can consume `.knowledge/`.
6. **Composable.** Works alongside `.skills/`, `.cursor/rules`, `.github/`, and any other convention.

---

## This Repo Uses Its Own Protocol

The [`.knowledge/`](./.knowledge) directory in this repository is a working example of the protocol. It contains the decision records and conventions for the protocol itself.

---

## `.knowledge/` + `.skills/`

| | `.skills/` | `.knowledge/` |
|---|---|---|
| **Provides** | **Instructions** -- how to do work | **Memory** -- what the team knows |
| **Contains** | Coding patterns, review checklists, workflow rules | Decisions, architecture, domain context |

Skills tell agents how to work. Knowledge tells agents what the team knows.

---

## License

- **Code and templates:** [Apache 2.0](./LICENSE)
- **Documentation:** [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/)

Copyright 2026 [Codespeed, Inc.](https://codespeed.ai)

---

*`.knowledge/` is an open protocol created by [Codespeed](https://codespeed.ai). [Learn more](https://codespeed.ai/protocols/knowledge).*
