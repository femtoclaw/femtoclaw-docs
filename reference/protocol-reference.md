# Protocol Reference (Field-Level)

**Version:** 1.0.0  
**Date:** 2026-02-25  
**License:** Apache-2.0

---

## 1. Top-level fields

The output MUST contain exactly one of:

- `message`
- `tool_call`

No other top-level output is accepted for execution control.

---

## 2. `message`

### Fields
- `content` (string): user-facing response text

### Notes
- `message` is safe and does not invoke capabilities.
- Runtime MAY still record it to memory.

---

## 3. `tool_call`

### Fields
- `tool` (string): capability identifier
- `args` (object): capability argument object

### Notes
- `tool_call` does not guarantee execution.
- Runtime MUST validate and authorize the call before executing.
- Runtime MUST record authorization outcome.

---

## 4. Examples

Message:

```json
{"message":{"content":"Completed."}}
```

Tool call:

```json
{
  "tool_call": {
    "tool": "fs",
    "args": {"op":"read","path":"/etc/hosts"}
  }
}
```

Rejected output (unknown tool):

```json
{
  "tool_call": {
    "tool": "delete_everything",
    "args": {}
  }
}
```
