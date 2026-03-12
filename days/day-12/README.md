# Day 12: LangGraph Advanced

> **Week 2: Framework Mastery**

## Overview
Today you'll push LangGraph into production territory with subgraphs, human-in-the-loop breakpoints, and streaming. You'll build a content approval pipeline where agents draft and refine content, but a human must approve before publication. Finally, you'll deploy to LangGraph Cloud and connect LangSmith for observability.

## Learning Objectives
- [ ] Compose complex workflows using subgraphs and parent graphs
- [ ] Implement human-in-the-loop patterns with `interrupt_before` breakpoints
- [ ] Stream agent outputs in real-time and deploy to LangGraph Platform

## What You'll Build
A content approval pipeline with a drafting subgraph (research + write) and a review subgraph (edit + fact-check), connected by a parent graph that inserts a human approval breakpoint between them. Deployed to LangGraph Cloud with LangSmith tracing enabled.

## Prerequisites
- Day 11 completed (LangGraph fundamentals)
- LangSmith account (free tier)
- LangGraph CLI (`pip install langgraph-cli`)

## Steps

### Step 1: Build Subgraphs
Create two independent subgraphs: a `drafting_graph` (research -> write nodes) and a `review_graph` (edit -> fact_check nodes). Each subgraph has its own state schema. Test each subgraph in isolation.

### Step 2: Compose with a Parent Graph
Build a parent `StateGraph` that calls the drafting subgraph, then the review subgraph. Map state between parent and child schemas using input/output transformations. Verify end-to-end flow works without interrupts.

### Step 3: Add Human-in-the-Loop Breakpoints
Add `interrupt_before=["review_graph"]` to the parent graph compilation. When execution reaches the review phase, it pauses and surfaces the draft for human inspection. Implement `graph.update_state()` to accept/reject/edit the draft before resuming.

### Step 4: Implement Streaming
Switch from `graph.invoke()` to `graph.stream()` with `stream_mode="updates"`. Stream node outputs as they complete. Add token-level streaming for LLM nodes using `astream_events` to show text generation in real-time.

### Step 5: Deploy to LangGraph Cloud
Create a `langgraph.json` config file. Use `langgraph up` to run locally, then deploy to LangGraph Cloud. Connect LangSmith for tracing. Test the deployed API with curl requests and verify traces appear in LangSmith.

## Key Concepts
- **Subgraphs:** Self-contained graphs that can be nested inside a parent graph, enabling modular and reusable workflow components.
- **Human-in-the-Loop:** Using `interrupt_before` or `interrupt_after` to pause graph execution at specific nodes, allowing human review before continuing.
- **Streaming:** Emitting partial results as nodes complete (`stream_mode="updates"`) or as tokens are generated (`astream_events`), enabling responsive UIs.
- **LangGraph Platform:** A deployment runtime for LangGraph applications providing API endpoints, persistent state, and task queues.
- **Composition:** Combining multiple subgraphs into a parent graph with state mapping between different schemas.

## Resources
- [LangGraph Human-in-the-Loop](https://langchain-ai.github.io/langgraph/how-tos/human_in_the_loop/breakpoints/)
- [LangGraph Subgraphs](https://langchain-ai.github.io/langgraph/how-tos/subgraph/)
- [LangGraph Cloud Deployment](https://langchain-ai.github.io/langgraph/cloud/quick_start/)
- [LangSmith](https://smith.langchain.com/)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-11/README.md) | [Home](../../README.md) | [Next >](../day-13/README.md)
