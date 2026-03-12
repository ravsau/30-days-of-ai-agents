# 30 Days of AI Agents - Comprehensive Plan

## Series Identity

**Repo Name:** `30-days-of-ai-agents`
**YouTube Playlist:** "30 Days of AI Agents"
**Udemy Course:** "AI Agent Engineering: Build 30 Agents in 30 Days"
**Hashtag:** #30DaysOfAIAgents
**Discord:** "Agent Builders"

### Why 30, Not 100
- Ship-or-kill in 14 days is the rule. 30 days is the max tolerable scope.
- Forces ruthless topic prioritization - only the highest-ROI days survive
- Audience retention: YouTube series lose 80%+ by day 30 regardless
- 1 tight Udemy course > 4 fragmented ones
- Completion > ambition. Finished series >> abandoned series.
- Revenue starts at Day 35, not Day 100+
- Can always do "30 Days of AI Agents: Advanced" as a sequel

### Why This Name
- "AI agents" outranks "agentic AI" 3:1 in search volume
- "30 days" is a proven challenge format (achievable, not overwhelming)
- Matches existing CloudYeti brand (100-days-of-genAI lineage)
- Clean, scannable, instantly understood

---

## Market Context (March 2026)

### Industry Signals
- AI agents market: $7.84B (2025) -> $52.62B by 2030 (46.3% CAGR)
- 40% of enterprise apps will have AI agents by end of 2026 (Gartner)
- 1,445% surge in multi-agent system inquiries
- MCP: 8M+ downloads, 5,800+ servers, industry standard
- A2A: Google's agent-to-agent protocol, almost zero YouTube content (first-mover)
- Every major coding tool shipped multi-agent in Feb 2026

### Competitor Analysis
- Top Udemy: "Complete Agentic AI Engineering" - 141K students, 4.7/5
- Gap: No course covers MCP + A2A + ALL frameworks in one place
- Gap: Very little A2A content on YouTube
- Gap: n8n crossover audience under-served
- Gap: AWS-specific agent deployment barely covered

### CloudYeti Advantages
- 14K subs, 1.3M views - existing audience
- 37K Udemy students - existing course buyers
- Deep AWS expertise - unique for agent deployment
- Content factory pipeline - can produce at scale

---

## Curriculum Architecture

### 4 Weeks, 3 Milestones, 30 Builds

```
Week 1 (Days 1-7):   Foundations & First Agents
Week 2 (Days 8-14):  Framework Mastery
Week 3 (Days 15-21): Multi-Agent & Production
Week 4 (Days 22-30): Specialized Agents & Capstone
```

### 3 Milestone Projects

| Day | Codename | What It Is |
|-----|----------|-----------|
| 10 | **YetiBot** | Full ReAct agent: 5 tools, streaming, eval suite |
| 20 | **ResearchCrew** | Multi-agent research pipeline: crawl -> analyze -> synthesize -> report |
| 30 | **AgentForge** | Full-stack agent platform: YAML config -> deploy -> monitor dashboard |

### Design Principles
- Every day has a hands-on build (no theory-only days)
- Each day is 1 YouTube video (12-20 min) + 1 Short
- Progressive: Day 1 anyone can follow, Day 30 is enterprise-grade
- Days are dense: what was 3 days in 100-day plan becomes 1 day here
- Each day produces a working artifact (code, agent, dashboard, or deployed system)

---

## Detailed Day-by-Day Plan

### WEEK 1: FOUNDATIONS & FIRST AGENTS (Days 1-7)

**Goal:** Go from "what's an agent?" to building real agents with tools, memory, RAG, and protocols.

---

**Day 1: Agents vs Chatbots vs Copilots + Your First Agent**
- Learning objective: Understand the agent landscape; build a working agent
- Build: Classify 10 real products (ChatGPT, Devin, Copilot, etc.) + build a ReAct agent with 2 tools
- Covers: Agent definition, ReAct pattern, Perceive-Reason-Act loop, LLM selection
- Viral hook: "Day 1: Is ChatGPT an Agent? (The answer will surprise you)"
- YouTube: 15 min | Short: "Most people can't tell agents from chatbots"

