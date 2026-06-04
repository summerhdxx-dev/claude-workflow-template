# Project Specification

**English** | [简体中文](SPEC.zh-CN.md)

This file takes `PROJECT.md` as its scope constraint and provides **detailed rules, protocol fields, task state machine, error handling, and change tiers** at an actionable level of definition.

Conflict resolution: `PROJECT.md` overrides `SPEC.md`; `SPEC.md` overrides `docs/architecture.md`.

## 1. Overview

### 1.1 Document Scope

> Describe what this SPEC covers and what it does not, with references to the corresponding PROJECT sections.
>
> Example: This file covers the inbound protocol, task state machine, business logic main flow,
> outbound callback protocol, error handling, and change tiers. It does NOT cover: implementation-layer
> directory structure (see `docs/architecture.md`), external API documentation (see `docs/api-conventions.md`).

<!-- DELETE the example above and fill in this project's content -->

### 1.2 Phase-1 Goals

> Align with the Phase-1 MVP Goals in PROJECT.md and expand each by one level into verifiable conditions.
>
> Example: Complete the full X → Y → Z chain; persist task state end-to-end; resume incomplete tasks
> within 24 h after process restart.

<!-- DELETE the example above and fill in this project's content -->

### 1.3 Module Boundaries

> List each code-level module name and its one-line responsibility (aligned with `docs/architecture.md §2`).
>
> Example:
> ```
> src/<package>/
> ├── api/             # External interface (routing, auth, field validation)
> ├── tasks/           # Task state machine + worker
> ├── data/            # Data queries (read-only external data store + task store)
> ├── <ai/>            # (if applicable) LLM calls
> ├── callback/        # Outbound push
> └── observability/   # Logging
> ```

<!-- DELETE the example above and fill in this project's content -->

## 2. Scope and Feature Switches

> List the protocol-level representation of "Explicit Non-Goals" from PROJECT.md: which fields are
> kept for compatibility, and which switches accept input parameters without implementing actual logic.
>
> Example: `content_config` accepts 6 switches; only X and Y are implemented; the remaining 4 are
> listed as `unsupported` fields in the callback.

<!-- DELETE the example above and fill in this project's content -->

## 3. Inbound Interface Protocol (if applicable)

### 3.1 Protocol Overview

> HTTP / WebSocket / gRPC / message queue; delete this section if not applicable.

### 3.2 Field Constraints

> List type, required status, length limit, character set restrictions, and control character filtering
> for each request field.
>
> Example:
> | Field | Type | Required | Constraints |
> |---|---|---|---|
> | `config_id` | int | yes | > 0, unique idempotency key |
> | `callback_url` | str | yes | length ≤ 2048, must be https |
> | `prompt_text` | str | no | length ≤ 1000, control characters filtered |

<!-- DELETE the example above and fill in this project's content -->

## 4. Task State Machine

### 4.1 State Enumeration

> Define all valid states. **State names are defined by the individual project.** The entries below
> are placeholder examples.
>
> Example:
> - `<INITIAL>`: Just received; processing has not started
> - `<STAGE_1>`: Processing in progress
> - `<STAGE_2>`: Stage 2 complete (optional)
> - `<TERMINAL_OK>`: Success terminal state (irreversible)
> - `<TERMINAL_FAIL>`: Failure terminal state (may be manually reset to `<INITIAL>`)

<!-- DELETE the example above and fill in this project's content -->

### 4.2 Valid Transition Table

> Table columns: from → to / trigger action / trigger module / failure handling / log fields.
>
> Example:
> | From | To | Trigger Module | Trigger Condition | Log Fields |
> |---|---|---|---|---|
> | `<INITIAL>` | `<STAGE_1>` | worker | Async start after receipt | `from_status, to_status, triggered_at, triggered_by` |
> | `<STAGE_1>` | `<TERMINAL_OK>` | callback | Push succeeded | same as above |

<!-- DELETE the example above and fill in this project's content -->

