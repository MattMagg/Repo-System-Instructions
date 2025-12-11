---
description: Systematically review pull requests and commits for code quality, correctness, and project alignment
---

# Pull Request Review Workflow

## Workflow Variables

Before starting, establish these inputs:

| Variable | Required | Description |
|----------|----------|-------------|
| `PR_NUMBER` | Yes* | PR number to review (e.g., `42`) |
| `BRANCH_NAME` | Yes* | Branch name if no PR exists (e.g., `feature/new-auth`) |
| `REVIEW_DEPTH` | No | `quick` (15 min) or `comprehensive` (45+ min). Default: `comprehensive` |
| `FOCUS_AREAS` | No | Comma-separated categories to prioritize (e.g., `security,performance`) |

*One of `PR_NUMBER` or `BRANCH_NAME` is required.

---

## Phase 1: Context Gathering

### 1.1 Fetch PR Metadata (if PR exists)

```bash
# Get PR details
gh pr view $PR_NUMBER --json title,body,author,baseRefName,headRefName,additions,deletions,changedFiles,labels,reviewDecision

# Get PR diff
gh pr diff $PR_NUMBER

# List PR files changed
gh pr view $PR_NUMBER --json files --jq '.files[].path'

# Get existing review comments
gh pr view $PR_NUMBER --json reviews,comments
```

### 1.2 Fetch Commit History

```bash
# Get commits in PR
gh pr view $PR_NUMBER --json commits --jq '.commits[] | "\(.oid[:7]) \(.messageHeadline)"'

# Or for branch comparison
git log main..$BRANCH_NAME --oneline

# Get detailed commit info
git log main..$BRANCH_NAME --stat
```

### 1.3 Understand the Change

- [ ] Read PR title, description, and linked issues
- [ ] Identify the **purpose** of the change (feature, bugfix, refactor, docs)
- [ ] Note any special instructions from the author
- [ ] Check if this is a draft or ready for review

---

## Phase 2: Commit Analysis

### 2.1 Commit Message Quality

For each commit, verify:

- [ ] **Format**: Subject line ≤72 chars, imperative mood ("Add" not "Added")
- [ ] **Clarity**: Message explains *what* and *why*, not just *how*
- [ ] **Scope**: Each commit is atomic (single logical change)
- [ ] **References**: Includes issue/ticket number if applicable

```bash
# View full commit messages
git log main..$BRANCH_NAME --format=fuller
```

### 2.2 Commit Structure

- [ ] **Atomic commits**: Each commit compiles and passes tests independently
- [ ] **Logical ordering**: Commits build on each other sensibly
- [ ] **No fixup commits**: Squash or amend should have been done pre-review
- [ ] **No merge commits**: Prefer rebase for clean history (if project standard)

---

## Phase 3: Code Review Checklist

### 3.1 Code Quality

- [ ] **Logic correctness**: Does the code do what it claims?
- [ ] **Edge cases**: Are boundary conditions handled?
- [ ] **Error handling**: Are errors caught, logged, and handled gracefully?
- [ ] **DRY principle**: Is there unnecessary duplication?
- [ ] **Readability**: Can another developer understand this in 6 months?
- [ ] **Naming**: Are variables, functions, and classes named clearly?
- [ ] **Complexity**: Are functions reasonably short? Is cyclomatic complexity low?

```bash
# Search for TODO/FIXME/HACK markers
git diff main..$BRANCH_NAME | grep -E "(TODO|FIXME|HACK|XXX)"
```

### 3.2 Security

- [ ] **Input validation**: Are all external inputs validated/sanitized?
- [ ] **SQL injection**: Are queries parameterized?
- [ ] **XSS prevention**: Is user content escaped in templates?
- [ ] **Secrets exposure**: No hardcoded API keys, passwords, or tokens?
- [ ] **Dependency vulnerabilities**: Are new deps audited?
- [ ] **Authentication/Authorization**: Are access controls correctly applied?
- [ ] **Sensitive data**: Is PII/PHI logged or exposed inappropriately?

```bash
# Check for potential secrets
git diff main..$BRANCH_NAME | grep -iE "(password|secret|api_key|token|private_key)" 

# Audit new dependencies
npm audit  # or yarn audit, pip-audit, etc.
```

### 3.3 Testing

- [ ] **Coverage**: Are new code paths tested?
- [ ] **Edge cases**: Do tests cover boundary conditions?
- [ ] **Negative cases**: Are failure scenarios tested?
- [ ] **Test quality**: Are tests clear, maintainable, not brittle?
- [ ] **Test isolation**: No shared state between tests?
- [ ] **Mocking**: Are external dependencies appropriately mocked?

```bash
# Run tests
npm test  # or project-specific command

# Check coverage impact
npm run test -- --coverage
```

### 3.4 Documentation

- [ ] **Code comments**: Are complex sections explained?
- [ ] **JSDoc/docstrings**: Are public APIs documented?
- [ ] **README updates**: Does this change require README changes?
- [ ] **API documentation**: Are new endpoints documented?
- [ ] **Changelog**: Is this change noted if required?
- [ ] **Migration guides**: Are breaking changes documented?

