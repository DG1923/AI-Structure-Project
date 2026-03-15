# patterns.md

> Conventions, algorithms, and clean code rules for this project.
> AI reads this at session start. Update when a new pattern is introduced or changed.

---

## Naming

- Files: `kebab-case.ts`
- Functions: `camelCase`
- Types / Interfaces: `PascalCase`
- Constants: `UPPER_SNAKE_CASE`
- Test files: `<name>.test.ts` (unit), `<name>.integration.test.ts` (integration)

---

## Function design

- One function = one responsibility
- Max ~30 lines per function — if longer, split
- Return `Result<T, E>` for operations that can fail — do not throw silently
- Pure functions where possible; isolate side effects at boundaries
- No default exports — named exports only

---

## Error handling

- Never swallow errors in `try/catch` — log + propagate or return `Result`
- All external API calls: set explicit timeout
- DB writes that depend on each other: wrap in a transaction
- Use typed error classes (not plain `Error`) so callers can distinguish them

---

## Data access

- No raw queries inline in business logic — use a repository/service layer
- Add LIMIT to all list queries — never unbounded
- Batch DB calls when looping over collections (no N+1)
- Index required on any field used in a WHERE clause at scale

---

## Testing conventions

- Test file lives next to the source file
- Describe blocks mirror the function name: `describe('functionName', ...)`
- Every test: arrange → act → assert, no logic in assertions
- Mock at the boundary (DB, HTTP) — do not mock internal functions
- Failure tests are required, not optional

---

## Security defaults

- Validate all external input at system boundaries
- No secrets in code or logs — use env vars
- Parameterize all DB queries — no string interpolation
- Auth check before any data access

---

<!-- Add new patterns here as the project evolves -->
