# 30 Days of AI Agents

> Build a new AI agent every day for 30 days. From zero to production multi-agent systems.

[![CloudYeti](https://img.shields.io/badge/YouTube-CloudYeti-red)](https://youtube.com/@cloudyeti)
[![Udemy](https://img.shields.io/badge/Udemy-AI%20Agent%20Engineering-purple)](https://udemy.com)
[![Discord](https://img.shields.io/badge/Discord-Agent%20Builders-blue)](https://discord.gg/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## What You'll Build

30 hands-on agent projects in 30 days. Every major framework, protocol, and production pattern.

**Frameworks:** LangGraph | CrewAI | OpenAI Agents SDK | Claude Agent SDK | Google ADK | n8n

**Protocols:** MCP (Model Context Protocol) | A2A (Agent-to-Agent)

**Cloud:** AWS Bedrock | Lambda | Step Functions

## Quick Start

```bash
git clone https://github.com/cloudyeti/30-days-of-ai-agents.git
cd 30-days-of-ai-agents
pip install -r requirements.txt
cp .env.example .env  # Add your API keys
```

## 30-Day Roadmap

### Week 1: Foundations & First Agents (Days 1-7)

*Go from zero to building real agents with tool use, memory, RAG, and MCP.*

| Day | Topic | What You Build | Code |
|-----|-------|----------------|------|
| 1 | Agents vs Chatbots vs Copilots | Classify 10 real products + build your first ReAct agent | [Code](days/day-01/) |
| 2 | Tool Use & Function Calling | Multi-tool agent: web search + calculator + file I/O | [Code](days/day-02/) |
| 3 | Memory Systems | Conversation agent with sliding window + vector memory | [Code](days/day-03/) |
| 4 | RAG Agents | RAG agent over PDF docs with ChromaDB + Cohere reranking | [Code](days/day-04/) |
| 5 | MCP: Model Context Protocol | Build a custom MCP server + connect Claude to your database | [Code](days/day-05/) |
| 6 | A2A: Agent-to-Agent Protocol | Two agents communicating via Google's A2A protocol | [Code](days/day-06/) |
| 7 | Agent Evaluation & Testing | Eval harness with 20 test cases + LLM-as-judge scoring | [Code](days/day-07/) |

### Week 2: Framework Mastery (Days 8-14)

*Build the same agent in every major framework. Know which to pick and why.*

| Day | Topic | What You Build | Code |
|-----|-------|----------------|------|
| 8 | OpenAI Agents SDK | Customer service system: triage -> billing -> tech support | [Code](days/day-08/) |
| 9 | OpenAI Guardrails & Tracing | Add PII detection + toxicity filters + tracing dashboard | [Code](days/day-09/) |
| **10** | **MILESTONE: YetiBot** | **Full ReAct agent from scratch: 5 tools, streaming, eval suite** | [Code](capstones/day-010-yetibot/) |
| 11 | LangGraph Fundamentals | Graph-based research -> write -> review cycle with state | [Code](days/day-11/) |
| 12 | LangGraph Advanced | Checkpointing + human-in-the-loop + subgraphs + deploy | [Code](days/day-12/) |
| 13 | CrewAI | Content creation crew: researcher + writer + editor + SEO | [Code](days/day-13/) |
| 14 | Claude Agent SDK + Computer Use | Extended thinking agent + browser automation agent | [Code](days/day-14/) |

### Week 3: Multi-Agent & Production (Days 15-21)

*Move from single agents to orchestrated systems. Ship to production.*

| Day | Topic | What You Build | Code |
|-----|-------|----------------|------|
| 15 | Google ADK + n8n (No-Code) | Gemini multimodal agent + zero-code Slack bot in n8n | [Code](days/day-15/) |
| 16 | Framework Showdown | Same task in LangGraph vs CrewAI vs OpenAI SDK - benchmark | [Code](days/day-16/) |
| 17 | Multi-Agent Orchestration | 4-agent supervisor: PM + designer + developer + QA | [Code](days/day-17/) |
| 18 | Agent Communication Patterns | Message passing vs shared state vs pub-sub + conflict resolution | [Code](days/day-18/) |
| 19 | Production Reliability | Retries, fallbacks, circuit breakers, model routing by cost | [Code](days/day-19/) |
| **20** | **MILESTONE: ResearchCrew** | **Multi-agent research system: crawl -> analyze -> synthesize -> report** | [Code](capstones/day-020-researchcrew/) |
| 21 | Observability & CI/CD | LangSmith dashboard + GitHub Actions pipeline + canary deploy | [Code](days/day-21/) |

### Week 4: Specialized Agents & Capstone (Days 22-30)

*Build agents for real jobs. Deploy on AWS. Ship the capstone.*

| Day | Topic | What You Build | Code |
|-----|-------|----------------|------|
| 22 | Coding Agent | GitHub issue -> code -> tests -> PR (autonomous) | [Code](days/day-22/) |
| 23 | Data Analysis Agent | NL-to-SQL + auto chart generation + insight extraction | [Code](days/day-23/) |
| 24 | Customer Service Agent | Knowledge base + escalation + CSAT tracking + personalization | [Code](days/day-24/) |
| 25 | Local & Edge Agents | 100% local agent with Ollama - no API keys, no cloud | [Code](days/day-25/) |
| 26 | AWS for AI Agents | Bedrock Agents + Lambda + Step Functions + DynamoDB | [Code](days/day-26/) |
| 27 | Enterprise Patterns | RBAC + audit trails + PII redaction + multi-tenancy | [Code](days/day-27/) |
| 28 | Agent Self-Improvement | Meta-agent that analyzes failures + rewrites its own prompts | [Code](days/day-28/) |
| 29 | Building an Agent Business | Package Day 24's CS agent as a SaaS product + pricing model | [Code](days/day-29/) |
| **30** | **MILESTONE: AgentForge** | **Full-stack agent platform: YAML config -> deploy -> monitor dashboard** | [Code](capstones/day-030-agentforge/) |

## 3 Milestone Projects

| Day | Codename | What It Is |
|-----|----------|-----------|
| 10 | **YetiBot** | Full ReAct agent from scratch with 5 tools, streaming UI, and eval suite |
| 20 | **ResearchCrew** | Multi-agent research pipeline: crawl, analyze, synthesize, write report |
| 30 | **AgentForge** | Production agent platform: YAML config -> deploy -> monitor (your portfolio piece) |

## Tech Stack

| Purpose | Tools |
|---------|-------|
| Language | Python 3.12+ (primary), TypeScript (MCP servers) |
| Frameworks | LangGraph, CrewAI, OpenAI Agents SDK, Claude Agent SDK, Google ADK |
| No-Code | n8n |
| Protocols | MCP, A2A |
| Vector DB | ChromaDB (free, local) |
| Observability | LangSmith |
| Cloud | AWS (Bedrock, Lambda, Step Functions, DynamoDB) |
| Local | Ollama |
| Testing | pytest, custom eval harnesses |

## Cost for Learners

| Tier | Cost | What You Get |
|------|------|-------------|
| Free | $0 | Ollama + free API tiers (all major providers offer free credits) |
| Recommended | ~$15 total | API usage across providers for all 30 days |
| Full Experience | ~$30 total | AWS deployment (Days 26-27) using free tier + minimal spend |

## Udemy Course

**"AI Agent Engineering: Build 30 Agents in 30 Days"**

The complete course with extended explanations, quizzes, assignments, and certificate. Built from the same projects but with deeper walkthroughs.

## Follow Along

- **YouTube:** [@CloudYeti](https://youtube.com/@cloudyeti) - free video for every day
- **Udemy:** Full course with quizzes & certificate
- **Discord:** Join Agent Builders community
- **Newsletter:** Weekly digest + bonus tips

## License

MIT - build whatever you want with this.

---

*Built by [CloudYeti](https://youtube.com/@cloudyeti). Star this repo if you're joining the challenge!*
