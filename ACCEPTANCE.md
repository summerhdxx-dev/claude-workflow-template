# Acceptance Criteria

**English** | [简体中文](ACCEPTANCE.zh-CN.md)

This file specifies the verifiable acceptance conditions for the project's phase 1. Every item must be answerable as "pass / fail" using one of: automated test / CLI command / manual verification.

## 1. Acceptance Scope

> List the acceptance dimensions covered by this file
> (interface / state machine / business logic / security / performance / documentation / deployment / end-to-end).
>
> Example: This file covers acceptance for the following 11 dimensions, each aligned with the
> corresponding section of SPEC.md …

<!-- DELETE the example above and fill in this project's content -->

## 2. Interface Acceptance (if applicable)

### 2.1 Authentication

> List expected behavior for three cases: missing auth header / incorrect auth header / correct auth header.

### 2.2 Field Validation

> List invalid values and expected error codes for each field in SPEC.md §3.2.
>
> | Field | Invalid value | Expected |
> |---|---|---|
> | `<X>` | empty | HTTP 400, error_msg="field X is required" |

<!-- DELETE the example above and fill in this project's content -->

### 2.3 Idempotency

> Handling of repeated requests with the same ID.

## 3. State Machine Acceptance

> List the acceptance method for each valid transition (aligned with SPEC.md §4.2).
>
> | Acceptance Item | Verification Method | Pass Condition |
> |---|---|---|
> | `<INITIAL>` → `<STAGE_1>` | Unit test + DB row exists | Status field updated and log table written |
> | Terminal state irreversible | Unit test simulating illegal transition | Raises `IllegalTransitionError` |
>
> - [ ] All valid state machine transitions are covered by unit tests
> - [ ] Terminal state irreversibility is enforced by automated checks
> - [ ] State log table and master table fields are consistent

<!-- DELETE the example above and fill in this project's content -->

## 4. Business Logic Acceptance

> List acceptance test cases for each business rule.

<!-- DELETE the example above and fill in this project's content -->

## 5. LLM Call Acceptance (if applicable)

> - [ ] Prompt caching hit rate > 0
> - [ ] Input redaction validation rejects violating fields
> - [ ] Prompt injection test cases still produce valid output
> - [ ] Parse failure after 1 retry → task marked FAILED
> - [ ] Call log is complete (model / tokens / latency) + does not contain full prompt text

<!-- DELETE the example above and fill in this project's content -->

## 6. Outbound Push / Output Acceptance (if applicable)

> Success payload shape / failure payload shape / retry strategy / task row retained after sustained unreachability.

<!-- DELETE the example above and fill in this project's content -->

## 7. Data Security Acceptance

> - [ ] Credentials not committed to git (grep full history → 0 hits)
> - [ ] Credentials not written to logs (grep log output → 0 hits)
> - [ ] Sensitive fields not passed to third-party calls
> - [ ] Data store permissions comply with §9 project-specific rules

<!-- DELETE the example above and fill in this project's content -->

## 8. Performance Acceptance

> - [ ] Ack latency P95 < `<X>`s
> - [ ] Full-chain P95 < `<Y>`s (SQL only) / `<Z>`s (including LLM)
> - [ ] Startup recovery scan < `<W>`s (N tasks)

<!-- DELETE the example above and fill in this project's content -->

## 9. Documentation Acceptance

> - [ ] PROJECT.md / SPEC.md / TASKS.md / ACCEPTANCE.md all fully populated
> - [ ] `docs/architecture.md` / `api-conventions.md` / `runbook.md` consistent with code
> - [ ] `docs/decisions.md` contains all L3 change decisions from this phase
> - [ ] `CHANGELOG.md` contains delivery summary for this phase

## 10. Deployment Acceptance

> - [ ] Dockerfile build passes
> - [ ] `GET /health` returns ok
> - [ ] Startup recovery takes effect after container restart

## 11. End-to-End Test Cases

> Number as 11.1 / 11.2 / … and list all end-to-end test cases.
>
> Example:
> - 11.1: Full success path, assert `<TERMINAL_OK>`
> - 11.2: External data source unreachable → `<TERMINAL_FAIL>`
> - 11.3: LLM unreachable → `<TERMINAL_FAIL>` (if applicable)
> - 11.4: Duplicate ID request → first request 200, subsequent requests 409
> - 11.5: Process restart recovery

<!-- DELETE the example above and fill in this project's content -->