**Day 2: Tool Use & Function Calling**
- Learning objective: Master function calling across OpenAI, Anthropic, Google
- Build: Multi-tool agent with web search + calculator + file I/O + API calls
- Covers: Function calling, structured outputs, JSON mode, Pydantic validation, retry logic
- Viral hook: "Day 2: I Gave an AI Agent 5 Tools. Here's What It Did."
- YouTube: 15 min | Short: Speed build of 5-tool agent in 60 sec

**Day 3: Memory Systems**
- Learning objective: Understand all memory types; implement 3 memory patterns
- Build: Conversation agent with sliding window + vector long-term memory + user profile memory
- Covers: Buffer memory, summary memory, vector memory (ChromaDB), episodic vs semantic memory
- Viral hook: "Day 3: This Agent Remembers Everything (Even When You Don't)"
- YouTube: 15 min | Short: "Your agent forgets everything. Here's the fix."

**Day 4: RAG Agents**
- Learning objective: Build a production-quality RAG pipeline for agents
- Build: RAG agent over PDF documents with ChromaDB + Cohere reranking + iterative query refinement
- Covers: Chunking strategies, embedding models, hybrid search, reranking, agentic RAG (self-correcting retrieval)
- Viral hook: "Day 4: This Agent Reads 500 Pages in 3 Seconds"
- YouTube: 18 min | Short: RAG vs no-RAG accuracy comparison

**Day 5: MCP - Model Context Protocol**
- Learning objective: Understand MCP architecture; build a custom MCP server
- Build: Custom MCP server in Python that exposes a database as tools + connect to Claude Desktop
- Covers: MCP hosts/clients/servers/transports, tool discovery, SSE vs stdio, security
- Viral hook: "Day 5: MCP is the USB-C of AI (And Nobody Gets It Yet)"
- YouTube: 20 min | Short: "MCP in 60 seconds"
- **HIGH VIRAL POTENTIAL** - MCP has massive search volume, few quality tutorials

**Day 6: A2A - Agent-to-Agent Protocol**
- Learning objective: Understand Google's A2A protocol; build agent-to-agent communication
- Build: Two independent agents that discover each other via Agent Cards and delegate tasks via A2A
- Covers: Agent Cards, task lifecycle, streaming, MCP vs A2A comparison, hybrid MCP+A2A architecture
- Viral hook: "Day 6: Google's A2A Protocol - Why Every Developer Should Care"
- YouTube: 18 min | Short: "MCP vs A2A in 60 seconds"
- **FIRST-MOVER** - almost no A2A YouTube content exists

**Day 7: Agent Evaluation & Testing**
- Learning objective: Measure agent quality systematically
- Build: Eval harness with 20 test cases + LLM-as-judge scoring + cost/latency tracking
- Covers: Task completion metrics, accuracy, latency, cost-per-task, LLM-as-judge, regression testing
- Viral hook: "Day 7: Your Agent is Lying to You. Here's How to Catch It."
- YouTube: 15 min | Short: "3 metrics every agent builder must track"

---

### WEEK 2: FRAMEWORK MASTERY (Days 8-14)

**Goal:** Build agents in every major framework. Know which to pick for any use case.

---

**Day 8: OpenAI Agents SDK**
- Learning objective: Master OpenAI's agent framework (handoffs, tools, tracing)
- Build: Customer service system with triage agent -> billing agent -> tech support agent + handoffs
- Covers: Agent class, tool definitions, handoff patterns, built-in tracing, context management
- Viral hook: "Day 8: OpenAI Agents SDK - Build a Multi-Agent System in 20 Minutes"
- YouTube: 18 min | Short: "OpenAI just killed LangChain?" (provocative hook)

**Day 9: OpenAI Guardrails & Tracing**
- Learning objective: Make agents safe and debuggable
- Build: Add PII detection guardrail + toxicity filter + cost circuit breaker to Day 8's system + tracing dashboard
- Covers: Input/output guardrails, tripwire guardrails, custom spans, debugging agent failures
- Viral hook: "Day 9: My Agent Leaked PII. Here's How I Stopped It."
- YouTube: 15 min | Short: "This guardrail saved me from a data breach"

