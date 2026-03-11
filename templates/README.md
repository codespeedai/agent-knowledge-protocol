# Templates

Starter templates for common `.knowledge/` document types. Copy any template into your `.knowledge/` directory and fill in the placeholders.

Each template includes:
- Pre-filled YAML frontmatter with placeholder values
- Standard section headings for the document type
- Inline guidance in `<!-- HTML comments -->` (invisible when rendered, helpful when editing)

## Available Templates

| Template | Use For | Start Here |
|----------|---------|------------|
| [`knowledge-readme.md`](./knowledge-readme.md) | The routing table — your `.knowledge/` index | Every project |
| [`decision-record.md`](./decision-record.md) | Recording technical decisions and their rationale | Any decision worth remembering |
| [`architecture-overview.md`](./architecture-overview.md) | Documenting system design and component relationships | Projects with non-trivial architecture |
| [`convention.md`](./convention.md) | Codifying coding patterns and team rules | Teams that need consistency |
| [`context.md`](./context.md) | Domain knowledge, business rules, and personas | Projects with non-obvious domain logic |
| [`spec.md`](./spec.md) | Technical specifications with phased implementation | Projects with structured build phases |

## Usage

```bash
# Copy a template into your .knowledge/ directory
cp templates/decision-record.md .knowledge/decisions/2026-03-10-my-decision.md

# Edit and fill in the placeholders
```

Frontmatter is optional. Every template works as plain markdown if you remove the `---` block.
