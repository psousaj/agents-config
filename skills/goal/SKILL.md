---
name: goal
description: "Use when executing SDD loop over specs and tickets."
---

# Goal (Autonomous SDD Loop)

Executes an autonomous implementation loop driven strictly by specifications and ticket breakdowns.

## Strict clarification gate

Before inspecting implementation for the purpose of editing, parse the user's arguments and compare them with the formal spec, repository instructions, ticket dependencies, and requested task order.

Test doubles/stubs/fakes are allowed only inside tests and only when they preserve the behavior under test. Never use a production stub, fake, placeholder, or simulated integration to satisfy a requirement.

**Ask a focused clarification question before any code edit, commit, or tracker mutation** only when there is a genuine contradiction or material ambiguity about scope, order, acceptance criteria, starting point, baseline, or implementation strategy. Never ask whether a production stub is acceptable: it is not. This is the only normal pause; when the request is coherent, continue autonomously through the complete queue. Examples:

- the requested starting issue conflicts with ticket dependencies;
- “continue” does not say whether partial work must be completed or skipped;
- the user asks for implementation and review-only work at the same time;
- the spec requires a real integration/validator but the argument appears to authorize a fake or deferred implementation;
- a closed ticket's acceptance criteria are not demonstrably satisfied.

Do not silently choose an interpretation when the conflict is material. State the conflicting facts and offer concise options. Do not ask for confirmation of ordinary engineering decisions that are already determined by the spec, ticket, repository conventions, or tests.

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