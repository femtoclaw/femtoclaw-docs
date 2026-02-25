# Compliance Specification

**Version:** 1.0.0  
**Date:** 2026-02-25  
**Status:** Normative Compliance Definition  
**License:** Apache-2.0

---

## 1. Purpose

This document defines what it means to be “FemtoClaw compliant” at the runtime level.

Compliance ensures that implementations preserve:
- protocol correctness
- deterministic execution authority boundaries
- capability isolation
- safety gates and auditing

---

## 2. Compliance dimensions

### 2.1 Protocol compliance
Implementation MUST:
- enforce strict protocol parsing
- reject invalid or ambiguous outputs
- classify validation errors distinctly

### 2.2 Capability compliance
Implementation MUST:
- deny-by-default
- require explicit registration
- enforce policy checks prior to execution
- record audit events

### 2.3 Determinism compliance
Implementation MUST:
- preserve deterministic state transitions
- ensure runtime decisions are reproducible given identical inputs/policy

### 2.4 Observability compliance
Implementation MUST:
- emit structured events for all decision points
- provide stable correlation identifiers

---

## 3. Pass/fail criteria

A compliant implementation MUST pass:
- protocol test suite
- capability boundary tests
- determinism tests
- security isolation tests
- performance baseline tests (configurable thresholds)

---

## 4. Evidence requirements

Compliance evidence SHOULD include:
- test results (machine-readable JSON)
- runtime build fingerprint (version, commit hash)
- policy configuration snapshot used during testing
