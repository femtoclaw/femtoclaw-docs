# Protocol Specification (Strict Output Protocol)

**Version:** 1.0.0  
**Date:** 2026-02-25  
**Status:** Normative Specification  
**License:** Apache-2.0

---

## 1. Overview

FemtoClaw uses a strict structured output protocol to eliminate ambiguity and enable safe execution gating.

The runtime accepts exactly one of the following top-level objects:

1. `message`
2. `tool_call`

Anything else MUST be rejected.

---

## 2. Message form

### 2.1 Schema

```json
{
  "message": {
    "content": "string"
  }
}
```

### 2.2 Validation rules (MUST)

- `message.content` MUST be a string
- `message.content` MUST be ≤ configured max length

---

## 3. Tool call form

### 3.1 Schema

```json
{
  "tool_call": {
    "tool": "string",
    "args": { }
  }
}
```

### 3.2 Validation rules (MUST)

- `tool_call.tool` MUST be a non-empty string
- `tool_call.tool` MUST match allowed identifier rules (recommended: `[a-z0-9_\-](1, 64)`)
- `tool_call.args` MUST be an object (may be empty)
- Tool calls MUST be denied unless capability is registered and allowed by policy

---

## 4. Exclusivity rule (MUST)

Protocol output MUST contain **exactly one** of:

- `message`
- `tool_call`

Outputs containing both MUST be rejected.

---

## 5. Error handling

Errors MUST be categorized as:
- `validation_error` (invalid structure)
- `authorization_denied` (policy/capability denied)
- `execution_error` (tool failed)
- `infrastructure_error` (I/O, network, runtime issues)

Error details SHOULD be safe for logs (redact secrets).

---

## 6. Versioning

Protocol versioning SHOULD be handled via runtime configuration and validator version pinning.
A future extension MAY add a top-level `"protocol_version"` field; until then, implementations MUST follow this spec as v1.0 behavior.

---

## 7. Examples

Valid message:

```json
{"message":{"content":"Operation complete."}}
```

Valid tool call:

```json
{
  "tool_call": {
    "tool": "shell",
    "args": {"bin":"ls","argv":["-la"]}
  }
}
```

Invalid (both present):

```json
{"message":{"content":"x"},"tool_call":{"tool":"shell","args":{}}}
```
