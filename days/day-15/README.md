# Day 15: Google ADK + n8n (No-Code Agents)

> **Week 3: Multi-Agent & Production**

## Overview
Not every agent needs to be built from scratch in code. Today you'll explore two ends of the spectrum: Google's Agent Development Kit (ADK) for building multimodal agents with Gemini, and n8n for creating AI agents with zero code via a visual workflow editor. You'll build a Gemini-powered image understanding agent and a Slack bot — without writing a line of backend code for the latter.

## Learning Objectives
- [ ] Build a multimodal AI agent using Google ADK with Gemini's vision and reasoning capabilities
- [ ] Create a zero-code AI agent workflow in n8n with Slack integration
- [ ] Evaluate when code-based vs no-code agent building is the right choice

## What You'll Build
(1) A Google ADK agent that accepts images, analyzes them with Gemini's multimodal capabilities, and answers questions about visual content. (2) A no-code Slack bot built entirely in n8n that listens for messages, routes them to an AI agent node, and responds with context-aware answers.

## Prerequisites
- Google Cloud account with Gemini API access
- Node.js 18+ (for n8n)
- Slack workspace with admin access (for bot creation)
- Python 3.11+ (for Google ADK)

## Steps

### Step 1: Install Google ADK and Configure Gemini
Install `google-adk`. Set up authentication with your Google Cloud project. Initialize an ADK agent with Gemini as the underlying model. Verify basic text completion works before adding multimodal capabilities.

### Step 2: Build a Multimodal Image Understanding Agent
Configure the agent to accept image inputs (file path or URL). Send an image with a question (e.g., "What objects are in this image and how are they arranged?"). Parse Gemini's structured response. Add tools for the agent to search for more context about identified objects.

### Step 3: Install and Launch n8n
Install n8n locally via `npx n8n` or Docker. Open the visual workflow editor at `localhost:5678`. Familiarize yourself with the node-based interface: triggers, actions, AI nodes, and connections.

### Step 4: Create the Slack Bot Workflow
Add a Slack Trigger node (listens for messages). Connect it to an AI Agent node configured with an LLM (OpenAI or Anthropic). Add a tool node (e.g., web search or calculator) that the AI agent can use. Connect the agent output to a Slack Send Message node. Deploy and test.

### Step 5: Test Both and Compare Approaches
Send test queries to both agents. Compare: development time, flexibility, customization depth, debugging experience, and deployment complexity. Document when you'd choose ADK (custom logic, multimodal, production scale) vs n8n (rapid prototyping, non-technical teams, integrations-heavy workflows).

## Key Concepts
- **Google ADK:** Google's framework for building AI agents with Gemini, supporting multimodal inputs (text, image, video, audio) and tool integration.
- **Gemini Multimodal:** Gemini natively processes images, video, and audio alongside text, enabling agents that understand visual and auditory context.
- **n8n AI Nodes:** Pre-built workflow nodes for AI agents, LLM calls, vector stores, and tool use — no code required.
- **Visual Agent Building:** Designing agent logic as connected nodes in a canvas rather than writing code, trading flexibility for speed.
- **No-Code Agents:** Agent systems built entirely through visual interfaces, ideal for integration-heavy workflows and non-engineering teams.

## Resources
- [Google ADK Documentation](https://google.github.io/adk-docs/)
- [Gemini API](https://ai.google.dev/gemini-api/docs)
- [n8n Documentation](https://docs.n8n.io/)
- [n8n AI Agent Node](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-14/README.md) | [Home](../../README.md) | [Next >](../day-16/README.md)
