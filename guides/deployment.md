# Deployment Guide

**Version:** 1.0.0  
**Date:** 2026-02-25  
**License:** Apache-2.0

---

## 1. Deployment targets

FemtoClaw is designed for:
- developer workstations
- CI/CD runners
- enterprise servers and racks
- edge and IoT systems (resource permitting)
- air-gapped environments

FemtoClaw deploys as a **single native binary**.

---

## 2. Deployment modes

### 2.1 Developer mode
- run as user process
- limited capabilities
- verbose logs

### 2.2 Service mode (recommended)
- run as system service (systemd/launchd/Windows service)
- fixed policy allowlists
- structured logs shipped to observability stack

### 2.3 Infrastructure authority mode (high privilege)
- only when necessary
- strict allowlists and sandboxing recommended
- extensive audit requirements

---

## 3. Containers and Kubernetes

FemtoClaw runs well in containers due to small footprint.
Recommended patterns:
- immutable container image containing FemtoClaw binary
- read-only root filesystem where possible
- explicit capability configuration injected via config map / env vars

---

## 4. Air-gapped deployments

For air-gapped environments:
- use local inference providers
- disable network capabilities by policy
- store logs locally and export via approved channels

---

## 5. Operational configuration (example)

Example conceptual configuration items:
- enabled capabilities
- allowlists per capability
- timeouts and budgets
- log redaction rules

Keep policy under version control and review changes like infrastructure code.
