# Capability Architecture

**Version:** 1.0.0  
**Date:** 2026-02-25  
**Status:** Architecture Reference  
**License:** Apache-2.0

---

## 1. Purpose

This document defines FemtoClaw’s **capability model**. Capabilities (also called “Claws”) are the only way the runtime can interact with the operating system, the network, or external systems.

Capabilities are designed to be:
- explicit
- auditable
- policy-controlled
- safe by construction

---

## 2. Capability fundamentals

A capability is an implementation of a stable interface that exposes:

- **name** (stable identifier)
- **description** (operator-facing documentation)
- **execute(args)** (validated execution entrypoint)

A capability MAY be pure (no side effects) or effectful (system changes). Effectful capabilities MUST be gated by stricter policy.

---

## 3. Registration and discovery

- Capabilities MUST be **registered explicitly** at runtime start (deny-by-default).
- The runtime MUST NOT expose dynamic capability discovery to inference outputs beyond what is explicitly allowed.

This prevents inference output from expanding authority.

---

## 4. Policy enforcement

The Capability Gate MUST enforce policy over:

- which capabilities may run
- which arguments are allowed (allowlists/regex/schemas)
- rate limits and budgets
- environment restrictions (e.g., “no writes”, “no network” modes)

Example policy decision outcomes:

- allow
- deny (policy)
- deny (unknown capability)
- deny (invalid args)

---

## 5. Argument validation

Capability inputs MUST be validated:
- required fields present
- field types correct
- length bounds and allowed values enforced
- path traversal and command injection mitigations applied

Example (illustrative) args for a shell capability:

```json
{
  "bin": "ls",
  "argv": ["-la"],
  "cwd": "/var/app"
}
```

In industrial deployment, the runtime SHOULD require an allowlist for `"bin"` and limit `"cwd"` to approved directories.

---

## 6. Execution isolation

Capabilities SHOULD run with:
- least privilege OS user
- sandboxing or container boundary (where feasible)
- timeouts and output size limits

FemtoClaw can operate without sandboxing, but production deployments SHOULD use containment for high-risk capabilities.

---

## 7. Audit and observability

Every capability execution MUST produce an audit record including:
- capability name
- policy decision
- argument digest (redacted where necessary)
- execution latency
- result classification (success, error, denied)

---

## 8. Capability categories (recommended)

- **Read-only**: safe inspection (fs read, status, logs)
- **Write**: controlled changes (config edits, apply patches)
- **Network**: outbound requests (strict allowlists, timeouts)
- **Process/Service**: service restarts, process control (high-risk)
- **Secrets**: retrieval only via OS keychains / vault integrations (high-risk)

Operators SHOULD enable categories explicitly.
