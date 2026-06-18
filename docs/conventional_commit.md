# Conventional Commits Best Practices

## What are Conventional Commits?

Conventional Commits provide a standard format for commit messages.

Benefits:

* Easy to understand Git history
* Better code reviews
* Automatic changelog generation
* Semantic versioning support
* Cleaner release notes
* Consistent team workflow

---

# Commit Format

```text
<type>(optional-scope): <description>
```

Examples:

```text
feat(auth): add login endpoint

fix(cart): handle null quantity

fix(security): prevent path traversal attack

docs(readme): update setup instructions

refactor(product): simplify filtering logic
```

---

# Most Common Commit Types

## feat

New feature.

```text
feat(auth): add JWT authentication

feat(cart): add bulk remove functionality

feat(product): add search API
```

---

## fix

Bug fix.

```text
fix(auth): validate refresh token

fix(cart): correct quantity calculation

fix(product): handle missing image URL
```

---

## fix(security)

Security-related fix.

```text
fix(security): prevent SQL injection

fix(security): sanitize file paths

fix(security): replace external CDN script

fix(security): add integrity validation
```

Use this for:

* CodeQL findings
* Security vulnerabilities
* Authentication issues
* Authorization issues

---

## docs

Documentation changes only.

```text
docs(readme): add setup instructions

docs(api): update endpoint examples
```

---

## refactor

Code changes without changing functionality.

```text
refactor(auth): simplify token validation

refactor(product): extract search service
```

---

## test

Add or update tests.

```text
test(auth): add login service tests

test(cart): cover edge cases
```

---

## chore

Maintenance work.

```text
chore: update dependencies

chore: upgrade node version

chore: configure eslint
```

---

## ci

CI/CD changes.

```text
ci: add GitHub Actions workflow

ci: update deployment pipeline
```

---

## perf

Performance improvements.

```text
perf(search): optimize product query

perf(cart): reduce database calls
```

---

## build

Build-related changes.

```text
build: update webpack configuration

build: migrate to vite
```

---

# Scope Guidelines

Format:

```text
type(scope): description
```

Examples:

```text
feat(auth): add login endpoint

fix(cart): resolve tax calculation issue

refactor(product): simplify search logic

test(user): add profile tests
```

Common scopes:

```text
auth
cart
product
order
user
payment
search
api
security
ui
```

---

# Description Guidelines

## Good

```text
fix(auth): validate JWT expiration

feat(cart): add bulk item removal

fix(security): prevent path traversal attack
```

## Bad

```text
fixed bug

changes

update

last fix

final change

testing
```

---

# Use Imperative Mood

Think:

```text
If applied, this commit will...
```

Examples:

```text
fix(auth): validate JWT expiration

feat(product): add category filter

refactor(order): extract service layer
```

Avoid:

```text
fixed JWT issue

added category filter

refactored service
```

---

# Commit Size Best Practices

## Good

One logical change per commit.

Example:

```text
feat(auth): add login endpoint
```

---

## Bad

One commit containing:

```text
Login changes
Cart changes
UI changes
Dependency updates
```

---

# Examples for CodeQL Work

## SQL Injection

```text
fix(security): use parameterized queries for user lookup
```

## Command Injection

```text
fix(security): validate host input before command execution
```

## Path Traversal

```text
fix(security): restrict file access to uploads directory
```

## SSRF

```text
fix(security): allowlist outbound request hosts
```

## External Script Loading

```text
fix(security): replace CDN script with local asset
```

---

# Commiting Review Changes

Example:

Reviewer says:

```text
Add validation
```

Commit:

```text
fix(auth): add input validation for login request
```

Avoid:

```text
review changes

address comments

fix review
```

---

# Interactive Rebase Before PR

Clean up messy commits:

Before:

```text
fix

fix again

oops

last fix

review update
```

Use:

```bash
git rebase -i develop
```

After:

```text
fix(auth): add login validation
```

---

# Recommended Types for Daily Work

You will use these 90% of the time:

```text
feat
fix
fix(security)
refactor
docs
test
chore
```

---

# Examples from Real Projects

```text
feat(auth): add refresh token endpoint

fix(cart): correct VAT calculation

fix(security): prevent path traversal in file download

refactor(product): extract search repository

test(order): add order creation tests

docs(api): update authentication examples

chore: update dependencies
```

---

# Golden Rules

* Use lowercase commit types.
* Keep description under ~72 characters.
* Use meaningful scope.
* One logical change per commit.
* Use `fix(security)` for CodeQL/security work.
* Avoid generic commit messages.
* Squash noisy commits before review.
* Make commit history tell a story.

## Recommended Format

```text
feat(scope): description

fix(scope): description

fix(security): description

refactor(scope): description
```
