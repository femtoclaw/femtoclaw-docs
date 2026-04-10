# Runtime API Reference

**Version:** 1.0.0  
**Date:** 2026-02-25  
**License:** Apache-2.0

---

## 1. Overview

This document describes the runtime integration surface. Exact function signatures may vary by implementation, but the conceptual API and configuration model must preserve FemtoClaw invariants.

---

## 2. Runtime modes

Common runtime modes:

- `run` — interactive session / daemon loop
- `once` — single-shot evaluation and response
- `serve` — optional server mode (HTTP/gRPC integration)

---

## 3. Configuration model (recommended)

A runtime SHOULD accept configuration via:
- environment variables
- configuration file (TOML/YAML/JSON)
- CLI flags

Key configuration domains:
- enabled capabilities
- capability allowlists/deny rules
- timeouts and budgets
- logging verbosity and redaction
- inference provider selection (Brain)

---

## 4. Event model

Runtimes SHOULD expose structured events for:
- state transitions
- validation failures
- authorization decisions
- capability invocations
- errors and timeouts

Events should carry:
- correlation_id
- session_id
- step_id
- timestamps
- classification fields

---

## 5. Embedding FemtoClaw

For embedding in other applications, a runtime library SHOULD allow:
- registering capabilities programmatically
- providing a Brain implementation
- providing a Memory backend
- providing policy rules or hooks