**Day 10: MILESTONE - YetiBot** (Capstone #1)
- Learning objective: Synthesize Week 1-2 into a complete agent system
- Build: Full ReAct agent from scratch with 5 tools (web search, calculator, file I/O, code execution, API calls), streaming UI, structured output, eval suite with 30 test cases
- Covers: Everything from Days 1-9 integrated into one polished system
- Viral hook: "Day 10: I Built YetiBot - A Complete AI Agent From Scratch"
- YouTube: 25 min (milestone episode) | Short: YetiBot demo reel

**Day 11: LangGraph Fundamentals**
- Learning objective: Master graph-based agent design (the fastest framework)
- Build: Research -> write -> review cycle with state management, conditional edges, persistence
- Covers: Nodes, edges, state schemas, conditional routing, checkpointing, time-travel debugging
- Viral hook: "Day 11: LangGraph - The Framework That Runs 3x Faster"
- YouTube: 18 min | Short: "LangGraph explained in 60 seconds"

**Day 12: LangGraph Advanced**
- Learning objective: Production LangGraph patterns
- Build: Content approval pipeline with human-in-the-loop breakpoints + subgraphs + LangGraph Cloud deploy
- Covers: Subgraphs, composition, human-in-the-loop, streaming, LangGraph Platform, LangSmith integration
- Viral hook: "Day 12: Deploying AI Agents to Production with LangGraph Cloud"
- YouTube: 20 min | Short: "Human-in-the-loop agents in 60 seconds"

**Day 13: CrewAI**
- Learning objective: Master role-based multi-agent orchestration
- Build: Content creation crew with 4 agents: researcher + writer + editor + SEO optimizer (hierarchical process)
- Covers: Crew, Agent, Task classes, sequential vs hierarchical processes, memory, delegation, flows
- Viral hook: "Day 13: 4 AI Agents Wrote This Blog Post (And It's Actually Good)"
- YouTube: 18 min | Short: CrewAI content pipeline speed demo

**Day 14: Claude Agent SDK + Computer Use**
- Learning objective: Master Anthropic's agent capabilities
- Build: (1) Extended thinking agent for complex multi-step reasoning + (2) Browser automation agent that fills forms and extracts data
- Covers: Claude Agent SDK, extended thinking, computer use, tool use, screenshot analysis
- Viral hook: "Day 14: I Let Claude Control My Browser (Computer Use Demo)"
- YouTube: 20 min | Short: Claude Computer Use browser automation clip
- **HIGH VIRAL POTENTIAL** - computer use demos are inherently shareable

---

### WEEK 3: MULTI-AGENT & PRODUCTION (Days 15-21)

**Goal:** Orchestrate multi-agent systems. Ship reliable agents to production.

---

**Day 15: Google ADK + n8n (No-Code Agents)**
- Learning objective: Cover the remaining two frameworks
- Build: (1) Gemini multimodal agent with image understanding via Google ADK + (2) Zero-code AI Slack bot in n8n that triages support tickets
- Covers: Google ADK agent types, Gemini multimodal, n8n AI nodes, visual agent building
- Viral hook: "Day 15: Build AI Agents Without Writing a Single Line of Code"
- YouTube: 18 min | Short: n8n Slack bot speed build
- **HIGH VIRAL POTENTIAL** - no-code has a massive, different audience

**Day 16: Framework Showdown**
- Learning objective: Know exactly which framework to pick for any use case
- Build: Same "analyze a GitHub repo and write a report" task in LangGraph vs CrewAI vs OpenAI SDK - benchmark latency, tokens, cost, code complexity
- Covers: Framework comparison, decision matrix, weighted scoring across 10 dimensions
- Viral hook: "Day 16: LangGraph vs CrewAI vs OpenAI SDK - I Built the Same Agent 3 Times"
- YouTube: 22 min | Short: "The winner is..." (cliff-hanger)
- **HIGHEST VIRAL POTENTIAL** - comparison videos outperform tutorials 3-5x

**Day 17: Multi-Agent Orchestration**
- Learning objective: Build and coordinate multi-agent systems
- Build: "Software company" simulator with 4 agents: PM (scopes task) -> designer (specs UI) -> developer (writes code) -> QA (tests)
- Covers: Supervisor pattern, peer-to-peer, hierarchical, dynamic agent spawning, shared state
- Viral hook: "Day 17: I Built a Software Company with AI Agents"
- YouTube: 20 min | Short: "4 agents, 1 feature, zero humans"
- **HIGHEST VIRAL POTENTIAL** - "AI replacing jobs" narratives drive massive engagement

**Day 18: Agent Communication & Conflict Resolution**
- Learning objective: Handle agent disagreements and complex coordination
- Build: Multi-agent debate system with voting, consensus, and arbiter patterns + distributed trace visualizer
- Covers: Message passing, pub-sub, conflict resolution, consensus algorithms, debugging multi-agent
- Viral hook: "Day 18: 3 AI Agents Argued for 10 Minutes. The Result Blew My Mind."
- YouTube: 18 min | Short: Agent argument highlight clip

**Day 19: Production Reliability & Cost Optimization**
- Learning objective: Make agents reliable and affordable
- Build: (1) Add retries + fallbacks + circuit breakers to Day 17's system + (2) Model router that picks GPT-4o-mini vs Claude Sonnet vs Ollama by task complexity
- Covers: Reliability patterns, chaos testing, token budgets, model routing, caching, cost tracking
- Viral hook: "Day 19: How I Cut My AI Agent Costs by 90%"
- YouTube: 18 min | Short: "Stop wasting money on GPT-4o"

**Day 20: MILESTONE - ResearchCrew** (Capstone #2)
- Learning objective: Build a complete multi-agent production system
- Build: Multi-agent research pipeline: web crawler agent -> content analyzer agent -> synthesizer agent -> report writer agent. Includes LangSmith observability, cost tracking, eval suite, FastAPI wrapper.
- Covers: Multi-agent orchestration, production patterns, observability, API deployment
- Viral hook: "Day 20: This AI Research Team Replaced 8 Hours of Work"
- YouTube: 25 min (milestone episode) | Short: ResearchCrew demo reel

**Day 21: Observability & CI/CD for Agents**
- Learning objective: Monitor and deploy agents like production software
- Build: LangSmith dashboard (tokens, latency p50/p95/p99, error rate, cost/request) + GitHub Actions pipeline (test + deploy with canary strategy)
- Covers: Agent metrics, SLOs, alerting, automated testing, deployment pipelines, canary releases
- Viral hook: "Day 21: My Agent Went Down at 3 AM. Here's What I Built."
- YouTube: 18 min | Short: "If you deploy agents without this, you're gambling"

---

### WEEK 4: SPECIALIZED AGENTS & CAPSTONE (Days 22-30)

**Goal:** Build agents for real-world use cases. Deploy on AWS. Ship the capstone.

---

**Day 22: Coding Agent**
- Learning objective: Build an autonomous coding agent
- Build: Agent that takes a GitHub issue, reads the codebase, writes code, generates tests, and opens a PR
- Covers: Code generation, test writing, Git integration, sandboxed execution, self-debugging
- Viral hook: "Day 22: I Built an AI Coding Agent (Better Than Copilot?)"
- YouTube: 20 min | Short: "This agent wrote its own tests"
- **HIGH VIRAL POTENTIAL** - coding agents are the hottest demo in tech

**Day 23: Data Analysis Agent**
- Learning objective: Build agents for data work
- Build: Agent that connects to Postgres, answers natural language questions via SQL, auto-generates charts, and writes insight summaries
- Covers: NL-to-SQL, chart generation (matplotlib/plotly), insight extraction, iterative refinement
- Viral hook: "Day 23: This Agent Replaced My Morning Data Review"
- YouTube: 18 min | Short: NL question -> SQL -> chart speed demo

**Day 24: Customer Service Agent**
- Learning objective: Build the most common enterprise agent
- Build: End-to-end CS agent with knowledge base search, intent classification, escalation to human, CSAT tracking, user personalization
- Covers: KB retrieval, intent routing, handoff patterns, satisfaction measurement, preference learning
- Viral hook: "Day 24: This Customer Service Agent Has a 94% Satisfaction Rate"
- YouTube: 20 min | Short: CS agent handling an escalation

**Day 25: Local & Edge Agents (No API Keys)**
- Learning objective: Run agents 100% locally for privacy and zero cost
- Build: Complete agent running on Ollama with local embedding model - no API keys, no cloud, no cost
- Covers: Ollama setup, local LLMs (Llama 3, Mistral, Qwen), local embeddings, privacy-first architecture
- Viral hook: "Day 25: Run AI Agents 100% Locally (Free Forever)"
- YouTube: 18 min | Short: "Zero API keys, zero cost, full agent"
- **HIGH VIRAL POTENTIAL** - privacy + free = powerful combination

**Day 26: AWS for AI Agents**
- Learning objective: Deploy agents on AWS using managed services
- Build: Agent deployed on AWS Bedrock + Lambda + Step Functions + DynamoDB with API Gateway frontend
- Covers: Bedrock Agents, Lambda functions for tools, Step Functions for orchestration, DynamoDB for state
- Viral hook: "Day 26: Deploy AI Agents on AWS (Bedrock + Lambda)"
- YouTube: 22 min | Short: AWS architecture diagram walkthrough
- **CLOUDYETI CORE AUDIENCE** - bridges agent series to existing AWS audience

**Day 27: Enterprise Patterns**
- Learning objective: Build agents that enterprises will actually buy
- Build: Enterprise agent layer with RBAC (admin vs restricted agents), audit trail logging, PII redaction, multi-tenancy
- Covers: Agent permissions, compliance, governance, data residency, SOC2 implications
- Viral hook: "Day 27: The Enterprise Agent Checklist (What Nobody Tells You)"
- YouTube: 18 min | Short: "Skip this and your enterprise deal is dead"

**Day 28: Agent Self-Improvement**
- Learning objective: Build agents that get better over time
- Build: Meta-agent that analyzes its own failure cases, identifies patterns, and rewrites its system prompt + tool descriptions
- Covers: Self-reflection, prompt optimization, A/B testing prompts, continuous improvement loops
- Viral hook: "Day 28: This Agent Rewrites Its Own Brain"
- YouTube: 18 min | Short: Before/after self-improvement comparison

**Day 29: Building an Agent Business**
- Learning objective: Package agents as products
- Build: Take Day 24's CS agent and package it: SaaS pricing model, Stripe billing, usage tracking, onboarding flow
- Covers: Agent-as-a-Service business model, pricing strategies, usage metering, API design
- Viral hook: "Day 29: How to Turn an AI Agent into a $10K/Month Business"
- YouTube: 18 min | Short: "The agent business model that works"

**Day 30: MILESTONE - AgentForge** (Capstone #3 - Grand Finale)
- Learning objective: Build a complete agent platform
- Build: Full-stack agent platform where users define agents in YAML config -> system deploys them to AWS -> monitoring dashboard shows real-time metrics
- Covers: Platform engineering, agent DSL design, automated deployment, monitoring, the full stack
- Viral hook: "Day 30: I Built an AI Agent Platform in 30 Days (Full Demo)"
- YouTube: 30 min (grand finale) | Short: AgentForge platform demo
- This is the **portfolio piece** that proves you can build production agent systems

---

## Distribution Strategy

### YouTube Content Calendar

**Publishing: Daily (Mon-Sun for 30 days)**

| Format | Frequency | Length | Purpose |
|--------|-----------|--------|---------|
| Long-form build video | Daily | 15-22 min | Core content, watch time, course funnel |
| YouTube Short | Daily | 30-90 sec | Reach, subs, algorithm fuel |

Total: 30 long-form + 30 Shorts in 30 days.

**Shorts categories:**
1. Hook clip from long-form (40%)
2. Speed build / result reveal (25%)
3. Framework comparison (20%)
4. Agent failure / surprise moment (15%)

### Social Media

**LinkedIn:** Daily post, 7:30 AM ET
- Hook -> what I built -> what surprised me -> CTA
- Target: 300 followers growth over 30 days

**Twitter/X:** Daily tweet/thread
- Build day thread (3-5 tweets)
- Engage with AI influencer tweets

**Reddit:** Days 10, 20, 30 (milestone posts only)
- r/MachineLearning, r/artificial, r/aws, r/ClaudeAI
- Genuine value posts, repo link in comments

### Community

**Discord: "Agent Builders"** (launch Day 1)
- Channels: #daily-builds, #show-your-agent, #help, #course-students
- Target: 300 members by Day 30

### Email List

**Target: 1,000 subscribers by Day 30**

Lead magnets:
1. Day 1: "AI Agents Toolkit Cheatsheet" (1-page PDF)
2. Day 15: "Framework Decision Matrix" poster
3. Day 30: "30 Agent Architectures" diagram pack

### Content Repurposing (1 Day = 5 Atoms)

| Atom | Time | Output |
|------|------|--------|
| Long-form YouTube | 60-90 min | Build walkthrough |
| YouTube Short | 15 min | Hook clip or speed build |
| LinkedIn post | 10 min | Text + screenshot |
| Twitter thread | 10 min | 3-5 tweets |
| GitHub commit | 10 min | Clean code + README update |
| **Total per day** | **~2 hrs** | **5 content atoms** |

**Total production: ~60 hours over 30 days = 2 hrs/day. Sustainable.**

---

## Monetization Ladder

### Free Tier (During the 30 Days)
| Asset | Revenue |
|-------|---------|
| YouTube (30 videos + 30 Shorts) | $500-1,500 (ad revenue) |
| GitHub repo (public) | $0 (credibility engine) |
| Email list | $0 (launch channel) |

### Paid Tier 1: Udemy Course (Ship by Day 35)

**"AI Agent Engineering: Build 30 Agents in 30 Days"**

| Detail | Value |
|--------|-------|
| Release | 5 days after series ends |
| Launch price | $14.99 |
| Regular price | $79.99 |
| Content | 30 video lessons, re-recorded with deeper walkthroughs + quizzes + assignments |
| Differentiator | Source code + starter templates + eval harnesses (not on YouTube) |

**Revenue model (conservative):**
- 3,000 students in first 6 months x $8 net = $24,000
- Upside: 5% of competitor's 141K demand = 7,000 students = $56,000

### Paid Tier 2: Maven Cohort (Ship at Day 45)

**"Agent Engineering Sprint" - 2-week live cohort**

| Detail | Value |
|--------|-------|
| Price | $299/seat |
| Size | 20-30 students |
| Format | 2x/week live sessions + async builds + code review |
| Revenue | 25 students x $299 = $7,475/cohort. Run 4/year = $30K |

### Paid Tier 3: Consulting (Starts around Day 20)

| Offering | Price |
|----------|-------|
| 1:1 Agent Architecture Review | $250/hr (min 2hr) |
| Agent Readiness Workshop | $2,500/half-day |
| Enterprise Implementation | $5,000-15,000/project |

### Total Revenue Projection (6 months from Day 1)

| Stream | Conservative | Upside |
|--------|-------------|--------|
| YouTube Ads | $1,000 | $3,000 |
| Udemy Course | $24,000 | $56,000 |
| Maven Cohorts | $15,000 | $30,000 |
| Consulting | $10,000 | $24,000 |
| **TOTAL** | **$50,000** | **$113,000** |

**60% of 100-day revenue in 1/3 the time. Better ROI.**

---

## Top 5 Viral Episodes

1. **Day 17: "I Built a Software Company with AI Agents"** - 300K-800K views
2. **Day 16: "LangGraph vs CrewAI vs OpenAI SDK - Same Agent, 3 Frameworks"** - 200K-500K
3. **Day 25: "Run AI Agents 100% Locally (Free Forever)"** - 200K-500K
4. **Day 5: "MCP is the USB-C of AI (And Nobody Gets It Yet)"** - 150K-400K
5. **Day 22: "I Built an AI Coding Agent (Better Than Copilot?)"** - 150K-400K

---

## Launch Strategy (10-Day Pre-Launch)

Tighter than 21 days. Move fast.

### Days -10 to -7: Seed
- LinkedIn post: AI agents authority piece (no series mention)
- Twitter thread: "AI agents landscape in 2026"
- YouTube Community poll: "What agent framework should I learn first?"
- Pre-record Days 1-5

### Days -7 to -3: Announce
- YouTube trailer: "I'm Building 30 AI Agents in 30 Days (Here's My Plan)"
- GitHub repo goes live with README + full roadmap
- Email blast to 37K Udemy students
- LinkedIn announcement tagging 5-10 AI people

### Days -3 to -1: Hype
- 3 countdown YouTube Shorts
- Launch lead magnet (Toolkit Cheatsheet)
- Discord opens
- Pre-record Days 6-7

### Day 1: Launch
- Long-form + Short simultaneously
- All social channels + email blast
- Engage with EVERY comment for 48 hours
- Pin comment: GitHub + Discord

---

## Growth Targets

| Metric | Day 10 | Day 20 | Day 30 |
|--------|--------|--------|--------|
| YouTube subs | +1K (15K) | +2K (16K) | +4K (18K) |
| GitHub stars | 200 | 500 | 1,000+ |
| Email list | 300 | 600 | 1,000+ |
| Discord | 100 | 200 | 300 |
| Udemy (post-Day 35) | - | - | 500 (first month) |

---

## Sequel Strategy

If 30 Days hits (>1K GitHub stars, >500 Udemy students in 30 days):

**"30 Days of AI Agents: Advanced"** (Sequel)
- Days 1-10: Agent fine-tuning, multimodal agents, long-running agents
- Days 11-20: Agent-to-agent ecosystems, simulation, self-improvement at scale
- Days 21-30: Enterprise at scale, agent marketplaces, Agent OS

**"30 Days of AI Agents: Enterprise"** (B2B version)
- Focus: compliance, RBAC, multi-tenancy, cloud deployment, ROI measurement
- Target: engineering managers, CTOs
- Price: $199 Udemy, $499 Maven

This turns one 30-day sprint into a franchise.

---

## Tech Stack

| Purpose | Tool |
|---------|------|
| Primary language | Python 3.12+ (90%), TypeScript (10%) |
| Frameworks | LangGraph, CrewAI, OpenAI Agents SDK, Claude Agent SDK, Google ADK |
| No-code | n8n |
| Protocols | MCP, A2A |
| Vector DB | ChromaDB (free, local) |
| Observability | LangSmith |
| Cloud | AWS (Bedrock, Lambda, Step Functions, DynamoDB) |
| Local | Ollama |
| Learner cost | $0 (free) to $30 (full experience) |

---

## Repo Structure

```
30-days-of-ai-agents/
├── README.md
├── PLAN.md
├── CLAUDE.md
├── LAUNCH-CHECKLIST.md
├── requirements.txt
├── .env.example
├── .gitignore
├── days/
│   ├── day-01/
│   │   ├── README.md          # Topic, objectives, step-by-step
│   │   ├── starter/           # Starting code (learner completes)
│   │   ├── solution/          # Complete solution
│   │   └── tests/             # pytest validation
│   ├── day-02/
│   │   └── ...
│   └── day-29/
├── capstones/
│   ├── day-010-yetibot/
│   ├── day-020-researchcrew/
│   └── day-030-agentforge/
├── diagrams/
│   ├── 00-series-roadmap.png
│   ├── 01-react-loop.png
│   ├── 02-mcp-architecture.png
│   ├── 03-multi-agent-topologies.png
│   └── 04-aws-agent-stack.png
├── assets/
│   ├── cheatsheets/
│   └── templates/
└── .github/
    └── workflows/
        └── test.yml
```

---

## Architecture Diagrams Needed

1. **Series Roadmap** - 4 weeks, 3 milestones, progression arc
2. **ReAct Agent Loop** - Perceive -> Reason -> Act -> Learn
3. **MCP Architecture** - Host, client, server, transport
4. **Multi-Agent Topologies** - Supervisor, peer-to-peer, hierarchical, swarm
5. **AWS Agent Stack** - Bedrock + Lambda + Step Functions + DynamoDB + API Gateway
