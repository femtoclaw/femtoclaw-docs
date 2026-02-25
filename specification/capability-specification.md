# Capability Specification (Claw Contract)

**Version:** 1.0.0  
**Date:** 2026-02-25  
**Status:** Normative Specification  
**License:** Apache-2.0

---

## 1. Overview

Capabilities (“Claws”) define the execution surface of FemtoClaw. This document specifies the required behavior and interface contract for capability implementations.

A capability implementation is considered compliant if it:
- implements the required interface
- validates inputs
- enforces policy constraints delegated by the runtime
- emits consistent, structured results

---

## 2. Required interface (conceptual)

A capability MUST provide:

- `name() -> &'static str`
- `description() -> &'static str`
- `execute(args: JSON) -> Result<JSON>`

`name()` MUST be stable across versions. Changing a capability name is a breaking change.

---

## 3. Input validation (MUST)

Capabilities MUST validate:
- required fields present
- types are correct
- bounds are enforced (length, count, sizes)
- strings are sanitized for command/path injection risk

Capabilities MUST return structured errors on invalid input.

---

## 4. Side-effect classification (SHOULD)

Capabilities SHOULD declare a risk classification:

- read_only
- write
- process_control
- network
- secrets

The runtime SHOULD use classifications to apply default policies.

---

## 5. Output constraints (SHOULD)

Capabilities SHOULD bound output:
- stdout/stderr size limits
- response object size limits

Large outputs SHOULD be truncated with explicit markers.

---

## 6. Idempotence (recommended)

For operational safety, write-oriented capabilities SHOULD support idempotent modes where possible and expose a `dry_run` option when appropriate.

---

## 7. Audit requirements (MUST)

Capability executions MUST be auditable by the runtime. Capabilities SHOULD return metadata useful for audit trails, such as:

- operation name
- resource identifiers (paths/URLs) (redacted where sensitive)
- outcome category

---

## 8. Example: Shell capability args (illustrative)

```json
{
  "bin": "systemctl",
  "argv": ["restart","nginx"],
  "cwd": "/",
  "timeout_ms": 10000
}
```

Production runtimes SHOULD enforce:
- allowlist on `bin`
- maximum argv length
- maximum timeout
