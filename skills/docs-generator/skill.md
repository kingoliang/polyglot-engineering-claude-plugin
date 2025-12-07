# Documentation Generator Skill

A comprehensive skill for generating various types of documentation from code analysis.

## Capabilities

- Generate architecture documentation
- Create API reference documentation
- Produce UML diagrams (Mermaid format)
- Write README files
- Create user manuals
- Generate changelog entries

## Usage

This skill is invoked by the `/polyglot:docs` command and documentation agents.

## Process

### 1. Code Analysis

```bash
# Analyze project structure
find src -type f \( -name "*.ts" -o -name "*.py" -o -name "*.java" \)

# Extract exports and public APIs
grep -r "export" src/
```

### 2. Pattern Recognition

- Identify architectural patterns
- Map component relationships
- Document data flows

### 3. Template Application

Apply appropriate template based on documentation type:
- `architecture-template.md` for architecture docs
- `api-template.md` for API reference
- `readme-template.md` for README files
- `manual-template.md` for user manuals

### 4. Content Generation

Generate content sections:
1. Overview and purpose
2. Technical details
3. Usage examples
4. Configuration options

### 5. Quality Checks

- Verify completeness
- Check for broken links
- Validate code examples
- Ensure consistency

## Output Locations

| Doc Type | Default Location |
|----------|------------------|
| Architecture | `docs/architecture/` |
| API | `docs/api/` |
| UML | `docs/diagrams/` |
| README | Project root |
| Manual | `docs/user-guide/` |

## Integration Points

- Works with `codebase-researcher` agent
- Uses templates from `templates/` directory
- Outputs to standard documentation locations
