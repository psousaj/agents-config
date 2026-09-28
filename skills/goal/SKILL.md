---
name: goal
description: "Use when executing SDD loop over specs and tickets."
---

# Goal (Autonomous SDD Loop)

Executes an autonomous implementation loop driven strictly by specifications and ticket breakdowns.

## Prerequisites Check (Strict Guard)

Before writing any code or making edits, verify that the repository has:

1. **Spec Source:** An existing spec file (e.g. `docs/specs/*.md`, `specs/*.md`, or a referenced requirement document).
2. **Tickets / Tasks:** Defined tasks/tickets in the issue tracker (`docs/agents/issue-tracker.md`) or a structured task list in the plan.

If either is missing, refuse to implement blindly. Stop and ask the user to generate the spec and tickets first.

---

## Workflow

### 1. Build the Execution Queue
- Parse the spec and ticket list into an ordered sequence (Task 1..N).
- Detect the project tech stack and preload relevant domain/language skills (e.g. `@golang` for Go, `@astro-guidelines` for Astro, or user-specified skills).
- Present the planned queue and begin with Task 1.

### 2. Task Iteration Loop (Per Task)
For each task in sequential order:

1. **Implement (`/implement`):**
   - Apply the language/stack skills (e.g. `@golang`).
   - Implement the feature/fix along with corresponding tests (`_test.go`, `.test.ts`, etc.).
   - Verify compilation and unit tests pass.

2. **Review (`/code-review`):**
   - Run a two-axis review (`Standards` + `Spec`).
   - Check if standards or requirements were violated or if scope creep occurred.

3. **Iterate until Clean:**
   - If findings exist: fix them via `/implement` and re-run `/code-review`.
   - Repeat until the review passes 100% clean with zero unresolved issues.

4. **Advance:**
   - Mark task completed and proceed directly to the next task.

---

### 3. Global Verification
When all tasks are finished:
- Run full test suite with race detectors/coverage (e.g. `go test -race ./...`).
- Run project linters and typechecks (`golangci-lint`, `tsc`, etc.).
- Run a final consolidated `/code-review` across all changed files against the base branch.
- Output a summary of all executed tasks and verification evidence.