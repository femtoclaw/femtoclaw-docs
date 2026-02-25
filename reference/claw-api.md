# Claw API Reference (Capability Interface)

**Version:** 1.0.0  
**Date:** 2026-02-25  
**License:** Apache-2.0

---

## 1. Definition

A “Claw” is a capability module that implements a stable interface and provides controlled access to system resources.

---

## 2. Canonical interface (conceptual)

```rust
trait Claw: Send + Sync {
  fn name(&self) -> &'static str;
  fn description(&self) -> &'static str;
  fn execute(&self, args: serde_json::Value) -> anyhow::Result<serde_json::Value>;
}
```

---

## 3. Capability registry (recommended)

A runtime typically maintains a registry mapping `name -> implementation`.

Registry MUST:
- deny unknown names
- provide stable lookup
- support explicit registration only

---

## 4. Example: ShellClaw args

```json
{
  "bin": "echo",
  "argv": ["FemtoClaw operational"]
}
```

Production policy SHOULD:
- allowlist allowed binaries
- restrict argv length
- enforce timeouts
- capture stdout/stderr with size bounds

---

## 5. Example: FsClaw args

```json
{
  "op": "read",
  "path": "/var/log/app.log"
}
```

Implementations SHOULD prevent:
- path traversal
- unsafe writes (unless explicitly enabled)
