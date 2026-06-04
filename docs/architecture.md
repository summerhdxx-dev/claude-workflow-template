# Architecture

**English** | [简体中文](architecture.zh-CN.md)

This document describes the engineering implementation approach, code-organization boundaries, state-machine placement rules, dependency structure, and test strategy for the Phase 1 MVP.

If this document conflicts with `PROJECT.md` / `SPEC.md`, the latter takes precedence.

## 1. Architecture Goals

> List 4–6 goals aligned with the "Phase 1 MVP Objectives" in PROJECT.md, down to the implementation level.
>
> Example:
> 1. Support an end-to-end MVP loop for `<external API path>`
> 2. Enforce strict state transitions with full audit trails
> 3. Support read-only queries against the external data store plus read/write access to the task store
> 4. Support (if applicable) async LLM calls with input sanitization and injection protection
> 5. Keep the codebase structure clean and prevent business logic from spreading out of control

<!-- DELETE the example above and fill in your project content -->

## 2. Module Boundaries (aligned with SPEC.md §1.3)

> Draw a `src/` directory tree in a code block; add a one-line comment per module explaining its responsibility.
>
> Example:
> ```
> src/<package>/
> ├── main.py             # Application entry point + lifespan
> ├── settings.py         # Configuration loading
> ├── api/                # External-facing API layer
> ├── tasks/              # Task state machine + worker
> ├── data/               # Persistence layer
> ├── <ai/>               # (if applicable) LLM calls
> ├── callback/           # Outbound push / callbacks
> └── observability/      # Logging
> ```

<!-- DELETE the example above and fill in your project content -->

## 3. Data Flow (Core N Steps)

> Use an ASCII flow diagram to show key steps from incoming request to final callback.
>
> Example:
> ```
> Inbound request → Auth + field validation + idempotency check → write <INITIAL> → immediate ack
>      → async worker → business query → advance state
>      → (if applicable) LLM call → advance state
>      → outbound push → advance state to <TERMINAL_OK>
> ```

<!-- DELETE the example above and fill in your project content -->

## 4. State Machine Placement

> See SPEC.md §4 for the full definition. This section highlights **implementation hard rules**:
> - Single entry point: all state changes must go through `<state-machine module>::transition()`
> - Business modules must not directly UPDATE the status column
> - Terminal states are irreversible

## 5. Database Schema (if applicable)

### 5.1 Task Store

> List the field outline for the primary task table and the state-log table.

### 5.2 External Data Store (read-only)

> List the dependent business tables and any field discrepancies (reference probe/inspection conclusions in docs/decisions.md if available).

<!-- DELETE the example above and fill in your project content -->

## 6. Dependency Graph

> Use an ASCII diagram to describe inter-module dependency direction (no circular dependencies).
>
> Example:
> ```
> main.py → lifespan → recovery → repository
>       → app → routes → BackgroundTasks → worker
>                                        → state / repository / data / <ai> / callback
> ```

<!-- DELETE the example above and fill in your project content -->

## 7. Test Strategy

> | Type | Path | Trigger |
> |---|---|---|
> | Unit | `tests/unit/` | default `pytest` run |
> | Integration | `tests/integration/` | marked `-m integration` |
> | E2E | `tests/e2e/` | marked `-m e2e` |
> | Evals | `evals/<scenario>/` | standalone runner |

<!-- DELETE the example above and fill in your project content -->

## 8. Deployment Topology

> Detailed release steps are in docs/runbook.md.
>
> Example:
> - Single-instance `<language runtime>` process (MVP)
> - Docker image: multi-stage build from `<base image>`
> - Environment variables injected from `.env` (local) / K8s Secret (production)
> - External data store connection: internal network
> - LLM calls (if applicable): over the public internet to `<provider>`

<!-- DELETE the example above and fill in your project content -->
