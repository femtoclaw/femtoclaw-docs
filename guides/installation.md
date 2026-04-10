# Installation Guide

**Version:** 1.0.3
**Date:** 2026-04-09
**License:** Apache-2.0

---

## 1. Quick Install (macOS/Linux)

For a fast, one-liner installation on macOS or Linux:

```bash
curl -fsSL https://femtoclaw.org/install.sh | sh
```

This will download the latest pre-compiled binary and install it to `/usr/local/bin`.

---

## 2. Prerequisites

- Rust toolchain (stable) if installing via Cargo
- Supported OS: macOS, Linux, Windows
- Supported CPU: x86_64, arm64 (and other Rust targets, depending on builds)

---

## 2. Install (Cargo)

```bash
cargo install femtoclaw
```

Verify:

```bash
femtoclaw --version
```

---

## 3. Upgrade

```bash
cargo install femtoclaw --force
```

---

## 4. Verify operational mode

Run in interactive mode:

```bash
femtoclaw run
```

One-shot mode:

```bash
femtoclaw once "report system status"
```

---

## 5. Local-only mode (recommended for secure environments)

If your build supports local inference providers, prefer local-only mode in restricted environments:

```bash
femtoclaw run --brain local
```

---

## 6. Operational hardening (recommended)

- Use a dedicated OS user for FemtoClaw.
- Keep capabilities deny-by-default; enable only what you need.
- For servers, run FemtoClaw as a service with restricted filesystem permissions.
