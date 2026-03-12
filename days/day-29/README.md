# Day 29: Building an Agent Business

> **Week 4: Specialized Agents & Capstone**

## Overview
Today you'll take Day 24's customer service agent and package it as a SaaS product. You'll add Stripe subscription billing, usage metering, a tenant onboarding flow, auto-generated API documentation, and rate limiting -- everything needed to sell an agent as a service.

## Learning Objectives
- [ ] Integrate Stripe for subscription billing with multiple tiers
- [ ] Implement usage metering (API calls, tokens consumed)
- [ ] Build a self-serve onboarding flow for new tenants
- [ ] Generate OpenAPI documentation for the agent API
- [ ] Add rate limiting per pricing tier

## What You'll Build
A SaaS-packaged version of the customer service agent from Day 24: Stripe billing with Free/Pro/Enterprise tiers, real-time usage metering, a self-serve onboarding flow, auto-generated API docs, and tier-based rate limiting.

## Prerequisites
- Day 24's customer service agent (or any working agent with an API)
- [Stripe account](https://stripe.com/) with test API keys
- Python 3.11+ with `stripe`, `fastapi`, `slowapi`
- Basic understanding of SaaS business models

## Steps

### Step 1: Add Stripe Integration
Create Stripe products and prices for three tiers: Free (100 requests/month, $0), Pro (10,000 requests/month, $49/month), Enterprise (unlimited, $299/month). Implement checkout session creation, webhook handling for subscription events (created, updated, canceled), and billing portal access.

### Step 2: Implement Usage Metering
Track per-tenant usage: API calls, tokens consumed (input + output), knowledge base queries, and escalations. Report usage to Stripe for metered billing on the Enterprise tier. Build a usage dashboard showing current period consumption vs. limits.

### Step 3: Build Onboarding Flow
Create a self-serve onboarding flow: sign up -> select plan -> Stripe checkout -> API key generation -> knowledge base upload -> first test query. Generate a unique API key per tenant. Provide a quickstart guide with curl examples.

### Step 4: Generate API Documentation
Use FastAPI's built-in OpenAPI generation to create comprehensive API docs. Document all endpoints: `/chat`, `/conversations`, `/usage`, `/billing`. Include request/response schemas, authentication (API key header), error codes, and rate limit headers. Host interactive docs at `/docs`.

### Step 5: Create Pricing Page
Build a simple pricing page (HTML or React) showing the three tiers, feature comparison table, and checkout buttons. Include: request limits, response time SLA, knowledge base size limits, support level, and custom branding options per tier.

### Step 6: Add Rate Limiting
Implement per-tenant rate limiting based on their subscription tier: Free (10 req/min), Pro (100 req/min), Enterprise (1000 req/min). Use `slowapi` or Redis-based rate limiting. Return proper 429 responses with `Retry-After` headers. Track rate limit hits in usage metrics.

## Key Concepts
- **Agent-as-a-Service:** Packaging an AI agent behind an API with authentication, billing, and usage tracking -- turning a technical project into a revenue-generating product.
- **Usage-Based Pricing:** Charging customers based on consumption (API calls, tokens) rather than flat fees. Aligns cost with value and scales revenue with usage.
- **Metering:** Tracking and recording resource consumption in real-time for billing, quota enforcement, and usage analytics.
- **API Design:** RESTful API design with proper authentication, versioning, error handling, rate limiting, and documentation -- the interface between your agent and paying customers.
- **SaaS Packaging:** The full stack of business infrastructure: billing, onboarding, documentation, support tiers, and usage dashboards that transform code into a product.

## Resources
- [Stripe API Documentation](https://stripe.com/docs/api)
- [Stripe Subscription Billing Guide](https://stripe.com/docs/billing/subscriptions/overview)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [SaaS Metrics That Matter](https://www.saastr.com/saastr-saastr-saas-metrics/)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-28/README.md) | [Home](../../README.md) | [Next >](../../capstones/day-030-agentforge/README.md)
