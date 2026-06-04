# docs/prd/

**English** | [简体中文](README.zh-CN.md)

This directory holds product requirement documents (PRDs) and business-logic source materials, referenced during the "supplementary reading" step (Step 3) described in `CLAUDE.md`.

The template ships **without** any concrete PRD files — only this readme. Create files here as your project requires:

- `prd-v1.md` — Phase 1 product requirements document (business background, user scenarios, feature list)
- `业务逻辑文档.md` — Project-specific business logic, data filtering rules, etc. (if applicable)
- `<integration-doc>.md` — Caller-provided original specification for inbound / callback protocols (if applicable)

> Note: the files referenced in `CLAUDE.md` Step 3 and Section 4 (document priority) are the files in this directory.
> Until those files are created, the references are "create on demand" — not missing.
> These materials serve as **inputs to our implementation** and carry lower priority than `PROJECT.md` / `SPEC.md` (see `CLAUDE.md` Section 4).
