# /polyglot:review Command

Perform comprehensive multi-agent code review with language-specific and cross-cutting analysis.

## Usage

```
/polyglot:review [target]
```

### Targets
- `staged` - Review staged changes
- `branch` - Review current branch vs main
- `pr #123` - Review specific PR
- `files path/to/file.ts` - Review specific files
- `commit abc123` - Review specific commit

## Process

### Phase 1: Analysis

1. **Change Detection**
   ```bash
   # Determine what to review
   git diff --name-only [target]
   ```

2. **Language Classification**
   - Identify file types
   - Group by language
   - Note mixed-language changes

3. **Change Scope Assessment**
   - New files vs modifications
   - Lines added/removed
   - Affected components

### Phase 2: Agent Engagement

Based on changes, invoke appropriate agents:

| Files Changed | Agents Invoked |
|--------------|----------------|
| *.ts, *.tsx  | typescript-reviewer |
| *.py         | python-reviewer |
| *.java       | java-reviewer |
| API routes   | architecture-strategist, security-sentinel |
| Database     | performance-oracle, security-sentinel |
| Auth code    | security-sentinel |
| All changes  | code-simplicity-reviewer |

### Phase 3: Review Execution

Each agent reviews and reports:
1. Security issues
2. Performance concerns
3. Code quality issues
4. Best practice violations
5. Improvement suggestions

### Phase 4: Synthesis

The `review-coordinator` agent:
1. Collects all findings
2. Removes duplicates
3. Assigns priorities
4. Creates unified report

## Output Format

```markdown
# Code Review Report

**Target**: [What was reviewed]
**Branch**: [Branch name]
**Reviewers**: [List of agents used]
**Date**: [Review date]

---

## Summary

| Severity | Count |
|----------|-------|
| Critical | 0     |
| High     | 2     |
| Medium   | 5     |
| Low      | 3     |

**Verdict**: [APPROVED / NEEDS CHANGES / BLOCKED]

---

## Critical Issues
*Must be fixed before merge*

None found.

---

## High Priority Issues
*Should be fixed*

### [H1] Missing Error Handling
**File**: `src/api/users.ts:45`
**Agent**: typescript-reviewer
**Issue**: Async function lacks try-catch block

**Current**:
```typescript
async function getUser(id: string) {
  const user = await db.users.find(id);
  return user;
}
```

**Suggested**:
```typescript
async function getUser(id: string) {
  try {
    const user = await db.users.find(id);
    if (!user) throw new NotFoundError('User not found');
    return user;
  } catch (error) {
    logger.error('Failed to get user', { id, error });
    throw error;
  }
}
```

---

## Medium Priority Issues
*Consider fixing*

### [M1] N+1 Query Pattern
...

---

## Low Priority Issues
*Nice to have*

### [L1] Consider Using Record Type
...

---

## Positive Observations

- Good test coverage for new authentication logic
- Clean separation of concerns in service layer
- Proper use of TypeScript generics

---

## Files Reviewed

| File | Issues | Status |
|------|--------|--------|
| src/api/users.ts | 2 | Needs Changes |
| src/services/auth.ts | 0 | Approved |
| tests/auth.test.ts | 1 | Minor Issues |

---

## Action Items

1. [ ] Fix error handling in `users.ts:45`
2. [ ] Address N+1 query in `users.ts:78`
3. [ ] Consider record type suggestion
```

## Review Depth Levels

### Quick Review
- Syntax and type issues only
- Fast, for small changes

```
/polyglot:review staged --quick
```

### Standard Review (Default)
- All language-specific checks
- Security for sensitive areas
- Performance for data operations

```
/polyglot:review branch
```

### Deep Review
- All agents engaged
- Architecture review included
- Comprehensive security scan

```
/polyglot:review pr #123 --deep
```

## Integration with Triage

After review, use:
```
/polyglot:triage
```

To interactively address findings with auto-fix suggestions.

## Best Practices

1. **Review Early**: Review before large commits
2. **Review Often**: Smaller reviews are more effective
3. **Address Criticals**: Never merge with critical issues
4. **Learn from Findings**: Use patterns to prevent future issues
