# Day 3: Memory Systems

> **Week 1: Foundations & First Agents**

## Overview
Today you'll build a conversation agent with three tiers of memory: a sliding window buffer for short-term context, a ChromaDB vector store for long-term semantic retrieval, and a persistent user profile that accumulates facts about the user across sessions. You'll learn why memory is the single biggest differentiator between a toy demo and a production agent.

## Learning Objectives
- [ ] Implement sliding window buffer memory with configurable token limits
- [ ] Build a vector-based long-term memory system using ChromaDB and OpenAI embeddings
- [ ] Create a persistent user profile memory that extracts and stores user facts
- [ ] Combine all three memory tiers into a unified retrieval pipeline
- [ ] Understand the tradeoffs between episodic, semantic, and procedural memory

## What You'll Build
A conversational agent with 3-tier memory: (1) buffer memory that keeps the last N messages, (2) vector memory that stores and retrieves relevant past conversations, and (3) user profile memory that persists facts like name, preferences, and past requests across sessions in a JSON file.

## Prerequisites
- Completed Days 1-2
- `pip install openai chromadb tiktoken`
- OpenAI API key

## Steps

### Step 1: Implement Buffer Memory
Build a `BufferMemory` class that stores conversation messages in a list. Implement `add_message(role, content)` and `get_messages(max_tokens)`. Use `tiktoken` to count tokens and implement a sliding window: when total tokens exceed the limit, drop the oldest messages (but always keep the system prompt). Test that the window slides correctly as conversations grow.

### Step 2: Build Vector Long-Term Memory with ChromaDB
Create a `VectorMemory` class backed by ChromaDB. On every conversation turn, embed the user message + assistant response as a single document using OpenAI's `text-embedding-3-small`. Store it in a ChromaDB collection with metadata (timestamp, topic). Implement `search(query, k=5)` that retrieves the top-k most relevant past interactions. Use ChromaDB's persistent client so memory survives restarts.

### Step 3: Build User Profile Memory
Create a `ProfileMemory` class that maintains a JSON file with structured user information: `{name, preferences, past_topics, facts: []}`. After each conversation turn, send the exchange to a cheap model (gpt-4o-mini) with a prompt: "Extract any new facts about the user from this conversation. Return JSON or null." Merge extracted facts into the profile, deduplicating. Load the profile on startup and inject it into the system prompt.

### Step 4: Combine into a 3-Tier Memory System
Build a `MemoryManager` that orchestrates all three. On each user message: (1) query vector memory for relevant past context, (2) load user profile, (3) construct the full message list: system prompt + profile summary + retrieved memories + buffer window + current message. Pass this assembled context to the LLM. After the response, update all three memory stores.

### Step 5: Test Across Sessions
Run a multi-turn conversation where you tell the agent your name, preferences, and ask about a topic. End the session. Start a new session and verify: (1) the agent remembers your name (profile memory), (2) it can reference specific past conversations when relevant (vector memory), (3) the sliding window keeps recent context manageable (buffer memory).

## Key Concepts
- **Buffer Memory:** The simplest form -- a sliding window of recent messages. Fast but limited by context window size. Essential for maintaining conversation coherence.
- **Vector Memory:** Embeds past interactions as vectors and retrieves semantically similar ones. Enables long-term recall without consuming the entire context window.
- **Episodic vs Semantic Memory:** Episodic memory stores specific events ("you asked about X on Tuesday"); semantic memory stores general knowledge ("the user prefers Python over JavaScript"). Both matter for agents.
- **Context Window Management:** The core engineering challenge -- you have a finite context window and must decide what goes in it. Memory systems are fundamentally about intelligent context curation.

## Resources
- [ChromaDB documentation](https://docs.trychroma.com/)
- [OpenAI Embeddings guide](https://platform.openai.com/docs/guides/embeddings)
- [tiktoken tokenizer](https://github.com/openai/tiktoken)
- [Letta (MemGPT) paper](https://arxiv.org/abs/2310.08560) -- memory management for LLM agents

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-02/README.md) | [Home](../../README.md) | [Next >](../day-04/README.md)
