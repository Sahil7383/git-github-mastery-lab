# GITHUB_PR_BEST_PRACTICES.md

# Pull Request Best Practices

## Standard Workflow

```text
Sync Develop
      ↓
Create Branch
      ↓
Implement Change
      ↓
Commit
      ↓
Push
      ↓
Create PR
      ↓
Review
      ↓
Rebase & Merge
      ↓
Delete Branch
```

---

# Branch Naming

## Feature

```text
feature/user-login
feature/product-search
```

## Fix

```text
fix/cart-total
fix/codeql-alert
```

## Refactor

```text
refactor/user-service
```

## Docs

```text
docs/setup-guide
```

## Chore

```text
chore/update-dependencies
```

---

# Conventional Commits

## Feature

```text
feat(auth): add login endpoint
```

## Fix

```text
fix(cart): handle null quantity
```

## Security

```text
fix(security): prevent path traversal attack
```

## Refactor

```text
refactor(product): simplify filtering logic
```

---

# PR Title Format

```text
feat(auth): add login functionality

fix(security): resolve CodeQL alert

refactor(product): simplify product service
```

---

# PR Description Template

Issue:

* What problem exists?

Fix:

* What was changed?

Validation:

* How was it tested?

Example:

Issue:
CodeQL flagged external script loaded from CDN.

Fix:
Moved script to locally hosted asset.

Validation:
Application tested successfully.

---

# Review Scenarios

## Scenario 1: Approved

Action:

```text
Rebase & Merge
```

---

## Scenario 2: Changes Requested

Action:

```text
Update Same Branch
Push Again
```

Do NOT:

```text
Create New Branch
Create New PR
```

---

## Scenario 3: Branch Outdated

Action:

```bash
git checkout develop

git fetch upstream

git rebase upstream/develop

git checkout feature/my-feature

git rebase develop

git push --force-with-lease
```

---

# Merge Conflict Resolution

When:

```bash
git rebase develop
```

conflict occurs:

Resolve file.

Then:

```bash
git add .

git rebase --continue
```

Repeat until complete.

---

# CI Failure

Never request approval while:

```text
❌ Tests Failed

❌ Lint Failed

❌ Build Failed
```

Fix first.

---

# CodeQL Failure

Process:

```text
Open Finding
Identify Source
Identify Sink
Fix Root Cause
Push
Verify Rerun
```

---

# PR Size Guidelines

Good:

```text
50-500 lines
Single Purpose
```

Avoid:

```text
Multiple Features
Thousands of Lines
Mixed Refactors
```

---

# Senior Engineer PR Checklist

## Code Quality

```text
Readable?
Maintainable?
Simple?
```

## Security

```text
Input Validation?
Authorization?
Secrets?
CodeQL Findings?
```

## Performance

```text
Extra Queries?
N+1 Problems?
Large Loops?
```

## Testing

```text
Unit Tests?
Manual Testing?
Edge Cases?
```

---

# Rebase & Merge Guidelines

Use:

```text
Rebase & Merge
```

Benefits:

```text
✓ Linear History

✓ No Merge Commits

✓ Cleaner Git Log

✓ Easier Debugging
```

---

# Golden Rules

```text
✓ One Branch = One Purpose

✓ One PR = One Change

✓ Small PRs

✓ Meaningful Commit Messages

✓ Keep Branch Updated

✓ Use --force-with-lease

✓ Fix CI Before Review

✓ Fix Security Findings

✓ Delete Merged Branches

✓ Sync Develop Before New Work
```
