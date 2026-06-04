# Current Phase Task List — comment-service (filled-in example)

**English** | [简体中文](TASKS.zh-CN.md)

> This file is a filled-in example for `claude-workflow-template`. The status markers intentionally
> **mix** `[x]` / `[~]` / `[ ]` to show what a project looks like halfway through.

## Current Progress

> **Current task**: Phase 3 — implement intake route (auth + field validation + idempotency + write RECEIVED + ack)
> **Last updated**: 2026-05-20

---

## Phase 1: Project Initialization and Development Foundations

- [x] Set up dependency management (uv)
- [x] Configure lint + type checking (ruff + mypy --strict)
- [x] Configure test framework (pytest, one happy-path test passing)
- [x] Create `.env.example` + local `.env` (not committed to git)
- [x] Implement settings loading (with field validation)
- [x] Implement structured logging
- [x] Implement `GET /health` (no external dependencies)
- [x] Containerize (Dockerfile)
- [x] Complete README

## Phase 2: Core Data Structures

- [x] Design task DB schema (`comment_tasks` + `comment_task_logs`)
- [x] Write migration scripts
- [x] Implement task DB connection pool
- [x] Implement business DB read-only connection pool
- [x] Wire DB ping into `GET /health`
- [x] Implement state-machine-backed repository layer
- [x] Inspect actual business DB table structure → record in docs/decisions.md (DECISION-001)

## Phase 3: Core API and State Machine Skeleton

- [x] Implement request schema (field constraints + control character stripping)
- [x] Implement callback payload schema
- [x] Implement auth dependency (static token)
- [x] Implement state enum + legal transition table + `transition()` validation function
- [~] Implement intake route: auth + field validation + idempotency check + write `RECEIVED` + immediate ack
- [ ] Implement worker skeleton (RECEIVED → QUERIED → placeholder failure)
- [ ] Implement startup recovery (scan unfinished tasks within past 24 h)
- [ ] Unit tests: state machine legal/illegal transitions, idempotency, field validation

## Phase 4: Business Logic Modules

- [ ] Implement interaction data query (read-only SQL, with redaction)
- [ ] Wire real query into worker, advance to `QUERIED`
- [ ] Query-only mode: assemble stats result directly to `GENERATED`

## Phase 5: LLM Call Module

- [ ] Implement prompt template (system + user rendering)
- [ ] Implement LLM SDK wrapper + ephemeral cache + prefill
- [ ] Implement single-call timeout + HTTP 5xx retry
- [ ] Implement input redaction validation
- [ ] Implement output parsing + parse-failure retry
- [ ] Unit tests + prompt injection security tests
- [ ] Evals: at least 1 case (comment generation happy path)

## Phase 6: Callback Delivery Module

- [ ] Implement callback client (async POST + timeout + 3-attempt exponential back-off retry)
- [ ] Implement success / failure payload assembly
- [ ] Implement error_msg category mapper
- [ ] Unit tests + integration tests

## Phase 7: End-to-End Integration and Evals

- [ ] End-to-end cases 11.1 ~ 11.5 (see ACCEPTANCE.md)
- [ ] Performance test (ack latency / full pipeline latency)
