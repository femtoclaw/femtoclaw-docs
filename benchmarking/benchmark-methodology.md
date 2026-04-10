# Benchmark Methodology

**Version:** 1.0.0  
**Date:** 2026-02-25  
**License:** Apache-2.0

---

## 1. Purpose

This document defines how to benchmark FemtoClaw runtime overhead in a repeatable, production-relevant way.

This methodology measures the runtime itself — not model intelligence.

---

## 2. Principles

Benchmarks MUST be:
- reproducible
- comparable across machines (when normalized)
- explicit about inputs and configurations

Benchmarks SHOULD separate:
- protocol validation cost
- capability dispatch cost
- memory update cost
- end-to-end step cost
- startup latency cost

---

## 3. Environment capture (MUST)

Benchmark reports MUST include:
- CPU model and core count
- OS version
- build profile (release flags)
- runtime version and commit hash
- iterations and warmup settings

---

## 4. Metrics

Recommended baseline metrics:

- **Startup latency**: p50/p95/p99 process start to ready
- **Protocol parse/validate**: ns/op and throughput
- **Capability dispatch**: ns/op
- **Memory operations**: push/evict costs
- **E2E step**: simulated step latency

---

## 5. Benchmark hygiene

- disable background workloads where possible
- pin CPU frequency governor (servers)
- run multiple trials and report distribution
- report percentiles, not just means

---

## 6. Reporting format

Reports SHOULD provide:
- summary table
- percentile charts (optional)
- JSON export for automation pipelines
