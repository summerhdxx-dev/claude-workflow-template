# Current Phase Task List

**English** | [简体中文](TASKS.zh-CN.md)

This file takes `PROJECT.md` as its scope constraint and `SPEC.md` as its rule constraint; acceptance criteria are governed by `ACCEPTANCE.md`.

Conflict resolution: `PROJECT.md` → `SPEC.md` → `ACCEPTANCE.md` in priority order; overrides are not permitted without justification.

Execution rules (from `CLAUDE.md`):
- Process only one explicit `[ ]` task at a time; do not open multiple incomplete tasks simultaneously
- After each task completes, update this file's status (`[~]` → `[x]`)
- Maintain the mandatory order: **data layer first → backend API next → frontend integration / E2E last**
- All state changes must go through the `<state machine module>` wrapper; direct UPDATEs are forbidden
- Each completed `[ ]` task = one git commit + push

Status labels:
- `[ ]` Not started
- `[~]` In progress (only 1 `[~]` allowed at any given time)
- `[x]` Completed

---

## Current Progress

> **Current task**: Phase 1 — Task 1 (project initialization)
> **Last updated**: YYYY-MM-DD (project just started)

The "current task" pointer line above must be updated every time a task is completed.

---

## Phase 1: Project Initialization and Development Foundation

**Goal**: Give the repository the foundational capabilities needed to run the project (dependency management, lint, tests, containerization, minimal application).

> REPLACE with this project's phase-1 task list using the actual technology stack.
>
> Example:
> - [ ] Configure dependency management (uv / poetry / npm, etc.)
> - [ ] Configure lint + type checking
> - [ ] Configure test framework (at minimum one happy-path test passing)
> - [ ] Create `.env.example` + local `.env` (**do not commit to git**)
> - [ ] Implement settings loading (with field validation)
> - [ ] Implement structured logging
> - [ ] Implement `GET /health` (no external dependencies)
> - [ ] Containerize (Dockerfile / docker-compose)
> - [ ] Complete README

<!-- REPLACE with this project's phase-1 task list -->

---

## Phase 2: Core Data Structures

**Goal**: Make task persistence available; determine the actual structure of external data sources.

> Example:
> - [ ] Design task store schema
> - [ ] Write migration scripts
> - [ ] Implement persistent connection pool
> - [ ] Implement external data source connection pool
> - [ ] DB ping integrated into `GET /health`
> - [ ] Implement state-machine-wrapped repository layer
> - [ ] Inspect actual external data source table structure → record in `docs/decisions.md`

<!-- REPLACE with this project's phase-2 task list -->

---

## Phase 3: Core API and State Machine Skeleton

**Goal**: End-to-end inbound interface reaching `<INITIAL>` state; state machine wrapper in place; startup recovery in place.

> Example:
> - [ ] Implement request schema (with field constraints + control character filtering)
> - [ ] Implement callback payload schema
> - [ ] Implement auth dependency
> - [ ] Implement state enumeration + valid transition table + `transition()` validation function
> - [ ] Implement receiver route: auth + field validation + idempotency check + write `<INITIAL>` + immediate ack
> - [ ] Implement worker skeleton (PENDING → PROCESSING → placeholder failure)
> - [ ] Implement startup recovery (scan incomplete tasks within 24 h)
> - [ ] Unit tests: state machine valid/invalid transitions, idempotency, field validation

<!-- REPLACE with this project's phase-3 task list -->

---

## Phase 4: Business Logic Module

**Goal**: Replace worker placeholders with real business queries; complete the core business path.

> Expand according to the project's business logic.

<!-- REPLACE with this project's phase-4 task list -->

---

## Phase 5: LLM Call Module (if applicable)

**Goal**: Connect LLM calls with redaction, injection defense, parsing, and retry. Delete this phase if the project does not call an LLM.

> Example:
> - [ ] Implement prompt template (system + user 5-section rendering)
> - [ ] Implement LLM SDK wrapper + ephemeral cache + prefill
> - [ ] Implement per-call timeout + HTTP 5xx retry
> - [ ] Implement input redaction validation
> - [ ] Implement output parsing + parse-failure retry
> - [ ] Unit tests: prompt rendering, redaction, parsing, retry
> - [ ] Prompt injection security tests
> - [ ] Integration test: mock LLM full-path run
> - [ ] Evals: at least 1 test case

<!-- REPLACE with this project's phase-5 task list -->

---

## Phase 6: Outbound Push / Output Module (if applicable)

**Goal**: Connect the outbound push; complete error_msg categorization.

> Example:
> - [ ] Implement push client (async POST + timeout + retry)
> - [ ] Implement success / failure payload assembly
> - [ ] Implement error_msg category mapper
> - [ ] Unit tests + integration tests

<!-- REPLACE with this project's phase-6 task list -->

---

## Phase 7: End-to-End Integration and Evals

**Goal**: Implement and pass all end-to-end test cases in ACCEPTANCE.md; meet performance targets.

> Example:
> - [ ] End-to-end test case N.M
> - [ ] Performance load test

<!-- REPLACE with this project's phase-7 task list -->

---

## Phase 8: Observability, Documentation, and Deployment

**Goal**: Production-ready; documentation consistent with code; security audit passed.

> Example:
> - [ ] Full log redaction audit
> - [ ] Full git history credential scan
> - [ ] Complete `docs/architecture.md`
> - [ ] Complete `docs/api-conventions.md`
> - [ ] Complete `docs/runbook.md` go-live checklist
> - [ ] `CHANGELOG.md` v1.0 release notes
> - [ ] ACCEPTANCE full item verification

<!-- REPLACE with this project's phase-8 task list -->

---

## Backlog (v2, outside MVP scope)

> Placeholder only — **do not expand into implementation**. These tasks must not be started until all MVP tasks are `[x]`.

<!-- List v2 todos here; do not act on them -->

---

## Phase Delivery Checklist (run through after each phase completes)

After all `[ ]` tasks in a phase are marked `[x]`:

1. All ACCEPTANCE items related to this phase are checked `[x]`
2. CHANGELOG includes a delivery summary for this phase
3. Technical decisions made during this phase (including inspections and integration confirmations) are written to `docs/decisions.md`
4. Unit tests + integration tests + evals (if applicable) all pass
5. One `git push` to sync to the remote
