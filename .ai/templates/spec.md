# [Feature Name]

> status: draft | review | approved | done
> date: YYYY-MM-DD
> author: [who wrote the spec]

---

## Why
[1–2 sentences: problem being solved and why now]

---

## What
[Concrete deliverable — specific enough to verify when done]

---

## Acceptance Criteria

> Written in Given/When/Then format. These are the pass/fail gates.

**AC1:** [Short label]
```
Given: [precondition / system state]
When:  [action taken]
Then:  [expected outcome, observable and verifiable]
```

**AC2:** [Short label]
```
Given:
When:
Then:
```

**AC3 (error case):** [Short label]
```
Given: [invalid input or failure condition]
When:  [action taken]
Then:  [error returned, no side effects]
```

---

## Constraints

### Must
-

### Must Not
- No new dependencies unless listed here
- Do not modify unrelated code

### Out of Scope
-

---

## Dependencies
- Blocked by: [spec or ticket, or "none"]
- Depends on: [service, API, data, or "none"]

---

## Current State
- Relevant files: `path/to/file.ts`
- Patterns to follow: `path/to/example.ts`
- Existing conventions:

---

## Tasks

### T1: [Title]
**What:**
**Files:** `path/to/file.ts`, `path/to/file.test.ts`
**Verify:** `npm test -- file.test.ts`

### T2: [Title]
**What:**
**Files:**
**Verify:**

### T3: [Title]
**What:**
**Files:**
**Verify:**

---

## Validation
End-to-end check after all tasks complete:

- `npm test`
- Manual: [what to verify in UI/API]
- All Acceptance Criteria above: [ ] AC1  [ ] AC2  [ ] AC3

---

## Rollback
[How to undo this change if it causes issues in production]
- Feature flag: yes / no
- DB migration: reversible / irreversible
- Steps to revert:
