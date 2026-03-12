# Day 27: Enterprise Patterns

> **Week 4: Specialized Agents & Capstone**

## Overview
Production agents in enterprise environments need security, compliance, and governance guardrails. Today you'll build an enterprise agent layer with role-based access control for tools, a complete audit trail, PII detection and redaction middleware, and multi-tenant isolation so each customer's data and configuration stays separate.

## Learning Objectives
- [ ] Implement role-based access control (RBAC) for agent tools
- [ ] Build a comprehensive audit trail logging every agent action
- [ ] Add PII detection and redaction middleware
- [ ] Implement multi-tenant isolation with per-customer config and data separation

## What You'll Build
An enterprise agent middleware layer providing RBAC (admin agents get different tools than user agents), timestamped audit logging of every action, automatic PII redaction in inputs and outputs, and full multi-tenant isolation.

## Prerequisites
- Working agent from a previous day
- Python 3.11+ with `pydantic`, `presidio-analyzer`, `presidio-anonymizer`
- SQLite or Postgres for audit logs
- Understanding of basic security concepts

## Steps

### Step 1: Implement Role-Based Tool Access
Define roles (admin, analyst, user) with different tool permissions. Admin agents can access database write tools, user agents get read-only tools, analyst agents get data query tools. Build a middleware that intercepts tool calls and checks permissions before execution. Deny unauthorized calls with a clear error message.

### Step 2: Build Audit Trail Logger
Create an audit logger that records every agent action: timestamp, user_id, tenant_id, action_type (llm_call, tool_call, response), input (redacted), output (redacted), latency_ms, token_count, and cost. Store in a structured format (SQLite/Postgres). Make logs immutable and tamper-evident.

### Step 3: Add PII Redaction Middleware
Use Microsoft Presidio (or regex patterns) to detect PII in agent inputs and outputs: emails, phone numbers, SSNs, credit cards, names, addresses. Replace detected PII with tokens (`[EMAIL_1]`, `[PHONE_1]`). Log the redaction mapping separately for authorized recovery. Apply redaction before LLM calls and in audit logs.

### Step 4: Implement Tenant Isolation
Build a tenant context system: each request carries a `tenant_id`. Isolate data access (each tenant's vector store is separate), configuration (per-tenant system prompts, tool sets, model selection), and rate limits. Ensure one tenant cannot access another's data or configuration. Test isolation with cross-tenant queries.

## Key Concepts
- **RBAC for Agents:** Controlling which tools and data sources an agent can access based on the user's role. Prevents privilege escalation where a user tricks an agent into performing admin actions.
- **Audit Trails:** Immutable, timestamped logs of every agent action. Required for compliance (SOC 2, HIPAA, GDPR) and essential for debugging, cost attribution, and incident response.
- **PII Redaction:** Automatically detecting and masking personally identifiable information before it reaches the LLM or gets stored in logs. Reduces data breach risk and supports GDPR compliance.
- **Multi-Tenancy:** Isolating each customer's data, configuration, and agent behavior so a single deployment serves multiple organizations securely. Includes data isolation, config isolation, and rate limit isolation.
- **Compliance:** Meeting regulatory requirements (SOC 2, HIPAA, GDPR) through technical controls -- audit logs, access control, data protection, and tenant isolation.

## Resources
- [Microsoft Presidio (PII Detection)](https://github.com/microsoft/presidio)
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [SOC 2 Compliance for AI](https://www.vanta.com/resources/soc-2-compliance)
- [Multi-Tenant Architecture Patterns](https://docs.aws.amazon.com/wellarchitected/latest/saas-lens/multi-tenant-architecture.html)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-26/README.md) | [Home](../../README.md) | [Next >](../day-28/README.md)
