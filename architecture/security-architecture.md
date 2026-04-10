# Security Architecture

**Version:** 1.0.0  
**Date:** 2026-02-25  
**Status:** Architecture Reference (Security)  
**License:** Apache-2.0

---

## 1. Security objectives

FemtoClaw security is designed to ensure:

- **execution integrity**: only validated, authorized actions execute
- **least privilege**: the runtime has no more authority than necessary
- **auditability**: every decision is recorded
- **resilience**: failures are contained and observable

---

## 2. Trust boundaries

There are two primary trust boundaries:

1. **Inference boundary**: inference output is untrusted until validated.
2. **Execution boundary**: only capability-gated execution may touch OS/network.

Additionally, secrets and credentials are a boundary: they MUST NOT be printed or stored in cleartext logs.

---

## 3. Threat model (informative)

Representative threats include:
- prompt injection attempting unauthorized tool invocation
- exfiltration attempts via network capabilities
- malicious file/path input
- command injection (shell)
- denial-of-service via large payloads or loops
- unsafe privilege configuration

FemtoClaw mitigations are implemented through validation, allowlists, budgets, and explicit enablement.

---

## 4. Protocol validation (normative)

- Runtime MUST accept only strict protocol outputs.
- Runtime MUST reject outputs containing both `message` and `tool_call`.
- Runtime MUST reject tool names outside allowed character set/length.
- Runtime MUST validate args against capability schemas/policies.

Protocol validation failures MUST be reported as “validation errors” (not execution errors).

---

## 5. Capability gate (normative)

The Capability Gate MUST:
- enforce deny-by-default
- enforce per-capability policy
- enforce budget limits (time, rate, bytes)
- enforce redaction rules

The Capability Gate MUST NOT be bypassable by inference output.

---

## 6. OS privilege and hardening (recommended)

Recommended deployment tiers:

- **User Mode**: safest; suitable for dev and local automation
- **Service Mode**: controlled authority; best for servers and CI
- **Administrator/Root Mode**: only when necessary; requires strict allowlists and sandboxing

Hardening recommendations:
- run as dedicated OS user
- set filesystem permissions narrowly
- disable shells or dangerous binaries unless necessary
- isolate network access (firewall/egress rules)

---

## 7. Secret handling

Secrets MUST:
- be sourced from environment variables, OS keychains, or vault providers
- never be hardcoded
- be redacted from logs and audit records

Capabilities accessing secrets SHOULD return opaque handles rather than raw secret values where possible.

---

## 8. Observability and incident response

FemtoClaw SHOULD emit structured events for:
- validation failures
- authorization denials
- execution errors
- abnormal latency/timeout events

These events enable operators to detect and respond to misuse or misconfiguration.
