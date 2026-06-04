# Dependency & Tool Inventory

**English** | [简体中文](tools.zh-CN.md)

This document lists every external tool required to run, develop, and deploy this project, along with version requirements.

## 1. Development Tools

> Language runtime / package manager / linter / type checker / test framework.
>
> Example:
> | Tool | Version | Purpose |
> |---|---|---|
> | `<language runtime>` | X.Y | Primary language |
> | `<package manager>` | A.B | Dependency management |
> | `<lint tool>` | C.D | Code style enforcement |
> | `<type checker>` | E.F | Static type checking |
> | `<test framework>` | G.H | Unit / integration tests |

<!-- DELETE the example above and fill in your project content -->

## 2. Runtime Dependencies

> Core runtime libraries + versions (aligned with PROJECT.md technical constraints and SPEC.md §10 tech stack).

<!-- DELETE the example above and fill in your project content -->

## 3. External Services

> Database / message queue / third-party APIs / LLM provider and other external service dependencies.
>
> Example:
> | Service | Purpose | Access method |
> |---|---|---|
> | `<persistent data store>` | Business data queries | Internal network, read-only account |
> | `<task store>` | Task persistence | Dedicated schema |
> | `<LLM provider>` (if applicable) | Text generation | Public HTTPS |

<!-- DELETE the example above and fill in your project content -->

## 4. CI / Deployment Tools

> Build / image / deployment pipeline.

<!-- DELETE the example above and fill in your project content -->

## 5. Credential Inventory

> **Do not record credential values here.** List only: credential name / purpose / storage location / who may access it / rotation cycle.
>
> Example:
> | Credential | Purpose | Storage | Owner | Rotation cycle |
> |---|---|---|---|---|
> | `<DB password>` | External data store connection | K8s Secret | DBA | Quarterly |
> | `<API Token>` | Authentication | K8s Secret | Backend | Bi-annually |
> | `<LLM API Key>` | LLM calls | K8s Secret | Backend | As needed |
>
> **Credential values must never appear in this file, commit messages, logs, or prompts.**

<!-- DELETE the example above and fill in your project content -->
