---
type: convention
status: active
confidence: high
last_validated: 2026-03-10
tags: [writing, format]
---

# Writing Knowledge Files

## The Rule

Every knowledge file is markdown with optional YAML frontmatter. Write for two audiences: your future self and the AI agents that will read this.

## Format

```markdown
---
type: decision          # decision | architecture | convention | context | api
status: active          # draft | active | review | superseded | deprecated
confidence: high        # high | medium | low | unknown
last_validated: YYYY-MM-DD
tags: []
---

# Title

Content here.
```

Frontmatter is always optional. A plain markdown file with a clear title is valid.

## Frontmatter Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `type` | string | Inferred from directory | Classification of knowledge |
| `status` | string | `active` | Lifecycle state |
| `confidence` | string | `unknown` | Team confidence in accuracy |
| `last_validated` | date | Git modified date | Last human confirmation |
| `expires` | date | None | Hard expiry date |
| `tags` | string[] | Inferred | Freeform taxonomy |
| `related` | string[] | None | Slugs of related files |
| `supersedes` | string | None | What this replaced |
| `superseded_by` | string | None | What replaced this (set when archiving) |
| `decision_date` | date | None | When a decision was made |
| `author` | string | None | Human or agent name |
| `source` | string | None | Origin (PR, meeting, review) |

## Rationale

Frontmatter provides structure for tools that can use it while keeping files human-readable. All fields are optional because convention over configuration means tools should infer what's missing from the filename, directory, and git history.

## Exceptions

None. All knowledge files follow this format. The only variation is whether frontmatter is included.
