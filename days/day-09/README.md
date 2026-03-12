# Day 9: OpenAI Guardrails & Tracing

> **Week 2: Framework Mastery**

## Overview
Today you'll add safety layers and deep observability to the customer service system from Day 8. You'll implement input guardrails (PII detection, prompt injection defense), output guardrails (toxicity filtering), a tripwire guardrail that halts execution on detection, and a cost circuit breaker. Then you'll build custom trace spans to create a debugging dashboard for the full multi-agent flow.

## Learning Objectives
- [ ] Implement an input guardrail that detects and redacts PII using regex and LLM verification
- [ ] Build an output guardrail that filters toxic or off-brand responses
- [ ] Add a tripwire guardrail that immediately stops agent execution on trigger
- [ ] Create a cost circuit breaker that halts agents exceeding a token/dollar budget
- [ ] Build custom trace spans and explore the tracing dashboard for agent debugging

## What You'll Build
A hardened version of Day 8's customer service system with PII detection, toxicity filtering, prompt injection defense, cost limits, and a full tracing dashboard -- the production safety stack every agent needs.

## Prerequisites
- Completed Day 8 (customer service multi-agent system)
- `pip install openai-agents`
- OpenAI API key

## Steps

### Step 1: Build the PII Detection Input Guardrail
Create an input guardrail that runs before the agent processes any message. Implement two layers: (1) **Regex layer** -- patterns for email addresses, phone numbers, SSNs, credit card numbers using compiled regex, (2) **LLM layer** -- send the message to `gpt-4o-mini` with a prompt: "Does this message contain PII? Return {contains_pii: bool, pii_types: [], redacted_text: str}". If PII is detected, either redact it and continue or reject the message. Register it using the SDK's `@input_guardrail` decorator.

### Step 2: Build the Toxicity Output Guardrail
Create an output guardrail that inspects every agent response before it reaches the user. Use `gpt-4o-mini` as a classifier: "Rate this response for toxicity, brand safety, and helpfulness on a 1-5 scale. Return {toxic: bool, off_brand: bool, reasoning: str}". If toxic or off-brand, replace the response with a safe fallback message. Register with `@output_guardrail`. Test with adversarial prompts designed to make the agent say something inappropriate.

### Step 3: Implement a Tripwire Guardrail
Build a guardrail that detects prompt injection attempts and immediately halts execution (tripwire pattern). Check for known injection patterns: "ignore previous instructions", "you are now", system prompt extraction attempts, and role-play attacks. When triggered, raise a `GuardrailTripwireTriggered` exception that stops the agent loop entirely and returns a security notice. This is different from regular guardrails -- it's a hard stop, not a filter.

### Step 4: Add a Cost Circuit Breaker
Implement a middleware that tracks cumulative token usage across all LLM calls in a session. Define limits: max 10,000 tokens per conversation, max $0.50 per session, max 20 LLM calls per conversation. When any limit is hit, stop the agent and return a message: "This conversation has reached its resource limit. Please start a new session or contact support." Track usage in a simple counter object passed through the agent context.

### Step 5: Build Custom Trace Spans
Use the SDK's tracing API to add custom spans: (1) a `guardrail_check` span around each guardrail execution (recording input, result, latency), (2) a `tool_execution` span with input/output sizes, (3) a `handoff` span capturing source agent, target agent, and reason. Structure spans hierarchically: conversation -> turn -> agent -> guardrail/tool/llm_call. Export traces to JSON.

### Step 6: Create a Debugging Dashboard
Build a simple Python script that reads trace JSON files and generates a terminal-based dashboard (using `rich` or plain print formatting): (1) conversation timeline showing agent activations and handoffs, (2) token usage breakdown by agent and tool, (3) guardrail trigger log with timestamps, (4) total cost and latency summary. Run your Day 8 test cases with guardrails enabled and analyze the dashboard output.

## Key Concepts
- **Input vs Output Guardrails:** Input guardrails inspect user messages before processing (prevent bad input). Output guardrails inspect agent responses before delivery (prevent bad output). Both are necessary -- they catch different failure modes.
- **Tripwire Guardrails:** Unlike regular guardrails that filter or modify content, tripwires halt execution entirely. Use them for security-critical detections (prompt injection, data exfiltration attempts) where continuing is itself dangerous.
- **Cost Circuit Breakers:** Agents can enter infinite loops or generate unexpectedly expensive tool chains. Circuit breakers enforce hard resource limits, preventing runaway costs in production.
- **Custom Trace Spans:** The SDK's auto-tracing captures LLM calls, but custom spans let you trace business logic: which guardrail triggered, why a handoff happened, how long a tool took. This is the difference between "I can see API calls" and "I can debug agent behavior."

## Resources
- [OpenAI Agents SDK Guardrails guide](https://openai.github.io/openai-agents-python/guardrails/)
- [OpenAI Agents SDK Tracing guide](https://openai.github.io/openai-agents-python/tracing/)
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) -- prompt injection and more
- [NeMo Guardrails by NVIDIA](https://github.com/NVIDIA/NeMo-Guardrails) -- alternative guardrails framework

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-08/README.md) | [Home](../../README.md) | [Next >](../../capstones/day-010-yetibot/README.md)
