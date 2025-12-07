# /polyglot:work Command

Execute implementation plans systematically using isolated git worktrees with continuous quality verification.

## Usage

```
/polyglot:work [plan reference or inline instructions]
```

## Process

### Phase 1: Setup

1. **Plan Loading**
   - Load the specified plan
   - Verify all tasks are clear
   - Check for blocking dependencies

2. **Environment Preparation**
   ```bash
   # Create feature branch
   git checkout -b feature/<plan-name>

   # Optional: Create isolated worktree
   git worktree add ../worktree-<plan-name> -b feature/<plan-name>
   ```

3. **Dependency Installation**
   - Install any new dependencies specified in plan
   - Verify build passes before starting

### Phase 2: Execution Loop

For each task in the plan:

1. **Pre-Implementation**
   - Read relevant existing code
   - Understand the context
   - Plan the specific changes

2. **Implementation**
   - Write code following project patterns
   - Add/update types and interfaces
   - Follow language-specific best practices

3. **Testing**
   - Write unit tests for new code
   - Update existing tests if needed
   - Run full test suite

4. **Verification**
   ```bash
   # TypeScript
   npm run lint && npm run type-check && npm test

   # Python
   ruff check . && mypy . && pytest

   # Java
   ./mvnw verify
   ```

5. **Commit**
   ```bash
   git add <files>
   git commit -m "feat(<scope>): <description>"
   ```

### Phase 3: Completion

1. **Final Verification**
   - Run all tests
   - Build the project
   - Check for any regressions

2. **Cleanup**
   ```bash
   # If using worktree
   cd ..
   git worktree remove worktree-<plan-name>
   ```

3. **Prepare for Review**
   - Push branch to remote
   - Create draft PR if configured

## Execution Modes

### Standard Mode
Execute all tasks sequentially with verification.

### Parallel Mode
Execute independent tasks in parallel (use with caution).

### Step Mode
Execute one task at a time, requiring confirmation between tasks.

## Output Format

```markdown
# Work Session Report

## Plan: [Plan Name]
**Branch**: feature/<name>
**Started**: [timestamp]
**Completed**: [timestamp]

## Task Progress

### Task 1: [Name]
- **Status**: Complete ✓
- **Files Changed**:
  - `src/file.ts` - Added new function
  - `tests/file.test.ts` - Added tests
- **Commit**: abc1234
- **Notes**: Any relevant observations

### Task 2: [Name]
- **Status**: Complete ✓
...

## Quality Metrics
- Tests: All passing (50/50)
- Lint: No issues
- Type Check: No errors
- Build: Successful

## Commits Made
| Hash | Message |
|------|---------|
| abc1234 | feat(auth): add login endpoint |
| def5678 | test(auth): add login tests |

## Next Steps
- [ ] Push to remote: `git push -u origin feature/<name>`
- [ ] Create PR for review
- [ ] Run /polyglot:review for code review
```

## Error Handling

### Test Failure
```markdown
## Task Blocked: Test Failure

**Task**: Task name
**Error**:
```
Error message here
```

**Attempted Fixes**:
1. Tried X
2. Tried Y

**Recommendation**: [What to do next]
```

### Build Failure
```markdown
## Task Blocked: Build Failure

**Error Type**: [Type/Compile/etc]
**Error**:
```
Error message
```

**Likely Cause**: Analysis
**Suggested Fix**: Recommendation
```

## Git Worktree Usage

For isolation during complex work:

```bash
# Create worktree
git worktree add ../feature-workspace -b feature/my-feature

# Work in isolated environment
cd ../feature-workspace

# Complete work and return
cd ../main-repo
git worktree remove ../feature-workspace
```

Benefits:
- Clean working directory
- Easy to abandon if needed
- Multiple features in parallel

## Best Practices

1. **Atomic Commits**: One logical change per commit
2. **Test First**: Write tests before or alongside code
3. **Verify Often**: Run tests after each change
4. **Small Steps**: Break large changes into smaller commits
5. **Clean History**: Use meaningful commit messages