### 4.3 Hard Rules

> List prohibited behaviors (terminal states irreversible / skipping states / direct UPDATE, etc.).

## 5. Business Logic Main Flow

> Describe each step in "Step N → Step N+1" sequential form: input, query, filter, aggregation, output.
> Include SQL templates (redacted) where applicable.
>
> Example:
> 1. Personnel lookup: <query step>
> 2. Data query: <query step>
> 3. Aggregation: <aggregation rules>
> 4. Output: <output format>

<!-- DELETE the example above and fill in this project's content -->

## 6. LLM Calls (if applicable, see CLAUDE.md §24)

### 6.1 Trigger Conditions

> At which stage the LLM is called and which switch controls it.

### 6.2 Prompt Structure

> System prompt template (which fields are cached / which are not) + user message rendering rules.

### 6.3 Input Redaction and Injection Defense

> List of fields that must be removed from the prompt + injection defense statements.

### 6.4 Output Parsing

> Expected format (JSON schema) + parse-failure retry strategy.

### 6.5 Token and Timeout Budget

> max_tokens / per-call timeout / total timeout / retry count and backoff.

> Full rules: CLAUDE.md §24. Delete this entire section if the project does not call an LLM.

<!-- DELETE the example above and fill in this project's content -->

## 7. Callback / Output Protocol (if applicable)

> Success payload / failure payload / retry strategy / idempotency expectations.
>
> Example:
> ```json
> {
>   "config_id": 123,
>   "status": "success" | "fail",
>   "result": {...},
>   "meta": {...},
>   "error_msg": "..."  // fail only
> }
> ```

<!-- DELETE the example above and fill in this project's content -->

## 8. Error Codes and error_msg Categories

> List all error categories with user-visible error_msg templates.
>
> Example:
> | Category | error_msg Template | HTTP Status |
> |---|---|---|
> | Auth failure | `authentication failed` | 401 |
> | Field validation failure | `field X is invalid: <reason>` | 400 |
> | Task expired | `stale task expired` | — |
> | Internal error | `internal error` | 500 |

<!-- DELETE the example above and fill in this project's content -->

## 9. Authentication and Security

> Authentication method (token / signature / mTLS) + credential storage + log redaction requirements.

## 10. Technology Stack

> Whitelist of frameworks the project is permitted to introduce (paired with CLAUDE.md §12).
>
> Example: Python 3.12 / <web framework> / <ORM> / <LLM SDK>. **Any framework outside this whitelist
> is an L3 change.**

<!-- DELETE the example above and fill in this project's content -->

## 11. Change Tiers (L1 / L2 / L3)

### L1: Local Safe Change

> All of the following must be true for direct implementation:
> - Change is confined to a single module
> - Does not modify task state enumeration or transitions
> - Does not modify the external protocol
> - Does not modify the business query main path
> - Does not modify LLM prompt structure (if applicable)

### L2: Controlled Change

> Any one of the following requires outputting an impact-scope description before implementation:
> - Involves multiple modules
> - Involves task store schema fields
> - Involves external field constraints
> - Involves LLM prompt structure modification

### L3: High-Risk Change

> Any one of the following requires **recording to `docs/decisions.md` first**; must not be
> implemented before confirmed:
> - Modifying task state enumeration or valid transition table
> - Modifying primary key / unique index / partitioning strategy
> - Modifying the main structure of the external protocol
> - Replacing a core framework (DB client / async framework / LLM provider)
> - Changing data store read/write permissions

## 12. Compatibility and Version Evolution

> Protocol version field / field deprecation process / client upgrade path.

## 13. Pending Integration / Unconfirmed Items

> List items that are documented but have not yet been verified through actual testing.
> Include verification method and owner.
>
> Example:
> - A: Actual field types in external data store X table — verification: DDL inspection — status: pending
> - B: Meaning of field N in third-party Y interface — verification: integration test — status: pending

<!-- DELETE the example above and fill in this project's content -->
