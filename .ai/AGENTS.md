# AGENTS.md

> Detailed workflow for this project.
> Lives in `.ai/` — read this after CLAUDE.md.

---

## Session Start

Read in this order before ANY task:

1. `docs/srs.md` — what the system does
2. `docs/architecture.md` — current structure and decisions
3. `docs/patterns.md` — conventions, algorithms, clean code rules
4. `tasks/lessons.md` — mistakes already made in this project
5. `specs/_index.md` — all existing specs and their status
6. `specs/<feature>.md` — if a specific feature is mentioned

Do not start any task until steps 1–5 are complete.

---

## Spec Gate — Hard Rule

**No implementation code may be written until:**

- [ ] A spec file exists at `specs/<feature>.md`
- [ ] The spec has `status: approved` in its header
- [ ] The spec entry is added to `specs/_index.md`

If the user jumps straight to "write the code": pause, ask ONE question to confirm scope, then write the spec first. Only proceed to code after the spec exists.

If requirements are unclear: ask ONE clarifying question, then fill the spec. Do not ask multiple questions in one message.

---

## Definition of Done

A task is done when ALL of these are true:

- [ ] All spec tasks (T1, T2, …) are checked off
- [ ] All acceptance criteria pass (run the verify commands from spec)
- [ ] Tests: happy path, error path, edge cases, failure scenarios
- [ ] No `TODO` / `FIXME` left without flagging in task summary
- [ ] `specs/_index.md` updated with status: `done` and date
- [ ] `docs/` updated if architecture or patterns changed
- [ ] Pre-commit scan passed (see scan table below)

---

## Workflow: Non-trivial Feature

> Use this for: new endpoint, new service, new data model, anything 3+ steps.

```
1. Design      → fill templates/design.md (7 questions)
2. Spec        → write specs/<feature>.md using templates/spec.md
                 set status: draft, show to user for approval
3. Gate        → user confirms spec → change status to: approved
4. Plan        → write tasks/todo.md with checkable items
5. TDD         → write failing tests first, then implement (see templates/tdd.md)
6. Verify      → run acceptance criteria from spec, all must pass
7. Update docs → if structure or patterns changed, update docs/
8. Close spec  → mark status: done in spec file and specs/_index.md
9. Lessons     → if any correction was made, update tasks/lessons.md
```

If requirements are ambiguous at step 1: ask ONE clarifying question, then proceed.
Never skip step 3 — coding before approval = restart from design.

---

## Workflow: Simple Task

> Use this for: bug fix, small change, single file edit.

```
1. Plan   → write tasks/todo.md (even if 2–3 lines)
2. Fix    → root cause only, no temporary fixes
3. Verify → test passes, log is clean
```

---

## Design Before Code

For non-trivial work, fill `templates/design.md` before writing any spec or code.

The 7 questions:

```
1. Data model     — fields, types, relations
2. Contracts      — function signatures and return types (pseudocode only)
3. Happy path     — step by step when everything works
4. Error path     — what to return/throw for each failure condition
5. What if fails  — DB down, timeout, concurrent writes, API null
6. Scale          — N+1 risk, indexes, cache, pagination strategy
7. Security       — auth layer, user isolation, input sanitization
```

If you skip this step and it surfaces during review: revert and redo properly.

---

## TDD Cycle

For every task that has a Verify step:

```
1. Write the test first — describe expected behavior
2. Run it — confirm it fails (red)
3. Implement minimum code to pass
4. Run again — confirm it passes (green)
5. Refactor if needed — tests must still pass
```

Test coverage required per task:

```
✓ Happy path
✓ Error path (invalid input, not found, conflict)
✓ Edge cases (null, empty, boundary values)
✓ Failure scenarios (DB down, timeout, concurrent writes)
```

Use `templates/tdd.md` for the test plan.

---

## Persistent Docs — Update After Every Feature

After a feature is merged, update these if relevant:

| File                  | Update when                                      |
|-----------------------|--------------------------------------------------|
| `docs/srs.md`         | Scope or requirements changed                    |
| `docs/architecture.md`| New component, new decision, structure changed   |
| `docs/patterns.md`    | New pattern introduced or existing one changed   |
| `docs/lessons.md`     | Architectural / perf / security lesson learned   |
| `specs/_index.md`     | Always — add every new spec with status and date |

Specs are permanent records. Do not delete after completion.

---

## Lessons Format

When writing to `tasks/lessons.md` or `docs/lessons.md`:

```markdown
## [YYYY-MM-DD] — [Short title]

**Context:** What feature/task was this?
**Mistake:** What went wrong?
**Root cause:** Why did it happen?
**Rule:** What prevents this in the future?
**Category:** performance | error-handling | architecture | security | algorithm
```

Graduate a lesson from `tasks/lessons.md` to `docs/lessons.md`
when it applies broadly beyond the current task.

---

## Scale & Maintainability — Pre-commit Scan

Before marking any task done, scan for these signals.
If found: add `// REVIEW: <reason>` inline and mention in task summary.

| Signal                                    | Action                              |
|-------------------------------------------|-------------------------------------|
| List query with no LIMIT                  | Add pagination or flag              |
| Loop with DB or API call inside           | Refactor to batch or join           |
| Hardcoded config or magic number          | Move to env / named constant        |
| try/catch that swallows error silently    | Log + propagate or return Result    |
| Function longer than ~30 lines            | Suggest split                       |
| TODO / FIXME in code                      | Flag before marking done            |
| Shared mutable state between async calls  | Flag race condition risk            |
| External API call with no timeout         | Add explicit timeout                |
| Multiple DB writes without transaction    | Wrap in transaction                 |

---

## File Structure

```
.ai/
├── AGENTS.md              ← this file
├── docs/
│   ├── srs.md             ← system requirements (update when scope changes)
│   ├── architecture.md    ← decisions, diagrams, component map
│   ├── patterns.md        ← conventions, algorithms, clean code rules
│   └── lessons.md         ← broad architectural / perf / security lessons
├── specs/
│   ├── _index.md          ← all specs: name | status | date
│   └── <feature>.md       ← one file per feature, permanent
├── tasks/
│   ├── todo.md            ← current plan with checkable items
│   └── lessons.md         ← session-level lessons
└── templates/
    ├── design.md          ← 7 design questions
    ├── spec.md            ← feature spec template
    └── tdd.md             ← test plan template
```