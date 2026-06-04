# Contributing Guide

**English** | [简体中文](CONTRIBUTING.zh-CN.md)

Thank you for helping improve `claude-workflow-template`. This project is a **technology-stack-agnostic "AI collaboration + docs-first" workflow template**. Contributing means making its rules and document skeleton clearer, more general, and easier to adopt.

## What to Contribute

Contributions welcome in the following categories:

- **Rule improvements** — a constraint in `CLAUDE.md` is unclear, ambiguous, or counterproductive in practice
- **Document skeleton improvements** — structural improvements to the core four (`PROJECT.md` / `SPEC.md` / `TASKS.md` / `ACCEPTANCE.md`) or to templates in `docs/`
- **Consistency fixes** — cross-references between documents that are broken (directory does not exist, section number is wrong, etc.)
- **Example additions** — add a fully filled-in example under `examples/` for a different tech stack or use case
- **Usability** — onboarding flow, placeholder conventions, cross-platform compatibility (especially Windows)

## Contributing Principles (consistent with the template's own philosophy)

This template advocates "docs-first, minimal change, stability over cleverness." Please follow the same approach when contributing:

1. **One PR, one thing** — do not mix unrelated changes
2. **Explain rule changes** — when modifying a constraint in `CLAUDE.md`, describe in the PR body what scenario caused the original rule to break down
3. **Stay technology-stack-agnostic** — do not embed assumptions about a specific language or framework into the general template (language-specific content belongs in `examples/`)
4. **Placeholder convention** — mark all fill-in positions with `<angle brackets>` and `DELETE the example above and fill in` / `REPLACE with your project`, so a single `grep` can locate them all
5. **Update both sides of a reference** — when you change a cross-reference in one document, confirm the target document actually exists and the section number is correct

## Submission Process

1. Fork the repository and cut a feature branch from `main`
2. Make your changes, ensuring placeholder conventions are consistent and cross-document references are correct
3. Commit messages: the type prefix should be English (e.g. `docs:` / `fix:`); the description body may be in English or Chinese, consistent with the history of this repository
4. Open a PR and describe what changed, why it changed, and which documents are affected
5. For significant rule or structural changes, consider opening an issue for discussion before starting work

## Feedback Channels

- Found a bug / inconsistency → open an issue (use the "Bug Report" template)
- Have an improvement idea → open an issue (use the "Improvement Suggestion" template) or send a PR directly
