# Agent Knowledge Protocol

[![Agent Knowledge Protocol](https://img.shields.io/badge/.knowledge-v0.1.0-blue?style=flat-square)](https://github.com/codespeedai/agent-knowledge-protocol)

**An open standard for structured project knowledge in software development — for humans and AI agents.**

> Protocol Version: **0.1.0**

`.knowledge/` is a directory convention that gives any AI coding tool access to your project's institutional memory. It's git-native, markdown-first, and tool-agnostic — no plugins, no configuration, no vendor lock-in.

Every AI coding tool starts every session from zero. Your architecture, your decisions, your conventions — lost. The smartest tools on earth can't remember what you told them yesterday. Tool-specific memory files become garbled, stale, bloated, or sycophantic.

`.knowledge/` solves this with the simplest possible approach: markdown files that live in your repo, versioned with your code, readable by any AI agent on any part of your codebase. Include anything — from business context to design systems. Over time, your `.knowledge/` directory compounds into a flywheel of vastly improved code quality and business value.

## What Compounds

Structured knowledge makes AI multiplicative. 

1. Agent reads your conventions, decisions and documented systems and immediately begins building better code.
2. Agent begins to understand why your architecture exists, and what solutions and systems fit best within it for new, wider areas of development. 
3. Agent operates with a senior team member's institutional memory, building and adapting your knowledge layer over time as it learns. 

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

### GitHub Copilot

Add to `.github/copilot-instructions.md`:

```markdown
## Knowledge Router

This project uses `.knowledge/` for institutional memory.
Read `.knowledge/README.md` for the routing table before answering questions
about architecture, conventions, or domain context.

- Check decision records before proposing alternatives to existing patterns
- Check conventions before suggesting style or structural changes
- Follow routing table entries — don't guess when a document exists
```

### Any Agent

The protocol is tool-agnostic. If your agent can read a file, it can consume `.knowledge/`. Point it at `.knowledge/README.md` — the routing table tells it where everything lives. No plugins. No configuration. Just markdown.

For custom agents, add this to your system prompt:

```
This project contains a .knowledge/ directory with structured project context.
Read .knowledge/README.md first — it contains a routing table that maps questions
to specific documents. Follow the routing table before making assumptions about
architecture, conventions, or domain concepts.
```

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
  archive/               # Superseded docs -- traceable history
```

Only `README.md` is required. Everything else is optional. Start with one file. Add structure as knowledge accumulates through development.

### Naming Conventions

- **Decisions:** `YYYY-MM-DD-slug.md` — date-prefixed for chronological ordering. The date is when the decision was made, not when the file was created. Example: `2026-03-10-auth-strategy.md`
- **Everything else:** `slug.md` — descriptive, lowercase, hyphen-separated. Example: `error-handling.md`, `domain-glossary.md`, `system-overview.md`

Filenames should be self-describing. An agent reading just the filename should understand the topic without opening the file.

### Archiving & Deletion

When a decision is superseded or a convention changes:

1. Set `status: superseded` in the original document's frontmatter
2. Add `superseded_by: new-document-slug` pointing to the replacement
3. Move the file to `archive/`
4. Update the routing table in `README.md`

The replacement document should include `supersedes: old-document-slug` in its frontmatter, creating a two-way link that lets agents trace the evolution of a decision.

**Deletion is fine** when knowledge is truly obsolete — a removed feature, a deprecated API, a library you no longer use. Git history preserves the record. Archive when the context might still be useful for understanding current decisions; delete when it's just noise.

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

All fields are optional. Tools infer missing values from the filename, directory, and git history.

**[Full field reference](./.knowledge/conventions/knowledge-files.md)** — complete list of supported fields, types, and defaults.

---

## Templates

Copy-paste starters for common document types:

| Template | Use For |
|----------|---------|
| [`knowledge-readme.md`](./templates/knowledge-readme.md) | The routing table -- your `.knowledge/` index |
| [`decision-record.md`](./templates/decision-record.md) | Technical decisions and their rationale |
| [`architecture-overview.md`](./templates/architecture-overview.md) | System design and components |
| [`convention.md`](./templates/convention.md) | Coding patterns and team rules |
| [`context.md`](./templates/context.md) | Domain knowledge, business rules, personas |
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

## Conflict Resolution

When knowledge and code disagree, or when two documents contradict each other:

- **Code wins over docs.** If the codebase does X and a knowledge file says Y, the code is the source of truth. Update the knowledge file.
- **Newer decisions supersede older ones.** Check `decision_date` or git history. If two decision records conflict, the more recent one governs.
- **Specific wins over general.** A convention for "API error handling" overrides a general "error handling" convention when they conflict.

---

## When to Write a Knowledge File

Not everything belongs in `.knowledge/`. Here's the heuristic:

**Write a knowledge file when:**
- A decision spans multiple files or affects system-wide behavior
- A convention isn't enforceable by linters or type systems
- Domain context can't be inferred from code, types, or naming alone
- You've explained the same "why" to an agent (or a teammate) more than once
- You chose between multiple valid approaches and want to prevent relitigating

**Just use code comments when:**
- The context is local to a single function or file
- The "why" is obvious from the surrounding code
- A type signature or test name already communicates the intent

The line is simple: if an agent working on a *different* file would need this context, it belongs in `.knowledge/`. If only someone reading *this* file needs it, a comment is enough.

---

## Keeping Knowledge Fresh

The biggest risk to any knowledge system is staleness. Two conventions prevent it:

**1. Update in the same PR.** If your PR changes a decision or convention documented in `.knowledge/`, update the knowledge file in the same PR. Don't create a follow-up task — it won't happen.

**2. Add a PR template checklist item.** Drop this into your `.github/pull_request_template.md`:

```markdown
- [ ] If this PR changes an architectural decision or team convention, the relevant `.knowledge/` file has been updated
```

Knowledge maintenance should be a side effect of normal development, not a separate activity.

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

## Contributing

`.knowledge/` is an open standard and contributions are welcome.

- **Try it** — add a `.knowledge/` directory to your project and [tell us how it went](https://github.com/codespeedai/agent-knowledge-protocol/discussions)
- **Report issues** — [open an issue](https://github.com/codespeedai/agent-knowledge-protocol/issues) for bugs, unclear docs, or missing guidance
- **Propose changes** — submit a PR for template improvements, new integrations, or protocol enhancements
- **Share templates** — built a useful knowledge file pattern? Contribute it to `templates/`

**Add the badge to your project:**

```markdown
[![Agent Knowledge Protocol](https://img.shields.io/badge/.knowledge-v0.1.0-blue?style=flat-square)](https://github.com/codespeedai/agent-knowledge-protocol)
```

---

## License

- **Code and templates:** [Apache 2.0](./LICENSE)
- **Documentation:** [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/)

Copyright 2026 [Codespeed, Inc.](https://codespeed.ai)

---

*`.knowledge/` is an open protocol created by [Codespeed](https://codespeed.ai). [Learn more](https://codespeed.ai/protocols/knowledge).*
