# Release Checklist + Operations Runbook

**English** | [简体中文](runbook.zh-CN.md)

This document is intended for operations / on-call / release engineers.

## 1. Pre-release Checklist

> - [ ] All Phase 1–N tasks in TASKS.md are marked `[x]`
> - [ ] All items in ACCEPTANCE.md are `[x]`
> - [ ] All tests pass (unit + integration + E2E + evals if applicable)
> - [ ] `git log` contains no credential leaks
> - [ ] Image build succeeds; local startup returns `200 OK` for `GET /health`
> - [ ] Credentials injected into K8s Secret (see docs/tools.md §5)
> - [ ] CHANGELOG.md includes release notes

## 2. Deployment Steps

> List every step from image build to traffic cutover.

<!-- DELETE the example above and fill in your project content -->

## 3. Health Check

> `GET /health` path + expected response + probe configuration.

## 4. Common Operations

### 4.1 Restart the Service

### 4.2 View Logs

> Where logs live / how to filter / key fields.

### 4.3 Manually Replay a Failed Task (if applicable)

> SQL template for resetting a `<TERMINAL_FAIL>` record back to `<INITIAL>` + retry_count handling.

### 4.4 Credential Rotation

> Steps: retrieve new credential from the secrets management system → rolling restart → verify.

### 4.5 Database Migration

> Migration tool + command + rollback procedure.

<!-- DELETE the example above and fill in your project content -->

## 5. Troubleshooting

> Common error patterns and diagnostic steps.
>
> | Symptom | Possible cause | Diagnostic command |
> |---|---|---|
> | `GET /health` returns degraded | DB unreachable | Check logs / DB ping |
> | High volume of `<TERMINAL_FAIL>` | External dependency outage | Inspect error_msg distribution |

<!-- DELETE the example above and fill in your project content -->

## 6. Rollback Plan

> If the new release causes issue X, how to roll back to the previous version.
>
> - [ ] Image rollback command
> - [ ] Database migration rollback (if applicable)
> - [ ] Traffic cutover

<!-- DELETE the example above and fill in your project content -->
