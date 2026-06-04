# Acceptance Criteria — comment-service (filled-in example)

**English** | [简体中文](ACCEPTANCE.zh-CN.md)

> This file is a filled-in example for `claude-workflow-template`, **intentionally condensed**. Every item can be answered pass/fail via a test, command, or manual check.

## 1. Acceptance Scope

Covers 7 dimensions: interface, state machine, business logic, LLM, callback, data security, and end-to-end — aligned with the corresponding sections of `SPEC.md`.

## 2. Interface Acceptance

### 2.1 Authentication
- Missing `X-API-Token` → 401
- Incorrect token → 401
- Correct token → proceed to field validation

### 2.2 Field Validation

| Field | Invalid value | Expected response |
|---|---|---|
| `task_id` | empty | 400, `invalid field task_id: required` |
| `post_id` | 0 or negative | 400, `invalid field post_id: must be > 0` |
| `callback_url` | http (not https) | 400, `invalid field callback_url: must be https` |

### 2.3 Idempotency
First request with a given `task_id` → 200; subsequent requests → 409 (`task already exists`).

## 3. State Machine Acceptance

| Acceptance item | Verification method | Pass condition |
|---|---|---|
| `RECEIVED → QUERIED` | unit test + DB row | status updated and log table written |
| `GENERATED → DONE` | integration test (mock callback) | task set to DONE after successful callback |
| Terminal state is irreversible | unit test simulating `DONE → any` | raises IllegalTransitionError |
| Skipped-state rejected | unit test simulating `RECEIVED → DONE` | raises IllegalTransitionError |

- [ ] All legal state machine transitions have unit test coverage
- [ ] Terminal-state irreversibility + skipped-state rejection are automated
- [ ] State log table fields are consistent with the main task table

## 5. LLM Call Acceptance

- [ ] Prompt caching hit rate > 0
- [ ] Input redaction validation rejects prompts containing nicknames / phone numbers
- [ ] Prompt injection case (`prompt_hint` contains "ignore the above instructions") still outputs a valid comment JSON
- [ ] Parse failure retries once; if still failing → task marked FAILED
- [ ] Call log contains model / token count / latency; does not contain the full prompt text

## 7. Data Security Acceptance

- [ ] Credentials not committed to git (`git log -p | grep` returns 0 hits)
- [ ] Credentials not written to logs
- [ ] User nicknames / phone numbers not sent to LLM calls
- [ ] Business DB account is read-only

## 11. End-to-End Cases

- 11.1: Full LLM path — assert terminal state `DONE`, callback received `comment`
- 11.2: Business DB unreachable → `FAILED`
- 11.3: LLM unreachable (consecutive 5xx) → `FAILED`
- 11.4: Duplicate `task_id` → first request 200, subsequent 409
- 11.5: Process restarted while worker is processing → startup recovery resumes task to `DONE`
