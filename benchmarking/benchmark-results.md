# Benchmark Results (Format + Example)

**Version:** 1.0.0  
**Date:** 2026-02-25  
**License:** Apache-2.0

---

## 1. Purpose

This document defines the expected structure of benchmark results and provides example tables suitable for internal performance tracking.

---

## 2. Example summary table

| Metric | Unit | p50 | p95 | p99 | Notes |
|---|---:|---:|---:|---:|---|
| startup.latency | ms | 6.2 | 9.1 | 11.4 | process spawn to exit/ready |
| protocol.parse.message | ns/op | 420 | 530 | 610 | strict JSON parse |
| protocol.parse.tool_call | ns/op | 680 | 820 | 940 | includes arg object |
| capability.dispatch | ns/op | 120 | 160 | 190 | registry lookup + validation |
| e2e.simulated.step | ns/op | 980 | 1200 | 1400 | parse+dispatch+mediate |

---

## 3. Report bundle contents (recommended)

- console summary
- JSON report artifact
- environment capture
- configuration snapshot
