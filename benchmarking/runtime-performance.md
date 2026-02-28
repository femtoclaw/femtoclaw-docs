# Runtime Performance: FemtoClaw

**Version:** 1.0.1  
**Date:** 2026-02-28  
**License:** Apache-2.0

---

## 1. Scope

This document reports runtime overhead and memory usage metrics for FemtoClaw.

---

## 2. Test Environment

- CPU: Intel Core i7-5500U (2 cores / 4 threads)
- OS: Windows 10 Home 10.0.19045
- Rust: rustc 1.93.0 (2026-01-19)
- Bench runner: `femtoclaw-bench` 1.0.3

---

## 3. Benchmark Method

Measurements were collected with:

```powershell
cd d:\code\femtoclaw\femtoclaw-bench
cargo run --release -- run --preset all --iters 200000 --json results-all.json
cargo run --release -- startup --bin ..\femtoclaw\target\release\femtoclaw.exe --iterations 100 -- once ping
```

---

## 4. Performance Results

### 4.1 Steady-state overhead

| Metric | Unit | FemtoClaw |
|---|---:|---:|
| protocol.parse.message | ns/op | 1964.84 |
| protocol.parse.tool_call | ns/op | 4611.75 |
| capability.dispatch.lookup+validate | ns/op | 105.35 |
| memory.stm.push+evict(25 msgs) | ns/op | 5786.81 |
| e2e.simulated.step | ns/op | 4853.40 |

### 4.2 Startup latency

| Metric | Unit | FemtoClaw |
|---|---:|---:|
| startup.p50 | ms | 16.63 |
| startup.p95 | ms | 25.61 |
| startup.p99 | ms | 38.87 |

### 4.3 Memory usage overhead (RSS)

| Metric | Unit | FemtoClaw |
|---|---:|---:|
| memory.rss.before | KiB | 3440 |
| memory.rss.after | KiB | 4260 |
| memory.rss.delta.alloc(4096 msgs) | KiB | 820 |

---

## 5. Interpretation

- FemtoClaw shows low runtime overhead in local measurements.
- Capability dispatch remains near sub-microsecond overhead (`~105 ns/op` in this run).
- The benchmark now captures process memory usage overhead using RSS before/after a fixed allocation burst.

---

## 6. Reproducibility

To reproduce, run the same benchmark commands on the same host profile and report:
- CPU model and core count
- OS version
- Rust/toolchain version
- iteration counts and build profile
