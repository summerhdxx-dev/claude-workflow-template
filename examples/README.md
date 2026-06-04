# examples/

**English** | [简体中文](README.zh-CN.md)

This directory contains **fully filled-in** reference examples so you can see at a glance what a completed template looks like.

## sample-comment-service — Comment Generation Service

A typical "receiver service" example that covers the complete scenario the template was designed for:

> Receive a POST request from an external admin backend → query business data → call an LLM to generate a comment → asynchronously callback the result to the caller.

It demonstrates how to fill out the blank templates in the root directory for a real project:

| Template file | What to look for in the example |
|---|---|
| `PROJECT.md` | How to write a concrete one-liner goal / role definition / explicit non-goals / success criteria |
| `SPEC.md` | How the task state machine (§4), LLM call rules (§6), and change classification (§11) map to real fields |
| `TASKS.md` | How to break phase 1–7 tasks along the "data → API → business logic → LLM → callback → E2E" axis |
| `ACCEPTANCE.md` | How to write acceptance criteria that can be answered pass/fail by a test, command, or manual check |

> Note: the example has been **intentionally condensed** for illustration purposes — it is not a complete production document. Its value is showing **writing style and level of detail**, not something to copy verbatim. Start your own project from the blank templates in the root directory and refer back here when you need a reference.
