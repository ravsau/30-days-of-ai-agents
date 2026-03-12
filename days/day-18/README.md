# Day 18: Agent Communication & Conflict Resolution

> **Week 3: Multi-Agent & Production**

## Overview
When multiple agents collaborate, they need structured communication patterns and mechanisms to resolve disagreements. Today you'll build a multi-agent debate system where agents with different perspectives argue a topic, then reach consensus through voting, arbitration, and structured deliberation. You'll also build a trace visualizer to observe the communication flow.

## Learning Objectives
- [ ] Implement three communication patterns: message passing, shared-state blackboard, and pub-sub
- [ ] Build consensus mechanisms including voting, weighted scoring, and arbiter-based resolution
- [ ] Visualize multi-agent communication traces for debugging and analysis

## What You'll Build
A debate system where three agents (Optimist, Skeptic, Pragmatist) analyze a proposal from different angles, exchange arguments via structured communication, resolve conflicts through voting and an arbiter agent, and produce a final consensus report. Includes a trace visualizer that renders the full communication graph.

## Prerequisites
- Day 17 completed (multi-agent orchestration)
- Python 3.11+
- OpenAI or Anthropic API key

## Steps

### Step 1: Implement Message-Passing Communication
Build a message bus where agents send typed messages (`Argument`, `Rebuttal`, `Question`, `Concession`) to specific recipients. Each message has a sender, recipient, type, content, and timestamp. Agents maintain an inbox and process messages in order.

### Step 2: Build a Shared-State Blackboard
Create a blackboard (shared dict) where agents post findings, claims, and evidence. Any agent can read the full blackboard. Implement read/write locking to prevent conflicts. Compare with message passing: blackboard enables implicit coordination without direct addressing.

### Step 3: Add Pub-Sub Pattern
Implement a topic-based pub-sub system where agents subscribe to topics ("evidence", "counterarguments", "consensus_proposals") and publish to them. This decouples senders from receivers and enables flexible, extensible communication without hardcoded routing.

### Step 4: Implement Voting and Arbiter Conflict Resolution
After debate rounds, implement a voting mechanism: each agent scores proposals 1-10 with justification. If no clear winner (margin < 2), invoke an Arbiter agent that reviews all arguments, identifies the strongest evidence, and makes a binding decision with a written rationale.

### Step 5: Build the Trace Visualizer
Log every message, state change, and decision point with timestamps. Build a visualization (HTML or terminal-based) showing the communication flow: which agent spoke when, what type of message, how votes were cast, and where the arbiter intervened. This is essential for debugging multi-agent systems.

## Key Concepts
- **Message Passing:** Direct agent-to-agent communication via typed, structured messages. Explicit and traceable but requires knowing recipients.
- **Shared State (Blackboard):** A common data store all agents read/write. Enables implicit coordination but can create contention and ordering issues.
- **Pub-Sub:** Publish-subscribe pattern where agents emit events to topics and subscribe to relevant topics. Decoupled and extensible.
- **Consensus Algorithms:** Mechanisms for multiple agents to agree on a decision — voting, weighted scoring, supermajority rules, or delegated arbitration.
- **Conflict Resolution:** When agents disagree, structured processes (debate rounds, evidence weighing, arbiter review) produce reasoned outcomes rather than deadlocks.
- **Trace Visualization:** Rendering the full communication history of a multi-agent interaction as a timeline or graph for debugging and analysis.

## Resources
- [Multi-Agent Communication Patterns](https://arxiv.org/abs/2308.08155)
- [LangGraph Message Passing](https://langchain-ai.github.io/langgraph/how-tos/pass-private-state/)
- [Blackboard Architecture](https://en.wikipedia.org/wiki/Blackboard_(design_pattern))

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-17/README.md) | [Home](../../README.md) | [Next >](../day-19/README.md)
