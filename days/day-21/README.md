# Day 21: Observability & CI/CD for Agents

> **Week 3: Multi-Agent & Production**

## Overview
Production agents fail silently without observability. Today you'll instrument your agents with LangSmith tracing, build a custom metrics dashboard tracking tokens, latency percentiles, error rates, and cost per request, then create a GitHub Actions CI/CD pipeline with canary deployment so you can ship agent updates safely.

## Learning Objectives
- [ ] Instrument agents with LangSmith tracing and custom metadata
- [ ] Build a monitoring dashboard with p50/p95/p99 latency, token usage, error rate, and cost/request
- [ ] Create a GitHub Actions pipeline that lints, tests, and deploys agents
- [ ] Implement canary deployment strategy with automatic rollback
- [ ] Define and monitor SLOs for agent reliability

## What You'll Build
A LangSmith observability dashboard with real-time agent metrics and a GitHub Actions CI/CD pipeline that deploys agent updates via canary releases with automatic rollback on SLO violations.

## Prerequisites
- [LangSmith account and API key](https://smith.langchain.com/)
- GitHub repository with Actions enabled
- Working agent from a previous day (e.g., Day 15 or Day 20)
- `langsmith`, `langchain` Python packages

## Steps

### Step 1: Set Up LangSmith Project
Create a LangSmith project and configure environment variables (`LANGCHAIN_TRACING_V2`, `LANGCHAIN_API_KEY`, `LANGCHAIN_PROJECT`). Verify traces appear in the LangSmith UI by running a simple agent call.

### Step 2: Instrument Agents with Tracing
Add `@traceable` decorators to all agent functions. Attach custom metadata (user_id, session_id, agent_version) to each trace. Log tool calls, LLM invocations, and retrieval steps as child runs.

### Step 3: Build Custom Dashboard Metrics
Query the LangSmith API to extract key metrics: token usage per run, latency distributions (p50/p95/p99), error rates by error type, and cost per request. Build a Streamlit or notebook dashboard that visualizes these over time.

### Step 4: Create GitHub Actions Workflow
Write a `.github/workflows/agent-deploy.yml` that runs on push to main. Include steps for linting (`ruff`), unit tests (`pytest`), integration tests (run agent against test cases), and deployment.

### Step 5: Add Canary Deployment Strategy
Deploy new agent versions to 10% of traffic first. Compare canary metrics (latency, error rate, cost) against the stable version. Auto-promote to 100% if SLOs are met after 15 minutes, or auto-rollback if any SLO is violated.

### Step 6: Set Up Alerts
Configure alerts for SLO breaches: error rate > 5%, p99 latency > 10s, cost per request > $0.50. Send notifications via Slack webhook or email when thresholds are crossed.

## Key Concepts
- **Agent Observability:** Tracing every LLM call, tool invocation, and decision point so you can debug failures and understand agent behavior in production.
- **SLOs for Agents:** Service Level Objectives adapted for AI agents -- latency targets, error budgets, cost ceilings, and quality scores that define "healthy."
- **Canary Releases:** Deploying new agent versions to a small traffic slice first, comparing metrics against the stable version before full rollout.
- **CI/CD Pipelines:** Automated lint -> test -> deploy workflows that catch regressions before they reach production.
- **Cost Tracking:** Monitoring per-request cost (tokens * price) to prevent budget blowouts from prompt regressions or infinite loops.

## Resources
- [LangSmith Documentation](https://docs.smith.langchain.com/)
- [GitHub Actions Workflow Syntax](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
- [Canary Deployment Patterns](https://martinfowler.com/bliki/CanaryRelease.html)
- [OpenTelemetry for LLM Observability](https://opentelemetry.io/)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-20/README.md) | [Home](../../README.md) | [Next >](../day-22/README.md)
