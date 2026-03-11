---
type: decision
status: active
confidence: high
decision_date: 2026-02-15
tags: [protocol, structure]
---

# Directory Structure: Convention-Based with Six Standard Subdirectories

## Context

We needed a standard directory layout for `.knowledge/` that covers the most common types of project knowledge without being prescriptive.

## Decision

Six standard subdirectories: `decisions/`, `architecture/`, `conventions/`, `context/`, `api/`, `archive/`. Only `README.md` is required. Everything else is optional.

## Rationale

- **decisions/** — The "why" behind technical choices is the single most valuable knowledge type for AI agents. Without it, agents re-suggest rejected approaches and hallucinate rationale.
- **architecture/** — System design context prevents agents from proposing changes that conflict with established patterns.
- **conventions/** — Coding standards that agents can follow consistently across sessions.
- **context/** — Domain-specific knowledge that can't be inferred from code alone.
- **api/** — API contracts change frequently and are a common source of agent errors.
- **archive/** — Knowledge should never be deleted. Superseded documents maintain traceability.

## Alternatives Considered

### Flat structure (no subdirectories)

Simpler, but doesn't scale. A project with 20+ knowledge files becomes hard to navigate for both humans and agents.

### Type-based subdirectories (by format, not content)

e.g., `records/`, `guides/`, `references/`. Rejected because content-based organization (`decisions/`, `architecture/`) maps more naturally to the questions agents ask.

## Consequences

- Agents can infer document `type` from the parent directory, reducing the need for explicit frontmatter.
- New users can start with just `README.md` and add directories as needed — no upfront decisions required.
