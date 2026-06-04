# comment-service

**English** | [简体中文](PROJECT.zh-CN.md)

> This file is a **filled-in example** for `claude-workflow-template` (comment generation service), provided as a reference for writing style.

# One-line Goal

Build a standalone comment-generation receiver service: accept POST requests from the admin backend, query interaction data by post ID, call an LLM to generate one operational comment, and asynchronously callback the result to the caller.

# Role Definition

This service acts as a "comment generation receiver" and operates **exclusively as a receiver and processor**:

- Does not act as a caller (does not initiate outbound requests on its own)
- Does not publish comments (only generates text; publishing is handled by the caller)
- Does not write to the business database (business DB is read-only)
- Does not provide an admin management UI

# Target Callers

- Current sole caller: internal operations admin backend
- Future potential callers: other internal systems that need "data → LLM text" capability

# Current Pain Point

The operations backend wants to use an LLM to batch-generate comment drafts, but does not want to integrate the LLM directly in its own code (key management, retries, redaction, and rate limiting are all a burden). This service is extracted as an independent component to take on that responsibility.

# Phase 1 MVP Goals

1. Expose `POST /v1/comment-tasks` as the intake endpoint
2. Acknowledge the request immediately, then process asynchronously
3. Query interaction data (likes / comment count / recent trending keywords) by `post_id`
4. Call the LLM to generate one comment text
5. Assemble the result and POST it to `callback_url`
6. Persist task state throughout the entire lifecycle in a dedicated task database
7. On process restart, resume any unfinished tasks created within the past 24 hours

# Explicit Non-Goals

1. No caller role / no comment publishing
2. No multi-model routing, temperature controls, or other advanced toggles
3. No webhook signature verification (Phase 1 uses a static token)
4. No Sentry / Prometheus integration
5. No custom time-range parameters
6. No horizontal multi-instance scaling
7. No admin management console

# Success Criteria

- Given a valid request, the full "receive → query → LLM → callback" pipeline completes end-to-end
- Task state is traceable in the `comment_tasks` table (`RECEIVED` / `QUERIED` / `GENERATED` / `DONE` / `FAILED`)
- Duplicate requests with the same `task_id` are rejected with idempotency check (returns 409)
- After a process restart, unfinished tasks resume automatically

# Core Business Modes

## Mode 1: Query-only mode (`use_llm=false`)
Flow: receive → query interaction data → assemble stats result directly → callback

## Mode 2: Query + LLM mode (`use_llm=true`, default)
Flow: receive → query interaction data → feed data + prompt to LLM → assemble comment → callback

# Constraints

- **Technology**: Python 3.12 / FastAPI / asyncpg / Anthropic SDK, fully async
- **Data**: business DB is read-only; task DB has its own schema with full read-write access
- **Security**: LLM API key is loaded from environment variables; comments must not contain user PII (redacted before entering the prompt)
- **Performance**: ack latency P95 < 200 ms; full pipeline including LLM P95 < 8 s
- **Compatibility**: callback payload structure must strictly conform to the integration specification

# Scope Control Principles

- Phase 1 priority is to complete the minimal viable business loop — not feature completeness
- Do not introduce queues or signature mechanisms ahead of v2
- Any requirements beyond the Phase 1 scope are excluded from the current development cycle by default

# Risk Notes

- The actual business table schema may differ from the documentation; needs DDL inspection in Phase 2 to verify
- LLM output format is not guaranteed to be stable; prefill guidance and parse-failure retries are required
- Callback failure retries may cause the caller to process duplicates; SPEC caps retries at 3 attempts
