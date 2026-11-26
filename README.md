<p align="center">
  <a href="https://ag.tavardt.com/">
    <img src="https://ag.tavardt.com/img/tavardt-banner.png" alt="TAVARDT" width="1024" />
  </a>
</p>

# OWASP LLM01 Guardrails Template & AI Security Blueprint

[![OWASP LLM01](https://img.shields.io/badge/OWASP-LLM01%20Hardened-ff0055.svg)](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
[![AI Diagnostics](https://img.shields.io/badge/TAVARDT-AI%20Evaluator-5b3cf5.svg)](https://tools.tavardt.com/llm-robustness-evaluator/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

***

Production-ready open source middleware and security blueprint for mitigating Prompt Injection (OWASP LLM01), system prompt extraction, and adversarial jailbreaks, engineered by **TAVARDT**, aligned with NIST AI RMF, OWASP Top 10 for LLMs, and SOC 2 Type II guidelines.

Large Language Models inherently process system instructions and user-supplied text within a shared context window. Without application-layer input sanitization and canary-backed output validation, autonomous agents and RAG pipelines remain vulnerable to context hijacking, credential exfiltration, and unauthorized tool execution.

***

## Core Capabilities and Defensive Architecture

* **Deterministic Ingress Sanitization**: Scans incoming prompts against compiled regex heuristics to block instruction overrides, simulated personas, and delimiter tampering before reaching the model.
* **Cryptographic Canary Token Verification**: Injects unpredictable tokens (`TAVARDT_CANARY_<hex16>`) via Python `secrets` to detect and terminate sessions attempting system prompt leakage.
* **Comprehensive Threat Coverage**: Mitigates OWASP-LLM01 (Prompt Injection), OWASP-LLM06 (Sensitive Information Disclosure), and OWASP-LLM07 (Insecure Plugin Design).
* **Zero External Dependencies**: Operates entirely with the Python standard library, delivering sub-2ms evaluation latency with zero third-party network calls.
* **Drop-in Integration Architecture**: Easily wraps any LLM provider (OpenAI, Anthropic, Google Gemini, local Llama models) across autonomous agents, chatbots, and RAG pipelines.

***

## Threat Vectors and Operational Impact

Deploying foundation models in production without defensive guardrails exposes organizational data and agentic tools to adversarial manipulation. The template neutralizes four critical risk vectors:

* **Direct Prompt Injection (OWASP LLM01)**: Attackers submitting instruction resets (`ignore previous instructions`) to force model compliance with malicious tasks.
* **System Prompt Exfiltration (OWASP LLM06)**: Social engineering queries designed to coerce the model into revealing proprietary prompt instructions and confidential rules.
* **Delimiter Escape and Jailbreak Roleplay**: Exploitation of markdown or XML boundary markers to switch the model into unrestricted or developer modes.
* **Indirect Context Injection via Vector Stores**: Adversarial payloads hidden within third-party documents that hijack agent reasoning during retrieval-augmented generation.

***

## Installation and Execution CLI

Integrate the guardrail middleware into your Python application or test it locally with the included quickstart runner:

```bash
# Clone the official repository
git clone https://github.com/TAVARDT-USA/owasp-llm-guardrails-template.git

# Enter repository workspace
cd owasp-llm-guardrails-template

# Run the quickstart verification script
python examples/quickstart.py
```

### Python Integration Example

Wrap any model inference call with deterministic ingress and egress guardrails:

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

***

## Frequently Asked Technical Questions

### What threat vectors does the OWASP LLM guardrails template mitigate across foundation model pipelines?

The template enforces deterministic application-layer defenses against direct prompt injection, adversarial jailbreak overrides, and system prompt exfiltration. By combining ingress regex pattern screening with canary token egress verification, the middleware protects LLM workloads without requiring fine-tuning.

### How does dynamic canary token verification prevent system prompt leakage?

The LLMGuardrail class generates an unpredictable cryptographic canary token and injects it into system instructions with strict non-disclosure directives. During output validation, the validator scans model completions for this secret token, immediately intercepting and suppressing responses that leak internal instructions.

### Why is deterministic input sanitization necessary if the underlying model already has safety alignment?

Model safety alignments can be bypassed through sophisticated adversarial phrasing, encoded instructions, or simulated roleplay personas. Deterministic regex screening intercepts known jailbreak patterns before tokens reach the context window, eliminating inferential risk and saving inference compute costs.

### How does this guardrails template integrate into agentic workflows and retrieval-augmented generation pipelines?

The guardrail wraps inference cycles by screening both retrieved third-party document chunks and user prompts before prompt construction occurs. This prevents indirect prompt injections hidden in vector stores from hijacking model reasoning or invoking unauthorized downstream tools.

### What is the computational and latency overhead introduced by the guardrail validation layer?

The Python validator executes strictly in-memory using compiled regular expressions and native string comparisons, completing validation in under 2 milliseconds. Because the guardrail operates without external API calls or secondary LLM evaluators, it adds zero network latency to production pipelines.

***

## Useful Links

* **Corporate Portal:** https://ag.tavardt.com/
* **Diagnostic Suite:** https://tools.tavardt.com/
* **Technical Contact:** https://ag.tavardt.com/contact/

***

### License
Released under the MIT License. See [LICENSE](LICENSE) for full details.

***

© 2026 TAVARDT. All rights reserved.
