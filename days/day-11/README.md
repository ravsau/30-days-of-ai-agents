# Day 11: LangGraph Fundamentals

> **Week 2: Framework Mastery**

## Overview
LangGraph brings graph-based orchestration to AI agents, giving you explicit control over state, routing, and execution flow. Today you'll learn how to model agent workflows as directed graphs with nodes, edges, and conditional branching. By the end, you'll have a research-write-review cycle that persists state across runs.

## Learning Objectives
- [ ] Understand the StateGraph abstraction and how it differs from chain-based orchestration
- [ ] Define typed state schemas, nodes, and conditional edges in LangGraph
- [ ] Implement checkpointing for persistent, resumable agent workflows

## What You'll Build
A graph-based research -> write -> review cycle where a research node gathers information, a write node drafts content, and a review node scores quality and conditionally loops back for revisions — all with persistent state via checkpointing.

## Prerequisites
- Python 3.11+
- OpenAI or Anthropic API key
- Completion of Days 1-10 (core agent patterns)
- Familiarity with async Python

## Steps

### Step 1: Install LangGraph and Define State Schema
Install `langgraph` and `langchain-openai`. Define a `TypedDict` state schema with fields for `topic`, `research_notes`, `draft`, `review_score`, and `revision_count`. This schema is the single source of truth flowing through your graph.

### Step 2: Build Graph Nodes
Create three node functions — `research_node` (calls a search tool and populates `research_notes`), `write_node` (generates a draft from research), and `review_node` (scores the draft 1-10 and provides feedback). Each node receives and returns the state dict.

### Step 3: Wire Edges and Conditional Routing
Build a `StateGraph` with your schema. Add nodes, then add edges: `research -> write -> review`. Add a conditional edge from `review` that routes back to `write` if `review_score < 7` (max 3 revisions), otherwise routes to `END`.

### Step 4: Add Checkpointing and Persistence
Attach a `MemorySaver` checkpointer to the compiled graph. Run the graph with a `thread_id` config so state persists between invocations. Verify you can resume a partially completed workflow from its last checkpoint.

### Step 5: Test and Observe
Run the full cycle on a sample topic. Print the state at each node transition. Observe how conditional edges trigger re-writes and how the revision count increments. Confirm checkpointing by interrupting and resuming mid-flow.

## Key Concepts
- **StateGraph:** A directed graph where nodes are functions and edges define execution order. State flows through the graph as a typed dictionary.
- **Nodes:** Python functions that receive the current state, perform work (LLM calls, tool use), and return state updates.
- **Conditional Edges:** Routing functions that inspect state and return the name of the next node, enabling dynamic branching and loops.
- **State Schema:** A `TypedDict` defining the shape of data flowing through the graph. Enforces structure and enables type checking.
- **Checkpointing:** Persisting graph state at each node boundary so workflows can be paused, resumed, or replayed.

## Resources
- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [LangGraph Quickstart](https://langchain-ai.github.io/langgraph/tutorials/introduction/)
- [State Management in LangGraph](https://langchain-ai.github.io/langgraph/concepts/low_level/#state)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-10/README.md) | [Home](../../README.md) | [Next >](../day-12/README.md)