### 3.5 Style & Conventions

- [ ] **Linting**: Does code pass lint checks?
- [ ] **Formatting**: Is code formatted per project standards?
- [ ] **Patterns**: Does code follow existing codebase patterns?
- [ ] **File organization**: Are files in correct locations?
- [ ] **Import ordering**: Are imports organized consistently?
- [ ] **Type safety**: Are TypeScript types used appropriately (no `any` abuse)?

```bash
# Run linters
npm run lint

# Type check
npx tsc --noEmit
```

### 3.6 Performance

- [ ] **N+1 queries**: Are database queries efficient?
- [ ] **Memory leaks**: Are resources properly cleaned up?
- [ ] **Bundle size**: Does this significantly increase bundle?
- [ ] **Caching**: Are cacheable operations cached?
- [ ] **Lazy loading**: Are heavy resources loaded on demand?
- [ ] **Algorithmic complexity**: Are there O(n²) or worse operations on large data?

```bash
# Check bundle size impact (if applicable)
npm run build && du -sh dist/
```

---

## Phase 4: Contextual Verification

### 4.1 Cross-File Impact

Use codebase search to verify:

```bash
# Find usages of modified functions
# Use codebase_search or grep_search tools

# Check for breaking interface changes
git diff main..$BRANCH_NAME -- "*.ts" | grep -E "^[\+\-].*export (function|interface|type|class)"
```

- [ ] Do changes to shared functions break callers?
- [ ] Are interface changes reflected in all implementations?
- [ ] Are type changes propagated correctly?

### 4.2 Integration Points

- [ ] Database migrations: Are they reversible? Tested?
- [ ] API contracts: Are changes backward compatible?
- [ ] Configuration: Are new env vars documented?
- [ ] Feature flags: Is new functionality behind a flag if needed?

---

## Phase 5: Review Depth Adjustments

### Quick Review (15 min)
Focus on:
1. Security issues (Phase 3.2)
2. Obvious bugs in logic (Phase 3.1 - logic correctness only)
3. Test existence (not quality)
4. Commit message format

### Comprehensive Review (45+ min)
Complete all phases, plus:
- Run the code locally if possible
- Test manual scenarios
- Review performance implications
- Check for architectural concerns

### Focused Review (specific areas)
If `FOCUS_AREAS` specified, prioritize those sections and do cursory review of others.

---

## Phase 6: Compile Review Summary

### 6.1 Structure Your Findings

Create a structured summary with these sections:

```markdown
## PR Review: #$PR_NUMBER - $TITLE

### Summary
[1-2 sentence overview of the change and its purpose]

### Recommendation
**[APPROVE | REQUEST_CHANGES | COMMENT]**

### Key Findings

#### 🔴 Blocking Issues (must fix)
- [Issue description with file:line reference]

#### 🟡 Suggestions (should consider)
- [Suggestion with rationale]

#### 🟢 Nitpicks (optional)
- [Minor style/preference notes]

### Tested
- [ ] Ran `npm run build`
- [ ] Ran `npm test`
- [ ] Manual verification: [describe what you tested]

### Checklist Summary
| Category | Status | Notes |
|----------|--------|-------|
| Code Quality | ✅/⚠️/❌ | |
| Security | ✅/⚠️/❌ | |
| Testing | ✅/⚠️/❌ | |
| Documentation | ✅/⚠️/❌ | |
| Style | ✅/⚠️/❌ | |
| Performance | ✅/⚠️/❌ | |
```

### 6.2 Decision Criteria

| Recommendation | When to Use |
|----------------|-------------|
| **APPROVE** | No blocking issues; suggestions are minor |
| **REQUEST_CHANGES** | Blocking issues exist (bugs, security, missing tests for critical paths) |
| **COMMENT** | Questions need answers before deciding; or non-blocking feedback only |

---

## Phase 7: Submit Review

### 7.1 Post Inline Comments

```bash
# Add line comment
gh pr review $PR_NUMBER --comment --body "Comment on specific line" 

# Or use the GitHub web UI for inline comments
```

### 7.2 Submit Overall Review

```bash
# Approve
gh pr review $PR_NUMBER --approve --body "LGTM! [summary]"

# Request changes
gh pr review $PR_NUMBER --request-changes --body "[structured summary from Phase 6]"

# Comment only
gh pr review $PR_NUMBER --comment --body "[structured summary from Phase 6]"
```

---

## Quick Reference Commands

```bash
# View PR
gh pr view $PR_NUMBER

# View diff
gh pr diff $PR_NUMBER

# Checkout PR locally
gh pr checkout $PR_NUMBER

# List files changed
gh pr view $PR_NUMBER --json files --jq '.files[].path'

# View commits
gh pr view $PR_NUMBER --json commits

# Compare branches
git diff main..$BRANCH_NAME --stat
git log main..$BRANCH_NAME --oneline

# Run local verification
npm run lint && npm run build && npm test
```
