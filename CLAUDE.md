# Coding Principles

## 1. Think Before Coding

Before implementing:
- State assumptions that affect correctness.
- If multiple interpretations exist, present them briefly.
- If ambiguity changes the solution, ask before coding.
- If ambiguity is minor, state the assumption and proceed with the simplest safe option.
- Prefer the simpler approach. Push back on unnecessary complexity.

## 2. Simplicity First

Write Use as little code as possible that solves the problem.
- No speculative features.
- No abstractions for single-use logic.
- No unnecessary configurability.
- No error handling for impossible scenarios.
- If the solution feels overbuilt, simplify it.

## 3. Surgical Changes

When editing existing code:
- Follow with SOLID, Clean architecture
- Touch only files and lines required by the request.
- Do not refactor unrelated code.
- Do not reformat unrelated code.
- Match the existing style.
- Remove only unused imports, variables, or functions caused by your own changes.
- Mention unrelated issues instead of fixing them.

Every changed line should trace directly to the request.

## 4. Goal-Driven Execution

Turn tasks into verifiable goals.

Examples:
- "Fix bug" → reproduce with a test or clear failing case, then fix.
- "Add validation" → test invalid inputs, then implement.
- "Refactor" → confirm behavior before and after.

For multi-step tasks, state:
1. Step → verification
2. Step → verification
3. Step → verification

## 5. Project Awareness

Before coding:
- Read nearby code.
- Check existing patterns.
- Check relevant tests.
- Check project docs/config when needed.

Do not invent project conventions.

## 6. Verification

After changes:
- Run the smallest relevant test or check.
- Run broader checks only when justified.
- If verification cannot be run, say exactly why.
- Do not claim success without evidence.

## 7. Reporting Back

When finished, report:
- What changed.
- How it was verified.
- Any remaining risk, only if relevant.
- Minimal report 
## 8. Skills
- use ponytail skill and openspec if needed
