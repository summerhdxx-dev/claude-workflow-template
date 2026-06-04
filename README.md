# claude-workflow-template

**English** | [简体中文](README.zh-CN.md)

> A stack-agnostic, documentation-first workflow template for AI collaboration — it turns the AI from "improvises and writes a pile of code" into a constrained engineering teammate that ships maintainable MVPs reliably.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
![Stack agnostic](https://img.shields.io/badge/stack-agnostic-blue.svg)

Distilled from the engineering practice of a real production project. Works best paired with AI coding tools like Claude Code, and is equally usable when followed by humans alone.

---

## When to use / not use

**Good fit:**
- Projects where scope creep is a real risk and you want an explicit "out of scope" line to hold it back
- You write code with AI but can't stand it "improvising, refactoring on a whim, skipping tests"
- Backend services with strict state transitions / external protocols / data-security requirements
- Teams that want collaboration conventions and technical decisions to be traceable

**Poor fit:**
- One-off scripts / demos of a few dozen lines (process overhead outweighs the benefit)
- Early-stage prototypes whose requirements are overturned daily (documentation-first slows you down)

---

## What it is

The template provides:
- `CLAUDE.md` — AI collaboration rules (25 sections; §9 / §24 left as placeholders)
- `PROJECT.md` / `SPEC.md` / `TASKS.md` / `ACCEPTANCE.md` — the four-document skeleton
- `docs/` — architecture / API / decisions / tools / runbook / bug templates
- `evals/` — LLM evaluation placeholder (delete if you don't call an LLM)
- `CHANGELOG.md` / `.gitignore` — generic helper files

The template does **not** provide: source-code scaffolding, dependency management, Dockerfile, or CI config — those are decided by your specific stack.

> Bilingual note: every core document ships in two versions, `*.md` (English) and `*.zh-CN.md` (Chinese).
> When you use the template, **keep the language your team works in and delete the other**.

---

## How to use (5-minute start)

### 1. Clone the template into a new project directory

```bash
git clone --depth=1 https://github.com/summerhdxx-dev/claude-workflow-template.git my-new-project
cd my-new-project
rm -rf .git
git init
```

### 2. Grep for placeholders

Every spot that needs filling can be located in one pass:

```bash
grep -rni "DELETE the example above\|REPLACE with your project\|删除以上示例后填写\|替换为本项目" .
```

### 3. Fill the four documents in order (**this is key — don't skip or reorder**)

1. Write `PROJECT.md` first: goal, role, scope, out-of-scope, risks (~20 min)
2. Then break down `TASKS.md` phase 1: project bootstrap tasks (~10 min)
3. Then write `SPEC.md` §1–§3 (overview, scope, core interface/protocol) (~30 min)
4. Then write `ACCEPTANCE.md` §1 (acceptance scope) + §2 (core interface acceptance) (~10 min)
5. First commit: `docs: land initial project documentation`

### 4. Tailor CLAUDE.md as needed

- **Required**: §9 project-specific rules (data-store read/write permissions, sensitive fields, project red lines)
- **If you call an LLM**: §24 LLM invocation rules; otherwise **delete the whole section**
- **§11 task state machine**: replace `<INITIAL> / <STAGE_1> / ... / <TERMINAL_OK>` placeholders with your project's real state names
- **§12 tech-stack red lines**: list the frameworks your project is allowed to introduce
- **§25 doc-sync matrix**: complete the table with your project's actual section numbers

### 5. Run the CLAUDE.md §2 core execution flow

Hand the first `[ ]` task of `TASKS.md` phase 1 to the AI (or yourself), and drive it through steps 1–7 of `CLAUDE.md §2`.

---

## Design philosophy

- **Documentation first**: nail down "what to do / what not to do / what 'done' means" before touching code
- **Stability > abstraction**: in the MVP phase, prioritize correctness, maintainability, and testability over architectural flair
- **Constrained AI**: the template gives the AI (incl. Claude Code) a strong set of constraints to avoid "improvising a pile of code"
- **Traceable decisions**: every non-obvious trade-off goes into `docs/decisions.md`

---

## Reference implementation

The template is distilled from a real production project (a receiver-side service with external data queries + LLM calls + async callbacks).

`examples/sample-comment-service/` provides a **fully filled-in** reference sample (a comment-generation service) that shows what the template looks like once completed — how the four documents read when written for real, and how state-machine / LLM rules map to concrete fields. When you're unsure how detailed a section should be, look there.

---

## Versioning of the template itself

See `CHANGELOG.md`. The template keeps evolving with practice; once a new project adopts it, you do **not** need to chase the template's later updates (unless there's a critical fix).
