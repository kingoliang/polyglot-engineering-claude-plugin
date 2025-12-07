# /polyglot:plan Command

Transform feature descriptions into detailed, actionable implementation plans with research and acceptance criteria.

## Usage

```
/polyglot:plan [feature description or issue reference]
```

## Process

### Phase 1: Research & Discovery

1. **Codebase Analysis**
   - Invoke `codebase-researcher` agent to understand current architecture
   - Identify relevant existing code, patterns, and dependencies
   - Map affected systems and components

2. **Framework Research** (if needed)
   - Invoke `framework-researcher` agent for technology guidance
   - Research best practices for the specific task
   - Identify potential libraries or approaches

3. **Requirement Clarification**
   - Parse the feature description
   - Identify ambiguities
   - Ask clarifying questions if needed

### Phase 2: Plan Generation

1. **Scope Definition**
   - Define clear boundaries
   - Identify in-scope and out-of-scope items
   - List assumptions

2. **Task Breakdown**
   - Break into atomic, estimable tasks
   - Identify dependencies between tasks
   - Order tasks logically

3. **Technical Design**
   - Define data models/types
   - Design API contracts (if applicable)
   - Specify component interactions

4. **Acceptance Criteria**
   - Define testable criteria for each task
   - Specify expected behaviors
   - Include edge cases

### Phase 3: Risk Assessment

1. **Technical Risks**
   - Identify complex areas
   - Note uncertainty points
   - Suggest mitigations

2. **Dependencies**
   - External service dependencies
   - Library version requirements
   - Team dependencies

## Output Format

```markdown
# Implementation Plan: [Feature Name]

## Overview
Brief description of what will be implemented.

## Research Summary
Key findings from codebase and framework research.

## Scope

### In Scope
- Item 1
- Item 2

### Out of Scope
- Item 1
- Item 2

### Assumptions
- Assumption 1
- Assumption 2

## Technical Design

### Data Models
```language
// Type definitions or models
```

### API Contracts (if applicable)
| Endpoint | Method | Description |
|----------|--------|-------------|
| /api/x   | POST   | Does Y      |

### Component Changes
| Component | Change Type | Description |
|-----------|-------------|-------------|
| file.ts   | Modify      | Add X       |

## Implementation Tasks

### Task 1: [Task Title]
**Description**: What needs to be done
**Files**: List of files to change
**Acceptance Criteria**:
- [ ] Criterion 1
- [ ] Criterion 2

### Task 2: [Task Title]
...

## Testing Strategy
- Unit tests for: [list]
- Integration tests for: [list]
- E2E tests for: [list]

## Risks & Mitigations
| Risk | Impact | Mitigation |
|------|--------|------------|
| X    | High   | Y          |

## Dependencies
- Library X version Y
- External service Z

## Notes
Additional considerations for implementation.
```

## Example Usage

### Simple Feature
```
/polyglot:plan Add user profile picture upload
```

### From Issue
```
/polyglot:plan #123
```

### Complex Feature
```
/polyglot:plan Implement real-time notifications using WebSocket
with support for mobile push notifications and email fallback
```

## Integration with Other Commands

After planning:
- Use `/polyglot:work` to execute the plan
- Use `/polyglot:review` after implementation
- Use `/polyglot:docs` to update documentation

## Best Practices

1. **Start Small**: Break large features into multiple plans
2. **Be Specific**: Vague descriptions lead to vague plans
3. **Include Context**: Reference existing code or patterns
4. **Review Before Executing**: Plans should be reviewed before work starts
