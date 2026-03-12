# Day 16: Framework Showdown

> **Week 3: Multi-Agent & Production**

## Overview
With multiple agent frameworks under your belt, it's time for a head-to-head comparison. You'll implement the exact same task — analyzing a GitHub repository and generating a structured report — in LangGraph, CrewAI, and the OpenAI Agents SDK. Then you'll benchmark each on latency, token usage, cost, and developer experience to build a data-driven decision matrix.

## Learning Objectives
- [ ] Implement an identical agent task across three different frameworks
- [ ] Benchmark and compare frameworks on latency, token cost, lines of code, and output quality
- [ ] Build a decision matrix for choosing the right framework for different use cases

## What You'll Build
Three implementations of a "GitHub Repo Analyzer" agent that clones a repo, analyzes its structure/code/docs, and produces a structured report — one each in LangGraph, CrewAI, and OpenAI Agents SDK. Plus a benchmarking harness that runs all three and generates a comparison report with metrics.

## Prerequisites
- Days 11-14 completed (LangGraph, CrewAI, Claude/OpenAI SDK experience)
- GitHub personal access token
- OpenAI and Anthropic API keys
- Python 3.11+

## Steps

### Step 1: Define the Task Specification
Write a precise task spec: given a GitHub repo URL, the agent must (1) fetch repo metadata via GitHub API, (2) analyze the directory structure, (3) read key files (README, package.json/pyproject.toml, main entry points), (4) produce a structured report with: summary, tech stack, architecture overview, code quality assessment, and suggestions. Define the expected output schema.

### Step 2: Implement in LangGraph
Build a StateGraph with nodes for `fetch_metadata`, `analyze_structure`, `read_files`, and `generate_report`. Wire edges sequentially. Use conditional edges to skip nodes if data is missing. Track total tokens and wall-clock time.

### Step 3: Implement in CrewAI
Define agents: `Repo Analyst` (fetches and understands structure), `Code Reviewer` (reads and assesses code), `Report Writer` (synthesizes findings). Create tasks with dependencies and run with a sequential process. Track the same metrics.

### Step 4: Implement in OpenAI Agents SDK
Build using the OpenAI Agents SDK with tools for GitHub API calls and file reading. Use a single agent with handoffs or a multi-agent setup. Track metrics identically.

### Step 5: Benchmark and Build Decision Matrix
Run all three against the same 3 repos (small, medium, large). Measure: wall-clock latency, total tokens (input + output), estimated cost, lines of code written, output quality (scored 1-10 manually). Build a comparison table and write up recommendations for when to use each.

## Key Concepts
- **Framework Tradeoffs:** Every framework optimizes for different things — LangGraph for control and observability, CrewAI for role-based simplicity, OpenAI SDK for minimal abstraction.
- **Latency vs Cost vs DX:** Faster frameworks may cost more tokens; simpler APIs may sacrifice flexibility. These tradeoffs matter in production.
- **Decision Matrix:** A structured comparison tool: rows = criteria (latency, cost, flexibility, learning curve, observability), columns = frameworks, cells = scores.
- **Benchmarking Agents:** Comparing agent frameworks requires controlling for the same task, same LLM, same tools, and same evaluation criteria.
- **When to Use Which:** LangGraph for complex stateful workflows; CrewAI for quick multi-agent prototypes; OpenAI SDK for lightweight, single-vendor stacks.

## Resources
- [LangGraph Docs](https://langchain-ai.github.io/langgraph/)
- [CrewAI Docs](https://docs.crewai.com/)
- [OpenAI Agents SDK](https://openai.github.io/openai-agents-python/)
- [GitHub REST API](https://docs.github.com/en/rest)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-15/README.md) | [Home](../../README.md) | [Next >](../day-17/README.md)
