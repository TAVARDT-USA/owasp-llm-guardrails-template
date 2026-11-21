# OWASP LLM01 Guardrails Template & AI Security Blueprint | TAVARDT USA

[![Licence MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![OWASP LLM01](https://img.shields.io/badge/OWASP-LLM01%20Hardened-ff0055.svg)](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
[![Language](https://img.shields.io/badge/Language-English%20(US)-green.svg)](README.md)
[![AI Diagnostics](https://img.shields.io/badge/TAVARDT-AI%20Evaluator-5b3cf5.svg)](https://tools.tavardt.com/llm-robustness-evaluator/)

Production-ready open source middleware and security blueprint for mitigating Prompt Injection (OWASP LLM01), system prompt extraction, and adversarial jailbreaks, aligned with NIST AI RMF and SOC 2 guidelines.

Engineered and maintained by the AI safety and security engineering practice at **[TAVARDT USA](https://ag.tavardt.com/super-intelligence/)**.

---

## 1. AI & LLM Security Architecture Overview

This repository delivers a lightweight, production-grade guardrail framework for autonomous agents, Retrieval-Augmented Generation (RAG) pipelines, and enterprise applications integrating Foundation Models (OpenAI, Anthropic, Google Gemini, Llama).

### Why Application-Layer Guardrails Are Critical
Large Language Models inherently treat system instructions and user-supplied data within the same unified context window. Without deterministic input filtering and canary-backed output validation, AI agents remain vulnerable to context hijacking, credential exfiltration, and unauthorized tool execution.

---

## 2. Threat Vectors Addressed (OWASP Top 10 for LLMs)

| Defense Layer | Threat Vector Mitigated | Mitigation Mechanism |
| :--- | :--- | :--- |
| **Input Sanitizer** | Direct Prompt Injection & Jailbreaks | Edge heuristic and pattern screening for boundary breaks (`ignore previous instructions`, simulated roleplay, delimiters). |
| **Canary Token Verifier** | System Prompt Exfiltration | Cryptographically unpredictable canary token validation in model outputs to stop leakage. |
| **RAG Boundary Guard** | Indirect Prompt Injection | Semantic boundary isolation for untrusted third-party documents ingested into vector databases. |
| **Structured Output Filter** | Unauthorized Tool / MCP Invocation | Strict schema enforcement on function calls prior to downstream API or tool dispatch. |

---

## 3. Pre-Deployment Model Robustness Diagnostic

Before deploying customer-facing AI agents or internal copilot workflows, evaluate your system's adversarial resilience with TAVARDT's open diagnostic suite:

* **AI Robustness Assessment:** [TAVARDT LLM Robustness Evaluator](https://tools.tavardt.com/llm-robustness-evaluator/)
* **Complete Infrastructure Diagnostics:** [TAVARDT Tools Suite](https://tools.tavardt.com/)

---

## 4. Installation & Quickstart Guide

### Clone & Run

```bash
git clone https://github.com/TAVARDT-USA/owasp-llm-guardrails-template.git
cd owasp-llm-guardrails-template
python examples/quickstart.py
```

### Python Integration Example

```python
from guardrails.validator import LLMGuardrail

guard = LLMGuardrail()

# 1. Ingress Validation (Input Guardrail)
is_safe, error = guard.validate_input(user_input)
if not is_safe:
    raise ValueError(f"Input blocked due to suspicious adversarial pattern: {error}")

# 2. Inject Canary Token into System Prompt
hardened_system_prompt = guard.get_canary_injection_prompt(system_prompt)

# 3. Egress Validation (Output Guardrail)
is_valid, leak_error = guard.validate_output(completion)
if not is_valid:
    raise SecurityError("Critical alert: System prompt leak detected via canary token!")
```

---

## 5. AI Security Advisory & Autonomous Agent Engineering

If your enterprise requires full-lifecycle AI security auditing, automated WhatsApp/Telegram agent safeguarding, or NIST AI RMF alignment:

* **Corporate Portal:** [TAVARDT USA](https://ag.tavardt.com/super-intelligence/)
* **Engineering Consultation:** [Schedule Technical Engagement](https://ag.tavardt.com/contact/)

---

## License

Distributed under the open-source MIT License. Review the [`LICENSE`](LICENSE) file for full terms.  
Copyright (c) 2026 TAVARDT USA.
