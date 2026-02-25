# Certification Process

**Version:** 1.0.0  
**Date:** 2026-02-25  
**License:** Apache-2.0

---

## 1. Overview

Certification is the operational process by which a FemtoClaw runtime build is verified to meet compliance requirements and is approved for production deployment.

Certification is repeatable and auditable.

---

## 2. Certification levels (recommended)

- **Level 1 — Development**
  - protocol compliance
  - basic capability isolation
  - minimal logging

- **Level 2 — Production**
  - full compliance suite
  - audit logging and redaction
  - performance baselines met

- **Level 3 — High Assurance**
  - sandboxing/containment required
  - stricter allowlists
  - extended security verification and review

---

## 3. Process steps

1. **Build**
   - produce signed artifacts if possible
2. **Test**
   - run compliance suite with pinned configuration
3. **Review**
   - verify failures and waivers (if any)
4. **Approve**
   - produce certification report (JSON + human-readable summary)
5. **Deploy**
   - deploy with the same policy baseline used for certification
6. **Monitor**
   - ensure observability indicates stable behavior

---

## 4. Certification artifacts

A certification bundle SHOULD include:
- test report JSON
- runtime binary checksum (SHA256)
- version manifest
- policy allowlist snapshot
- list of enabled capabilities
- operator sign-off metadata

---

## 5. Renewal and drift

Certification SHOULD be renewed when:
- runtime version changes
- policy changes significantly
- capability set changes
- operating environment changes (OS, container base, etc.)

Policy drift without recertification is strongly discouraged.
