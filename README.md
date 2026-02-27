# 🦅 FemtoClaw Docs

**FemtoClaw — Industrial Agent Runtime** documentation corpus.

FemtoClaw is its own class of product: a lightweight, Rust-based agent runtime built for enterprise and production environments where **correctness, observability, and safety gates** matter.

This repository is the canonical location for:

- Industrial white papers
- Architecture references
- Engineering specifications (protocol, capabilities, runtime model)
- Compliance and certification documentation
- Benchmark methodology and reporting
- API and integration references

**Version:** 1.0.3  
**Date:** 2026-02-26  
**License:** Apache-2.0

---

## 🚀 Quick Start

```bash
# Install
cargo install femtoclaw

# Run with Ollama (local)
export FEMTO_BRAIN=ollama
femtoclaw "What is 2+2?"

# Run with OpenAI
export FEMTO_BRAIN=openai
export FEMTO_OPENAI_API_KEY=sk-...
femtoclaw "your prompt"

# Run with LM Studio (local)
export FEMTO_BRAIN=lmstudio
femtoclaw "your prompt"
```

---

## 🤖 Supported LLM Providers (14)

FemtoClaw supports 14 LLM providers for maximum flexibility:

| Provider | Brain Name | Environment Variables |
|----------|------------|----------------------|
| Local Ollama | `ollama` | FEMTO_OLLAMA_MODEL (default: llama3.2) |
| LM Studio | `lmstudio` | FEMTO_LMSTUDIO_MODEL |
| OpenAI | `openai` | FEMTO_OPENAI_API_KEY, FEMTO_OPENAI_MODEL |
| OpenRouter | `openrouter` | FEMTO_OPENROUTER_API_KEY (100+ models) |
| Anthropic Claude | `anthropic` | FEMTO_ANTHROPIC_API_KEY |
| xAI Grok | `grok` | FEMTO_GROK_API_KEY |
| Google Gemini | `gemini` | FEMTO_GEMINI_API_KEY |
| Amazon Bedrock | `bedrock` | FEMTO_BEDROCK_REGION, FEMTO_BEDROCK_ACCESS_KEY |
| Azure OpenAI | `azure` | FEMTO_AZURE_ENDPOINT, FEMTO_AZURE_API_KEY |
| Mistral AI | `mistral` | FEMTO_MISTRAL_API_KEY |
| DeepSeek | `deepseek` | FEMTO_DEEPSEEK_API_KEY |
| Perplexity | `perplexity` | FEMTO_PERPLEXITY_API_KEY |
| OpenCode Zen | `zen` | FEMTO_ZEN_API_KEY |
| Echo (testing) | `echo` | (none) |

---

## 📚 Contents

### White Paper
- [`whitepaper/industrial-agent-runtime.md`](whitepaper/industrial-agent-runtime.md) — product definition, runtime authority model, deployment posture

### Architecture
- [`architecture/runtime-architecture.md`](architecture/runtime-architecture.md) — subsystem composition and data/control flow
- [`architecture/capability-architecture.md`](architecture/capability-architecture.md) — capability model, isolation, and execution boundaries
- [`architecture/security-architecture.md`](architecture/security-architecture.md) — threat model, gates, sandboxing, and operational hardening

### Specifications
- [`specification/engineering-specification.md`](specification/engineering-specification.md) — requirements, invariants, and implementation constraints
- [`specification/protocol-specification.md`](specification/protocol-specification.md) — strict JSON protocol and validation rules
- [`specification/capability-specification.md`](specification/capability-specification.md) — capability interface and contract

### Guides
- [`guides/installation.md`](guides/installation.md) — install, upgrade, verify
- [`guides/deployment.md`](guides/deployment.md) — dev, enterprise, edge, air-gapped deployment patterns
- [`guides/integration.md`](guides/integration.md) — CI/CD, observability stacks, policy engines

### Compliance
- [`compliance/compliance-specification.md`](compliance/compliance-specification.md) — compliance dimensions and pass/fail criteria
- [`compliance/certification-process.md`](compliance/certification-process.md) — certification lifecycle and evidence requirements

### Benchmarking
- [`benchmarking/benchmark-methodology.md`](benchmarking/benchmark-methodology.md) — measurement discipline, reproducibility rules
- [`benchmarking/benchmark-results.md`](benchmarking/benchmark-results.md) — reporting format and example tables

### Reference
- [`reference/runtime-api.md`](reference/runtime-api.md) — runtime integration surface and configuration model
- [`reference/claw-api.md`](reference/claw-api.md) — capability (“Claw”) interface and examples
- [`reference/protocol-reference.md`](reference/protocol-reference.md) — protocol field reference with examples

---

## 🧭 Documentation Conventions

- **Normative keywords** use RFC 2119 meanings: **MUST**, **SHOULD**, **MAY**.
- Security and compliance sections are **normative** unless explicitly marked as informative.
- Example JSON is illustrative; production policy should be enforced by the runtime validator.

---

## 🧩 Quick mental model

FemtoClaw separates inference from execution authority:

```text
Inference (probabilistic)  →  FemtoClaw Validator  →  Capability Gate  →  Execution (deterministic)
```
