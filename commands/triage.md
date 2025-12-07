# /polyglot:triage Command

Interactively present review findings for approval with auto-fix capabilities.

## Usage

```
/polyglot:triage [review-reference]
```

## Process

### Phase 1: Load Findings

1. Load the most recent review or specified review
2. Group findings by severity and file
3. Prepare auto-fix suggestions where available

### Phase 2: Interactive Resolution

Present each finding with options:

```markdown
## Finding 1 of 10: [H1] Missing Error Handling

**Severity**: High
**File**: `src/api/users.ts:45`
**Agent**: typescript-reviewer

**Issue**: Async function lacks try-catch block

**Current Code**:
```typescript
async function getUser(id: string) {
  const user = await db.users.find(id);
  return user;
}
```

**Suggested Fix**:
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

**Actions**:
[1] Apply Fix - Apply the suggested fix automatically
[2] Skip - Skip this finding for now
[3] Dismiss - Mark as won't fix with reason
[4] Custom - Provide a custom fix
[5] View Context - See more surrounding code
```

### Phase 3: Resolution Tracking

Track all decisions:

| Finding | Decision | Applied |
|---------|----------|---------|
| H1 | Apply Fix | Yes |
| H2 | Skip | - |
| M1 | Dismiss: Intentional | - |

### Phase 4: Summary

```markdown
# Triage Summary

## Applied Fixes
- [H1] Missing Error Handling in `users.ts`
- [M2] Added type annotation in `auth.ts`

## Skipped (For Later)
- [H2] Performance optimization in `query.ts`

## Dismissed
- [M1] Intentional pattern for compatibility

## Remaining Issues
| Severity | Count |
|----------|-------|
| High | 1 |
| Medium | 2 |

## Next Steps
- Address skipped high priority item
- Consider medium priority items
- Re-run review after fixes: `/polyglot:review staged`
```

## Auto-Fix Capabilities

### Supported Auto-Fixes

| Issue Type | Auto-Fix Available |
|------------|-------------------|
| Missing types | Yes |
| Missing error handling | Template |
| Unused imports | Yes |
| Formatting issues | Yes |
| Simple refactors | Yes |
| Security issues | Case-by-case |
| Architecture issues | No (requires design) |

### Fix Templates

When exact auto-fix isn't possible, provide templates:

```typescript
// Template: Error Handling
try {
  // Your code here
} catch (error) {
  // Handle error
  throw error;
}
```

## Batch Operations

### Apply All Safe Fixes
```
/polyglot:triage --apply-safe
```
Applies all low-risk fixes (formatting, imports, simple types).

### Skip All Low Priority
```
/polyglot:triage --skip-low
```
Focuses on high and medium priority issues.

### Review Only Critical
```
/polyglot:triage --critical-only
```
Shows only critical and high severity issues.

## Decision Guidelines

### When to Apply
- Clear improvement
- No behavioral change
- Well-understood pattern
- Test coverage exists

### When to Skip
- Need more context
- Uncertain about requirement
- Needs discussion with team
- Will address in related task

### When to Dismiss
- Intentional pattern
- False positive
- Not applicable to this codebase
- Already addressed elsewhere

## Integration

### After Triage
```bash
# Run tests to verify fixes
npm test

# Re-run review
/polyglot:review staged

# Commit if all passing
git add -A
git commit -m "fix: address code review findings"
```

### With Work Command
```bash
# During work execution
/polyglot:work step-3

# Quick review of step
/polyglot:review staged --quick

# Triage any issues
/polyglot:triage
```

## Output Format

```markdown
# Triage Complete

**Session**: Review from [date]
**Total Findings**: 10

## Resolution Summary
| Action | Count |
|--------|-------|
| Applied | 5 |
| Skipped | 3 |
| Dismissed | 2 |

## Verification
- [ ] All tests passing
- [ ] No new lint errors
- [ ] Build successful

## Commands Used
```bash
git add src/api/users.ts src/services/auth.ts
git commit -m "fix: apply code review fixes

- Add error handling to getUser
- Add missing type annotations
- Remove unused imports
"
```
```
