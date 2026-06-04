# Technical Decision Log

**English** | [简体中文](decisions.zh-CN.md)

Records important technical decisions and historical constraints for this project, enabling traceability across future iterations.

Entry format:
- **ID**: DECISION-NNN (chronological order)
- **Date**: YYYY-MM-DD
- **Context**: why this decision was needed
- **Options**: alternatives that were considered
- **Decision**: the chosen approach + rationale
- **Scope of impact**: which modules / documents / code are constrained
- **Follow-up**: under what circumstances should this decision be revisited

Recording principles:
- Every L3 change (see SPEC.md §11) must be written into this file before implementation
- When a recorded decision is overturned, add a new DECISION-NNN entry marked "supersedes DECISION-MMM" — do not delete the old entry
- Probe/inspection conclusions and integration-testing conclusions are also recorded as DECISION-NNN entries

---

## DECISION-000: Workflow Convention (template default — keep or replace)

- **Date**: YYYY-MM-DD
- **Context**: At project kickoff, the team needed to agree on the baseline conventions for AI collaboration, docs-first workflow, and commit discipline.
- **Options**:
  - A: Loose convention (document and commit as needed)
  - B: Strict convention (full CLAUDE.md ruleset, docs-first, one commit per task)
- **Decision**: Adopt B
  1. Follow the core execution flow in `CLAUDE.md` Section 2 strictly
  2. Document priority: PROJECT.md > SPEC.md > ACCEPTANCE.md > TASKS.md > others
  3. One TASKS.md task = one commit + push
  4. Commit message body in Chinese (type prefix in English)
- **Scope of impact**: All AI collaboration workflows and all commit cadence for this project
- **Follow-up**: Once the project stabilizes, evaluate whether to switch to a PR-based workflow

---

<!-- Append subsequent decisions as DECISION-001 / DECISION-002 ... -->
