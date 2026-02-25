# Integration Guide

**Version:** 1.0.0  
**Date:** 2026-02-25  
**License:** Apache-2.0

---

## 1. CI/CD integration

FemtoClaw can be used in CI/CD for:
- failure analysis
- controlled remediation (approved steps only)
- incident reporting

Recommended integration pattern:
1. run build/test
2. on failure, invoke FemtoClaw in one-shot mode with logs as input
3. allow only read-only capabilities unless an operator approves remediation

---

## 2. Observability integration

FemtoClaw SHOULD integrate with:
- JSON log collectors
- OpenTelemetry (optional)
- SIEM systems for audit ingestion

Key signals to export:
- validation failures
- authorization denials
- capability executions
- timeouts and anomalies

---

## 3. Policy engines

FemtoClaw capability gate can integrate with policy engines (informative examples):
- static allowlists
- OPA/Rego policy checks
- enterprise approval workflows

The runtime SHOULD support offline policy evaluation for secure environments.

---

## 4. Secrets and credentials

Integrate secrets via:
- environment variables (least preferred)
- OS keychains (preferred)
- vault providers (enterprise)

Never embed secrets in prompts or log output.
