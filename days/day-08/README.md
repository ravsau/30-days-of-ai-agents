# Day 8: OpenAI Agents SDK

> **Week 2: Framework Mastery**

## Overview
Today you'll move from raw API calls to the OpenAI Agents SDK (formerly Swarm), a lightweight framework for building multi-agent systems. You'll build a customer service system where a triage agent routes requests to specialized billing and tech support agents using handoff patterns. The SDK handles the agent loop, tool execution, and handoff mechanics so you can focus on agent design.

## Learning Objectives
- [ ] Set up the OpenAI Agents SDK and understand its core abstractions (Agent, Runner, Tool)
- [ ] Define three specialized agents with distinct instructions, tools, and personalities
- [ ] Implement agent handoffs where one agent delegates to another
- [ ] Use the SDK's built-in tracing to observe agent execution flow
- [ ] Compare the SDK approach to the raw API approach from Days 1-2

## What You'll Build
A customer service multi-agent system with three agents: a Triage Agent that classifies incoming requests, a Billing Agent that handles payment and subscription issues, and a Tech Support Agent that troubleshoots technical problems -- all connected via handoffs.

## Prerequisites
- Completed Days 1-7
- `pip install openai-agents`
- OpenAI API key

## Steps

### Step 1: Install and Explore the SDK
Install `openai-agents` and explore the core classes: `Agent` (defines an agent with instructions, tools, and handoffs), `Runner` (executes the agent loop), `FunctionTool` (wraps a Python function as a tool), and `handoff()` (creates a handoff tool). Read the SDK source -- it's intentionally small (~500 lines of core logic). Understand how `Runner.run()` implements the same loop you built manually in Day 1.

### Step 2: Define the Billing Agent
Create an `Agent` with: `name="BillingAgent"`, `instructions` that describe its role (handle billing inquiries, check account status, process refunds), and two tools: `check_account_status(customer_id: str) -> str` (returns mock account data) and `process_refund(customer_id: str, amount: float, reason: str) -> str` (returns confirmation). Use `@function_tool` decorator to register them.

### Step 3: Define the Tech Support Agent
Create a second `Agent` with: `name="TechSupportAgent"`, instructions for handling technical issues, and two tools: `check_system_status(service: str) -> str` (returns mock service health data) and `create_ticket(customer_id: str, issue: str, priority: str) -> str` (creates a mock support ticket). Give it a different `model` parameter if you want to test with cheaper models for simpler tasks.

### Step 4: Define the Triage Agent with Handoffs
Create the `TriageAgent` with instructions to classify the customer's issue and route to the appropriate specialist. Use `handoff()` to define two handoff tools: one to the Billing Agent and one to the Tech Support Agent. The triage agent has no tools of its own -- its only job is to understand the request and decide which agent should handle it.

### Step 5: Run the Multi-Agent Flow
Use `Runner.run(triage_agent, messages)` to execute the system. Test with: (1) "I was charged twice for my subscription" (should route to Billing), (2) "The API is returning 500 errors" (should route to Tech Support), (3) "I need a refund and also my dashboard is broken" (should handle billing first, possibly hand back). Observe how the SDK manages the conversation state across handoffs.

### Step 6: Enable and Explore Tracing
The SDK includes built-in tracing. Enable it and run your test cases. Examine the trace output: see each agent's reasoning, tool calls, handoff decisions, and token usage. Identify the full execution path for a multi-handoff conversation. Export traces to JSON for later analysis. This is the observability layer you'd need to build from scratch without a framework.

## Key Concepts
- **Agent Class:** The SDK's core abstraction -- bundles instructions, model, tools, and handoffs into a single object. Think of it as a "role" that can be activated and deactivated.
- **Tool Definitions:** The `@function_tool` decorator inspects your Python function's signature and docstring to auto-generate the JSON schema. Type hints become parameter types; the docstring becomes the tool description.
- **Handoff Patterns:** A handoff transfers the conversation from one agent to another. The new agent gets the full conversation history and takes over. Handoffs can be one-way or round-trip (the target can hand back).
- **Built-in Tracing:** The SDK automatically traces every LLM call, tool execution, and handoff. This gives you observability without instrumenting your code -- essential for debugging multi-agent flows.

## Resources
- [OpenAI Agents SDK documentation](https://openai.github.io/openai-agents-python/)
- [Agents SDK GitHub repository](https://github.com/openai/openai-agents-python)
- [Agents SDK examples](https://github.com/openai/openai-agents-python/tree/main/examples)
- [Multi-agent patterns blog post](https://openai.com/index/new-tools-for-building-agents/)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-07/README.md) | [Home](../../README.md) | [Next >](../day-09/README.md)
