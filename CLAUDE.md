# CLAUDE.md

## Workflow
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways: STOP and re-plan — do not keep pushing
- Write detailed specs upfront to reduce ambiguity
- Use subagents to keep main context window clean — one task per subagent

## Code Quality
- Simplicity first — make every change as simple as possible, minimal code impact
- No laziness — find root causes, no temporary fixes, senior developer standards
- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution"
- Skip elegance check for simple, obvious fixes — don't over-engineer

## Verification
- Never mark a task complete without proving it works
- Run tests, check logs, demonstrate correctness
- Ask yourself: "Would a staff engineer approve this?"

## Bug Fixing
- When given a bug report: just fix it, don't ask for hand-holding
- Point at logs, errors, failing tests — then resolve them
- Go fix failing CI tests without being told how

## Self-Improvement
- After ANY correction from the user: update `tasks/lessons.md` with the pattern
- Write rules for yourself that prevent the same mistake
- Review lessons at session start for relevant project

## Spec-Driven Development
- For any non-trivial task: spec file must exist at `specs/<feature>.md` before writing code
- Spec must have `status: approved` — draft is not enough
- Show the spec to the user and wait for confirmation before implementing
- If the user skips spec and asks for code directly: write the spec first, then confirm

## Never
- Modify unrelated code
- Install new dependencies without asking
- Leave TODO / FIXME without flagging it in the task summary
- Swallow errors silently in try/catch
- Write implementation code without an approved spec for non-trivial features
- Mark a task done if any Acceptance Criteria from the spec are unverified