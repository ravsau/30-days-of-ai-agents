# Day 20: MILESTONE - ResearchCrew

> **Week 3: Multi-Agent & Production**

## Overview
This is your Week 3 capstone: a production-grade multi-agent research system that combines everything you've learned. Four specialized agents — Web Crawler, Content Analyzer, Synthesizer, and Report Writer — work together in a pipeline to research any topic and produce a comprehensive, structured report. The system is wrapped in a FastAPI API, traced with LangSmith, and validated with an evaluation suite across 10 research topics.

## Learning Objectives
- [ ] Design and implement a 4-agent research pipeline with clear data flow between stages
- [ ] Wrap a multi-agent system in a production FastAPI service with async execution
- [ ] Add LangSmith observability and build an evaluation suite to measure research quality

## What You'll Build
ResearchCrew: a multi-agent research system with four pipeline stages (crawl -> analyze -> synthesize -> report), exposed via a FastAPI REST API, fully traced in LangSmith, and benchmarked against 10 diverse research topics with automated quality scoring. This is a complete, deployable research-as-a-service system.

## Prerequisites
- Days 11-19 completed (frameworks, multi-agent patterns, production reliability)
- OpenAI and/or Anthropic API keys
- LangSmith account
- Python 3.11+
- `pip install fastapi uvicorn langsmith langgraph crewai`

## Steps

### Step 1: Design the 4-Agent Pipeline
Map the data flow: `topic (string)` -> Crawler Agent (produces `raw_sources: list[Source]`) -> Analyzer Agent (produces `key_points: list[KeyPoint]`) -> Synthesizer Agent (produces `synthesis: Synthesis`) -> Report Writer Agent (produces `report: StructuredReport`). Define Pydantic models for each intermediate output.

### Step 2: Implement the Crawler Agent
Build the Web Crawler agent with tools: `web_search` (Tavily or SerpAPI), `web_scrape` (extract text from URLs), and `pdf_extract` (handle PDF sources). The agent searches for the topic, retrieves the top 5-10 sources, scrapes their content, and returns structured `Source` objects with URL, title, content, and credibility score.

### Step 3: Implement the Analyzer Agent
Build the Content Analyzer agent that receives raw sources and extracts key points. For each source, it identifies: main claims, supporting evidence, data points, quotes, and relevance score. It cross-references points across sources, flags contradictions, and produces a deduplicated list of `KeyPoint` objects.

### Step 4: Implement the Synthesizer Agent
Build the Synthesizer agent that receives key points and finds patterns: common themes, emerging trends, areas of consensus, points of disagreement, and knowledge gaps. It organizes findings into a coherent narrative structure and produces a `Synthesis` object with sections, connections, and confidence scores.

### Step 5: Implement the Report Writer Agent
Build the Report Writer agent that takes the synthesis and produces a final `StructuredReport` with: executive summary, methodology, findings (organized by theme), analysis, conclusions, limitations, and bibliography. Use structured output to ensure consistent formatting. The report should be publication-ready.

### Step 6: Wrap in FastAPI
Create a FastAPI application with endpoints: `POST /research` (accepts topic, returns job ID), `GET /research/{job_id}` (returns status and results), `GET /research/{job_id}/stream` (SSE stream of pipeline progress). Run the pipeline asynchronously with background tasks. Add input validation and error handling.

### Step 7: Add LangSmith Observability
Enable LangSmith tracing by setting `LANGCHAIN_TRACING_V2=true`. Add custom metadata tags for each agent stage. Verify traces appear in LangSmith with the full pipeline visible: each agent's inputs, outputs, token usage, and latency. Use traces to identify bottlenecks.

### Step 8: Build Evaluation Suite
Define 10 diverse research topics (e.g., "quantum computing applications in drug discovery", "impact of remote work on urban planning"). For each, run the full pipeline and score the output on: factual accuracy (manual spot-check), comprehensiveness (key points covered), coherence (logical flow), source quality (credible sources used), and report structure. Calculate aggregate scores and identify failure modes.

## Key Concepts
- **Multi-Agent Pipelines:** Sequential chains of specialized agents where each agent's output becomes the next agent's input, with typed contracts (Pydantic models) at each boundary.
- **Production Deployment:** Wrapping agent systems in web frameworks (FastAPI) with async execution, job queuing, status tracking, and streaming — making agents accessible as services.
- **Observability:** Using LangSmith (or similar) to trace every LLM call, tool invocation, and agent decision across the pipeline. Essential for debugging, optimization, and cost monitoring.
- **API Wrapping:** Exposing agent capabilities as REST endpoints with proper async patterns, background tasks, and streaming (SSE) for long-running operations.
- **Evaluation:** Systematically testing agent systems against diverse inputs and scoring outputs on multiple dimensions. The only way to know if your agents actually work reliably.
- **Structured Output:** Using Pydantic models and structured generation to ensure agents produce predictable, parseable outputs at each pipeline stage.

## Resources
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [LangSmith Documentation](https://docs.smith.langchain.com/)
- [LangGraph Multi-Agent Pipelines](https://langchain-ai.github.io/langgraph/tutorials/multi_agent/)
- [Pydantic Structured Output](https://docs.pydantic.dev/latest/)
- [Tavily Search API](https://tavily.com/)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../../days/day-19/README.md) | [Home](../../README.md) | [Next >](../../days/day-21/README.md)
