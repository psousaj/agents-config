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

### Harness task tracking

The coordinating goal agent owns task-status updates, including delegated work. Use whichever task-progress tool is available in the current session: prefer the native experimental todo tool (e.g. `todowrite`, present when `experimental.todo` is enabled in recent V2 versions), otherwise a plugin task-list tool (e.g. `tasks`), otherwise a local ledger. Never hard-require a specific plugin and never claim progress tracking is unavailable when any option exists — switch silently and continue. Whatever the tool: exactly ONE current item `in_progress`, future items pending/todo, mark the current item completed/done only after acceptance criteria + validations + clean review + verified commit, reconcile on resume without duplicates, then activate the next task.

Keep base ref, findings, evidence, and commit in the task item text or local ledger. If no task tool is visible in a restricted runtime catalog (e.g. Code Mode `execute`), keep the local ledger, disclose once, and continue IMPLEMENT; never refuse or return planning-only for this reason.

When a continuation report includes concrete findings, immediately use them as the current task's implementation checklist. For signature preview flows, preserve preview identity (document/revision, normalized fingerprint/hash, and payload) through confirmation, compare with the persisted preview, distinguish preview mismatch from a stale-document conflict, and return the specified conflict response. This is implementation work, not a clarification request.

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
   - If findings exist, convert every finding into a remediation checklist and return immediately to `/implement` for the same task.
   - A non-clean review is a normal loop state, not a terminal status, clarification reason, or permission request.
   - Explicit task status/findings override `no task started`, `no GitHub issue`, and clean-worktree notes; those describe new-task/tracker state and do not permit skipping the open task.
   - GitHub tracking is optional. Do not create or mutate GitHub without explicit authorization.
   - Repeat `/implement` and `/code-review` until the review passes 100% clean with zero unresolved issues.
   - Use `BLOCKED` only when autonomous diagnosis confirms that the environment or requirements prevent implementation or verification.

4. **Commit and advance:**
   - After the review is explicitly clean, stage only the current task's reviewed changes and create a Git commit.
   - Verify the commit succeeded, record its hash, and confirm no current-task changes remain uncommitted.
   - If unrelated work was already present, isolate it in a named stash or patch and restore it only when its task starts; do not let it contaminate the next task's base.
   - A dirty worktree alone is not a clarification reason. Ask only when changes from different tasks are interleaved so tightly that they cannot be separated safely without guessing.
   - If a clean review already covers changes that also satisfy a later ticket, treat those changes as part of the current task's reviewed baseline and commit them now; do not reopen the review or ask based on thematic overlap.
   - Mark the task completed and proceed directly to the next task only after the commit and worktree checks pass.
   - Advance in the same run: announce `IMPLEMENT` for the next task immediately. Never end with queue items unstarted and never ask permission to continue ("say the word" style closings are forbidden). Stop only on exhausted queue, genuine contradiction, or diagnosed environment blocker.

---

### 3. Global Verification
When all tasks are finished:
- Run full test suite with race detectors/coverage (e.g. `go test -race ./...`).
- Run project linters and typechecks (`golangci-lint`, `tsc`, etc.).
- Run a final consolidated `/code-review` across all changed files against the base branch.
- Output a summary of all executed tasks and verification evidence.