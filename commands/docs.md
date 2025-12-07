# /polyglot:docs Command

Generate comprehensive documentation from existing code, including architecture docs, API docs, UML diagrams, README, and user manuals.

## Usage

```
/polyglot:docs [type] [options]
```

### Documentation Types

| Type | Command | Description |
|------|---------|-------------|
| All | `/polyglot:docs all` | Generate all documentation |
| Architecture | `/polyglot:docs architecture` | System architecture docs |
| API | `/polyglot:docs api` | API reference documentation |
| UML | `/polyglot:docs uml` | UML diagrams |
| README | `/polyglot:docs readme` | Project README |
| Manual | `/polyglot:docs manual` | User manual |

## Process

### Phase 1: Analysis (Plan-Based Approach)

Following the compound engineering plan philosophy:

1. **Codebase Research**
   - Invoke `codebase-researcher` for project understanding
   - Map project structure and patterns
   - Identify key components

2. **Documentation Audit**
   - Check existing documentation
   - Identify gaps
   - Note outdated content

3. **Documentation Plan**
   - Determine what needs to be generated
   - Order by dependency
   - Estimate scope

### Phase 2: Generation

Invoke appropriate documentation agents:

1. **Architecture Documentation**
   - `architecture-doc-generator` agent
   - Produces: System overview, component docs, ADRs

2. **API Documentation**
   - `api-doc-generator` agent
   - Produces: Endpoint docs, schemas, examples

3. **UML Diagrams**
   - `uml-generator` agent
   - Produces: Class, sequence, component diagrams

4. **README**
   - `readme-generator` agent
   - Produces: Project README with badges, usage, etc.

5. **User Manual**
   - `manual-generator` agent
   - Produces: Getting started, full manual, troubleshooting

### Phase 3: Output

Generate files in standard locations:

```
project/
├── README.md                    # Project README
├── docs/
│   ├── architecture/
│   │   ├── overview.md          # System overview
│   │   ├── components.md        # Component documentation
│   │   ├── data-flow.md         # Data flow documentation
│   │   └── decisions/           # Architecture Decision Records
│   │       └── ADR-001-*.md
│   ├── api/
│   │   ├── reference.md         # API reference
│   │   ├── openapi.yaml         # OpenAPI spec (if REST)
│   │   └── examples/            # API examples
│   ├── diagrams/
│   │   ├── class-diagram.md     # Class diagrams
│   │   ├── sequence-*.md        # Sequence diagrams
│   │   └── component.md         # Component diagram
│   └── user-guide/
│       ├── getting-started.md   # Getting started guide
│       ├── user-manual.md       # Full user manual
│       └── troubleshooting.md   # Troubleshooting guide
└── CHANGELOG.md                 # Change log
```

## Command Options

### Scope Options
```
--scope=full        # Generate complete documentation
--scope=minimal     # Generate essential docs only
--scope=update      # Update existing docs only
```

### Format Options
```
--format=markdown   # Markdown (default)
--format=html       # HTML output
--format=pdf        # PDF output (requires pandoc)
```

### Target Options
```
--target=developers   # Developer-focused docs
--target=users        # End-user focused docs
--target=all          # Both audiences
```

## Examples

### Generate All Documentation
```
/polyglot:docs all
```

### Generate Architecture Docs Only
```
/polyglot:docs architecture
```

### Generate API Docs with OpenAPI
```
/polyglot:docs api --format=openapi
```

### Generate UML for Specific Package
```
/polyglot:docs uml --path=src/services
```

### Update README Only
```
/polyglot:docs readme --scope=update
```

### Generate User Manual
```
/polyglot:docs manual --target=users
```

## Output Format

```markdown
# Documentation Generation Report

**Project**: [Project Name]
**Date**: [Generation Date]

## Generated Documents

| Document | Path | Status |
|----------|------|--------|
| README | README.md | Created |
| Architecture Overview | docs/architecture/overview.md | Created |
| API Reference | docs/api/reference.md | Created |
| Class Diagram | docs/diagrams/class-diagram.md | Created |
| Getting Started | docs/user-guide/getting-started.md | Created |

## Summary

- **Total Documents**: 10
- **New**: 8
- **Updated**: 2

## Next Steps

1. Review generated documentation
2. Add project-specific details
3. Update any placeholder content
4. Commit documentation changes

## Notes

- [Any observations or recommendations]
```

## Integration with BMAD Method

Following BMAD's documentation principles:

### Document Sharding
For large projects, documentation is automatically sharded:
- `overview.md` - High-level summary
- `details/` - Detailed component docs
- `reference/` - Technical reference

### Context Engineering
Documentation includes context for AI agents:
- Clear file purposes
- Cross-references
- Implementation notes

### Living Documentation
Documentation is designed to be:
- Easy to update
- Version controlled
- Linked to code

## Best Practices

1. **Generate Early**: Create docs as code is written
2. **Review Generated**: AI-generated docs need review
3. **Keep Updated**: Re-run after major changes
4. **Customize**: Add project-specific content
5. **Link to Code**: Reference actual file paths
