# Day 19: Production Reliability & Cost Optimization

> **Week 3: Multi-Agent & Production**

## Overview
Agents in production face real-world challenges: API rate limits, model outages, unpredictable costs, and varying task complexity. Today you'll build a reliability layer with retries, fallbacks, and circuit breakers, plus a smart model router that picks the cheapest model capable of handling each task. These patterns are the difference between a demo and a production system.

## Learning Objectives
- [ ] Implement retry logic with exponential backoff and jitter for transient API failures
- [ ] Build fallback chains and circuit breakers for graceful degradation across model providers
- [ ] Create a model router that classifies task complexity and routes to the most cost-effective model

## What You'll Build
A production reliability layer consisting of: (1) retry middleware with exponential backoff, (2) a fallback chain (GPT-4o -> Claude Sonnet -> local Ollama), (3) a circuit breaker that stops calling failing providers, and (4) a model router that analyzes incoming tasks and routes simple ones to cheap models (GPT-4o-mini) and complex ones to capable models (GPT-4o, Claude). Includes cost tracking dashboard.

## Prerequisites
- OpenAI and Anthropic API keys
- Ollama installed locally with a model pulled (e.g., `ollama pull llama3`)
- Python 3.11+
- Days 11-18 completed

## Steps

### Step 1: Implement Retry with Exponential Backoff
Build a retry decorator that catches rate limit errors (429) and transient failures (500, 502, 503). Implement exponential backoff: wait 1s, 2s, 4s, 8s with random jitter (0-1s). Set max retries to 4. Log each retry attempt with the error and wait time.

### Step 2: Add Fallback Chains
Create a `FallbackLLM` class that wraps multiple providers in priority order. If the primary (GPT-4o) fails after retries, automatically fall back to the secondary (Claude Sonnet), then tertiary (local Ollama). Each fallback normalizes the response format. Log which provider ultimately served each request.

### Step 3: Build a Circuit Breaker
Implement a circuit breaker with three states: CLOSED (normal), OPEN (failing, skip provider), HALF-OPEN (testing recovery). Track failure counts per provider. After 5 consecutive failures, open the circuit for 60 seconds. After cooldown, allow one test request. If it succeeds, close the circuit; if not, reopen.

### Step 4: Implement the Model Router
Build a classifier that analyzes incoming tasks on two dimensions: complexity (simple/medium/complex) and type (generation/analysis/code/conversation). Route: simple tasks -> GPT-4o-mini ($0.15/1M input), medium -> Claude Haiku or GPT-4o-mini, complex -> GPT-4o or Claude Sonnet. The classifier itself uses a cheap model.

### Step 5: Add Cost Tracking
Instrument every LLM call to log: model used, input tokens, output tokens, cost, latency, and success/failure. Build a simple dashboard (terminal or HTML) showing cumulative cost, cost per task, model distribution, and estimated monthly spend at current usage rates. Set budget alerts.

## Key Concepts
- **Exponential Backoff:** Progressively increasing wait times between retries (1s, 2s, 4s, 8s) with random jitter to prevent thundering herd problems.
- **Fallback Chains:** Ordered lists of alternative providers/models tried sequentially when the primary fails, ensuring the system degrades gracefully rather than breaking.
- **Circuit Breaker:** A pattern from distributed systems that stops calling a failing service after repeated failures, preventing cascade failures and allowing recovery time.
- **Model Routing:** Classifying task complexity and routing to the cheapest model capable of handling it — the single biggest lever for reducing agent costs.
- **Token Budgets:** Setting maximum input/output token limits per request and per session to prevent runaway costs from verbose agents or infinite loops.
- **Cost Tracking:** Instrumenting every LLM call with token counts and pricing to maintain visibility into actual spend and optimize over time.

## Resources
- [Circuit Breaker Pattern](https://martinfowler.com/bliki/CircuitBreaker.html)
- [OpenAI Rate Limits](https://platform.openai.com/docs/guides/rate-limits)
- [Anthropic Rate Limits](https://docs.anthropic.com/en/api/rate-limits)
- [LiteLLM (multi-provider routing)](https://github.com/BerriAI/litellm)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-18/README.md) | [Home](../../README.md) | [Next >](../../capstones/day-020-researchcrew/README.md)
