# CODEQL_WORKFLOW.md

# CodeQL Remediation Workflow (Fork + Develop + Rebase & Merge)

## Repository Structure

```text
Company Repository (upstream)
        ↓
Your Fork (origin)
        ↓
Local Clone
```

Target Branch:

```text
develop
```

Merge Strategy:

```text
Rebase and Merge
```

---

# Alert Investigation Process

For every CodeQL alert:

```text
1. Open Alert
2. Read Rule Name
3. Identify Source
4. Identify Sink
5. Understand Attack Scenario
6. Verify Exploitability
7. Classify:
   - True Positive
   - False Positive
   - Accepted Risk
8. Fix
9. Verify
10. Create PR
```

---

# Alert Classification

## True Positive

Real vulnerability exists.

Example:

```js
const query =
 `SELECT * FROM users WHERE id=${id}`;
```

Action:

```text
Fix Required
```

---

## False Positive

Tool reports issue but code is already safe.

Example:

```js
const id = parseInt(req.query.id, 10);
```

Action:

```text
Document and Dismiss
```

---

## Accepted Risk

Risk exists but organization accepts it.

Example:

```html
<script src="approved-company-cdn.js"></script>
```

Action:

```text
Document Business Justification
```

---

# Common CodeQL Vulnerabilities

## SQL Injection

Source:

```js
req.query
```

Sink:

```js
db.query()
```

Fix:

```js
Parameterized Queries
```

---

## Command Injection

Source:

```js
req.query.host
```

Sink:

```js
exec()
```

Fix:

```js
spawn()
Input Validation
```

---

## Path Traversal

Source:

```js
req.query.filename
```

Sink:

```js
fs.readFileSync()
```

Fix:

```js
path.resolve()
Allowlist
```

---

## SSRF

Source:

```js
req.query.url
```

Sink:

```js
axios.get()
```

Fix:

```js
Allowlist URLs
```

---

## XSS

Source:

```js
User Input
```

Sink:

```js
dangerouslySetInnerHTML
```

Fix:

```js
Output Encoding
React Safe Rendering
```

---

# Starting a CodeQL Fix

## Sync Develop

```bash
git checkout develop

git fetch upstream

git rebase upstream/develop

git push origin develop
```

---

## Create Branch

```bash
git checkout -b fix/codeql-alert
```

Examples:

```text
fix/codeql-sql-injection
fix/codeql-path-traversal
fix/codeql-untrusted-source
```

---

## Commit

```bash
git commit -m "fix(security): prevent path traversal in file download"
```

---

## Push

```bash
git push origin fix/codeql-alert
```

---

## Create PR

Title:

```text
fix(security): resolve CodeQL path traversal alert
```

---

# Rebase Rules

## Branch Up To Date

```text
PR Open
Branch Current
```

Action:

```text
No Rebase Needed
```

---

## Branch Outdated

GitHub Shows:

```text
Branch is out of date
```

Action:

```bash
git checkout develop

git fetch upstream

git rebase upstream/develop

git checkout fix/codeql-alert

git rebase develop

git push --force-with-lease
```

---

# After Merge

```bash
git checkout develop

git fetch upstream

git rebase upstream/develop

git branch -d fix/codeql-alert
```

---

# Golden Rules

```text
✓ Understand alert before fixing

✓ Never blindly dismiss findings

✓ Verify locally

✓ Verify CodeQL rerun

✓ Verify alert closure

✓ Use fix(security): commit messages

✓ Delete merged branches
```
