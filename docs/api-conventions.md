# API Conventions

**English** | [简体中文](api-conventions.zh-CN.md)

This document is intended for external consumers. It defines the protocol (HTTP / other) exposed by this project, covering request structure, response structure, error codes, and authentication details.

Aligned one-to-one with SPEC.md §3 / §7 / §8; if a conflict is found, SPEC.md takes precedence.

## 1. Protocol Overview

> List protocol type, transport, character encoding, and Content-Type.
>
> Example: HTTP/1.1 + JSON + UTF-8 + `Content-Type: application/json`

<!-- DELETE the example above and fill in your project content -->

## 2. Authentication

> Auth header name / value rules / error code.
>
> Example: `X-API-Token: <static-token>` — missing or invalid → HTTP 401.

<!-- DELETE the example above and fill in your project content -->

## 3. Request Structure

> Complete definition of path / method / headers / body.

### 3.1 Path

### 3.2 Body

> Field table (consistent with SPEC.md §3.2).

<!-- DELETE the example above and fill in your project content -->

## 4. Response Structure

### 4.1 Success Response

> Shape of the immediate acknowledgment returned on successful receipt.

### 4.2 Error Response

> Shape of each failure mode.

<!-- DELETE the example above and fill in your project content -->

## 5. Error Codes and error_msg

> Enumerate all error_msg templates (consistent with SPEC.md §8).

## 6. Callback / Push Structure (if applicable)

> Async callback payload shape; idempotency handling required on the consumer side.

<!-- DELETE the example above and fill in your project content -->

## 7. Compatibility / Version Evolution

> Protocol version field (if applicable) + field deprecation process + client upgrade path.
