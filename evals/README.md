# evals/

**English** | [简体中文](README.zh-CN.md)

> **Enable this directory only when the project involves LLM / Agent calls. Otherwise the entire directory may be deleted.**

This directory holds evaluation cases that verify "output matches expectation" for LLM calls, complementing unit and integration tests:
- Unit tests → correctness of code logic
- Evals → whether the LLM produces stable, business-aligned output for a fixed input

## Case Convention

Every eval case must include:
1. **Input**: fixed prompt parameters (sanitized)
2. **Expected output**: JSON schema / keywords / length range / quantity constraints
3. **Assertion method**: pytest assert / string matching / LLM-as-judge

## Required Coverage Scenarios

Check off those applicable to your project:
- [ ] Main happy path (input → output conforms to schema)
- [ ] Prompt injection protection (crafted out-of-bounds input still yields valid JSON)
- [ ] Output format error handling (retry on parse failure / truncation)
- [ ] Edge-case data (empty input / oversized input / missing fields)

## How to Run

> Defined per project (`pytest evals/` / standalone runner / CI integration)

<!-- DELETE the example below and fill in your project content -->

> Example directory naming:
> - `evals/<feature-scenario>/` e.g. `comment_generation/` / `intent_classification/`
> - One `test_<specific_case>.py` file per scenario
> - Each case contains: inputs, expected outputs, and assertion functions
