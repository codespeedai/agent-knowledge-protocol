---
type: decision
status: active
confidence: high
decision_date: 2026-02-15
tags: [protocol, principles]
related: [protocol-structure]
---

# Design Principles: Git-Native, Markdown-First, Tool-Agnostic

## Context

Existing approaches to giving AI tools project context are fragmented. `.cursorrules` only works in Cursor. `CLAUDE.md` only works in Claude Code. Notion pages require API integration. There's no universal, portable standard.

## Decision

Six design principles govern the protocol:

1. **Git-native** — lives in the repo, versioned with code.
2. **Human-readable first** — plain markdown, no proprietary formats.
3. **AI-consumable** — optional frontmatter for structured queries.
4. **Convention over configuration** — sensible defaults, zero config to start.
5. **Tool-agnostic** — any tool that reads markdown can consume it.
6. **Composable** — works alongside any other convention-based directory.

## Rationale

- **Git-native** means knowledge is always co-located with the code it describes. No sync issues, no stale external docs, no broken links to external wikis.
- **Human-readable first** ensures the protocol is useful even without any tooling. A text editor is sufficient.
- **Tool-agnostic** is the critical differentiator. Knowledge that only works in one IDE creates lock-in and fragments the ecosystem. The protocol should work everywhere.
- **Convention over configuration** lowers the barrier to adoption. `mkdir .knowledge && touch .knowledge/README.md` is the entire setup.

## Alternatives Considered

### JSON or structured data format

Higher precision for tooling, but breaks the human-readable-first principle. Developers won't maintain files they can't easily read and edit.

### Tool-specific integration (plugins, APIs)

Higher fidelity but fragments the ecosystem. The value of a standard is universality.

## Consequences

- Any AI tool that reads files from a repository can consume `.knowledge/` with zero integration work.
- The tradeoff: less structure than a database or API. Frontmatter is optional, so tools must handle files with and without metadata.
