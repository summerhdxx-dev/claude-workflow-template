# Project Name

**English** | [简体中文](PROJECT.zh-CN.md)

<REPLACE with the project's official name (repository name / full public title)>

This file defines the project goal, phase-1 scope, explicit non-goals, constraints, and success criteria.
Detailed product requirements: `docs/prd/<PRD file>` (if applicable)
Detailed functional rules, state transitions, and field constraints: `SPEC.md`
Development task breakdown for the current phase: `TASKS.md`
Acceptance criteria: `ACCEPTANCE.md`
AI development execution rules: `CLAUDE.md`

# One-Line Goal

> State in one sentence what problem this project solves, for whom, and what it produces.
>
> Example: Build a standalone receiver service for the X side that accepts POST requests from external
> system Y, queries Z data on demand, calls W to generate results, and asynchronously POSTs the result
> back to the caller via callback.

<!-- DELETE the example above and fill in this project's content -->

# Role Definition

> What role does the project play in the broader system — **what it does and what it does not do**.
>
> Example: This service acts as the "X side" defined in the integration spec, functioning **solely as
> the receiver and processor**:
> - Does not act as a caller
> - Does not handle image generation
> - Does not send DingTalk notifications
> - Does not write to business data stores

<!-- DELETE the example above and fill in this project's content -->

# Target Callers

> List current and potential callers.
>
> Example:
> - Current sole caller: external admin portal X
> - Future possibility: other internal systems using the same protocol

<!-- DELETE the example above and fill in this project's content -->

# Current Pain Points

> Why does the caller need this service (what breaks without it)?
>
> Example: The business system wants to enhance X output with an LLM but does not want to integrate
> the LLM directly into its own codebase …

<!-- DELETE the example above and fill in this project's content -->

# Phase-1 MVP Goals

> List only what will be built in this phase (numbered). Keep to 8 items or fewer.
>
> Example:
> 1. Expose `<external interface path>` as the receiver endpoint
> 2. Acknowledge the request immediately; process asynchronously
> 3. Query Y by X; aggregate Z (baseline metrics)
> 4. (if applicable) Call the LLM to generate N
> 5. Assemble result and POST to callback_url
> 6. Persist task state end-to-end in a dedicated task store
> 7. Resume incomplete tasks after process restart

<!-- DELETE the example above and fill in this project's content -->

# Explicit Non-Goals

> Things that will absolutely not be built in phase 1 (numbered). Use this to block scope creep.
>
> Example:
> 1. No caller-side role
> 2. No X / Y / Z advanced feature switches
> 3. No webhook signature verification
> 4. No Sentry / Prometheus / log aggregation
> 5. No custom time-range parameters
> 6. No horizontal multi-instance scaling
> 7. No management console

<!-- DELETE the example above and fill in this project's content -->

# Success Criteria

> Verifiable conditions that must be met when phase 1 is complete (aligned with ACCEPTANCE.md).
>
> Example:
> - Given a valid request, the full chain "receive → query → process → callback" completes
> - Task state is traceable in `<task master table>` (`<INITIAL>` / `<STAGE_N>` / `<TERMINAL_OK>` / `<TERMINAL_FAIL>`)
> - Duplicate requests with the same ID are rejected (idempotency check)
> - Incomplete tasks resume after process restart

<!-- DELETE the example above and fill in this project's content -->

# Core Business Modes

> List the N primary operating modes of this project (e.g., query-only mode / AI-enhanced mode).
>
> Example:
> ## Mode 1: X-only mode
> Flow: receive → X → assemble directly → callback
>
> ## Mode 2: X + AI mode
> Flow: receive → X → feed data + prompt to LLM → assemble → callback

<!-- DELETE the example above and fill in this project's content -->

# Constraints

> One sentence per category: technical / data / security / performance / compatibility.
>
> Example:
> - **Technical**: <language / framework / package manager / async model>
> - **Data**: <read-only / read-write / isolation requirements>
> - **Security**: <credential management / redaction requirements>
> - **Performance**: <latency / throughput targets>
> - **Compatibility**: <protocol must strictly conform to X>

<!-- DELETE the example above and fill in this project's content -->

# Scope Control Principles

> Softer boundaries than "Explicit Non-Goals" — decision-making principles.
>
> Example:
> - Phase 1 prioritizes closing the minimal business loop; feature completeness is not the goal
> - Do not introduce complex scheduling, queuing, or signing mechanisms for v2
> - Do not pre-abstract for "things we might need later"
> - Any requirement beyond phase-1 scope is excluded from the current development cycle by default

<!-- DELETE the example above and fill in this project's content -->

# Known Risks

> Known risks that may affect the MVP (missing data, type mismatches, third-party rate limits, etc.).
>
> Example:
> - The actual business table schema may differ from documentation; verify via DDL inspection in phase 2
> - LLM JSON output format is not guaranteed to be stable; use prefill guidance and retry on parse failure
> - Callback retry on failure may cause duplicate processing on the caller side; specify retry count in SPEC

<!-- DELETE the example above and fill in this project's content -->
