# Engineering Specification (Normative)

**Version:** 1.0.0  
**Date:** 2026-02-25  
**Status:** Normative Specification  
**License:** Apache-2.0

---

## 1. Scope

This document defines **normative requirements** for FemtoClaw runtime implementations and compatible ecosystem components (capabilities, validators, and integration surfaces).

Normative keywords are interpreted per RFC 2119: **MUST**, **SHOULD**, **MAY**.

---

## 2. Invariants (MUST)

FemtoClaw implementations MUST preserve:

1. **Execution authority separation**
   - Inference output MUST NOT directly execute system actions.
   - All actions MUST pass through validation and capability gates.

2. **Strict protocol validation**
   - Only the protocol forms defined in the protocol spec are accepted.

3. **Capability-gated execution**
   - Capabilities MUST be deny-by-default.
   - Only registered capabilities may execute.

4. **Deterministic control flow**
   - Runtime control logic MUST be deterministic for a given input, policy, and capability set.
   - Non-determinism is confined to inference output only.

5. **Observability**
   - Each step MUST emit structured diagnostic events.

---

## 3. Runtime state machine (MUST)

Runtime MUST implement a state machine equivalent to:

- Idle
- Thinking
- Validating
- Authorizing
- Executing
- Recording
- Responding
- Error

Transitions MUST be auditable and produce traceable events.

---

## 4. Resource governance (SHOULD)

Runtime SHOULD enforce:
- maximum input size
- maximum tool output size
- per-step timeouts
- per-session budgets (total time, tool invocations)

---

## 5. Security requirements (MUST)

Runtime MUST:
- reject invalid protocol outputs
- deny unknown capabilities
- validate and sanitize all capability arguments
- support operator-configurable allowlists and deny rules
- implement log redaction for secrets

---

## 6. Compatibility requirements

A compatible FemtoClaw ecosystem component MUST:
- follow protocol spec
- implement capability interface contract
- produce stable identifiers and versioning
- provide deterministic error categories (validation/deny/exec)

---

## 7. Compliance

Implementations SHOULD validate conformance using the FemtoClaw compliance test harness and publish evidence of compliance for production deployments.
