# Code Analysis Skill

A skill for analyzing code structure, patterns, and quality across TypeScript, Python, and Java projects.

## Capabilities

- Project structure analysis
- Dependency mapping
- Pattern recognition
- Complexity metrics
- Code quality assessment

## Supported Languages

| Language | File Extensions | Frameworks |
|----------|-----------------|------------|
| TypeScript | `.ts`, `.tsx` | React, Next.js, NestJS |
| JavaScript | `.js`, `.jsx` | Express, Vue |
| Python | `.py` | Django, FastAPI, Flask |
| Java | `.java` | Spring Boot, Jakarta EE |

## Analysis Types

### 1. Structure Analysis

Analyze project organization:
- Directory structure
- Module organization
- File relationships

### 2. Dependency Analysis

Map dependencies:
- External packages
- Internal imports
- Circular dependencies

### 3. Pattern Analysis

Identify patterns:
- Architectural patterns (MVC, Hexagonal, etc.)
- Design patterns (Factory, Strategy, etc.)
- Anti-patterns

### 4. Complexity Analysis

Calculate metrics:
- Cyclomatic complexity
- Lines of code
- Function/method counts
- Nesting depth

### 5. API Analysis

Extract API information:
- Endpoints and routes
- Request/response types
- Authentication requirements

## Usage

### TypeScript Analysis

```bash
# Find all TypeScript files
find src -name "*.ts" -o -name "*.tsx"

# Extract exports
grep -r "export" --include="*.ts" src/

# Find dependencies
cat package.json | jq '.dependencies'
```

### Python Analysis

```bash
# Find all Python files
find . -name "*.py" -not -path "./.venv/*"

# Extract classes
grep -r "class " --include="*.py" .

# Find imports
grep -r "^import\|^from" --include="*.py" .
```

### Java Analysis

```bash
# Find all Java files
find src -name "*.java"

# Extract classes
grep -r "public class\|public interface" --include="*.java" .

# Find annotations
grep -r "@" --include="*.java" src/
```

## Output Format

```markdown
# Code Analysis Report

## Project Overview
- Type: [TypeScript/Python/Java]
- Files: [Count]
- Lines of Code: [Count]

## Structure
[Directory tree]

## Dependencies
[Dependency list]

## Patterns
[Identified patterns]

## Metrics
[Complexity metrics]

## Recommendations
[Improvement suggestions]
```

## Integration

- Used by review agents for context
- Used by documentation agents for analysis
- Used by planning agents for scope estimation
