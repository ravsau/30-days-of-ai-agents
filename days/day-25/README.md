# Day 25: Local & Edge Agents

> **Week 4: Specialized Agents & Capstone**

## Overview
Today you'll build a fully functional AI agent that runs 100% locally -- no API keys, no cloud calls, no cost per request. Using Ollama for local LLM inference and local embeddings, you'll create a privacy-first agent with tool calling, vector search, and a complete agentic pipeline that works entirely offline.

## Learning Objectives
- [ ] Install and configure Ollama for local LLM inference
- [ ] Implement tool calling with a local model (Llama 3 or Qwen)
- [ ] Set up local embeddings with nomic-embed-text
- [ ] Build a local ChromaDB vector store for RAG
- [ ] Create a complete agent pipeline that works fully offline

## What You'll Build
A complete AI agent running on Ollama with local tool calling, local embeddings via nomic-embed-text, and a local ChromaDB vector store -- zero cloud dependencies, zero API costs, full data privacy.

## Prerequisites
- Machine with 16GB+ RAM (8GB minimum for smaller models)
- [Ollama installed](https://ollama.com/download)
- Python 3.11+ with `ollama`, `chromadb`, `langchain-community`
- ~5GB disk space for models

## Steps

### Step 1: Install Ollama and Pull Models
Install Ollama for your platform. Pull a capable model: `ollama pull llama3.1:8b` or `ollama pull qwen2.5:7b`. Verify it works with `ollama run llama3.1:8b "Hello"`. Check available models with `ollama list`.

### Step 2: Implement Tool Calling with Local LLM
Ollama supports structured tool calling with compatible models. Define tools as JSON schemas (calculator, web_search, file_reader). Send tool definitions in the chat request and parse the model's tool call responses. Handle the tool execution and feed results back.

### Step 3: Add Local Embeddings
Pull the embedding model: `ollama pull nomic-embed-text`. Use the Ollama embeddings API to generate vectors locally. Verify embedding quality by testing similarity between related and unrelated sentences.

### Step 4: Build Local ChromaDB Vector Store
Create a persistent ChromaDB collection using the local nomic-embed-text embeddings. Ingest sample documents (local files, notes, documentation). Implement semantic search with relevance filtering.

### Step 5: Create Full Agent Pipeline 100% Offline
Wire everything together: user query -> local LLM decides whether to search the vector store or use tools -> execute -> generate response. The entire pipeline must work with Wi-Fi disabled. Test by disconnecting from the internet and running end-to-end queries.

## Key Concepts
- **Ollama:** A local LLM runtime that runs open-weight models (Llama, Qwen, Mistral) on your machine with an OpenAI-compatible API, enabling cloud-free inference.
- **Local LLMs:** Open-weight models running on consumer hardware. Smaller (7-8B parameters) but fast, free, and private. Quality varies by model and task.
- **Local Embeddings:** Generating vector representations on-device using models like nomic-embed-text, eliminating the need for cloud embedding APIs.
- **Privacy-First Architecture:** Keeping all data and computation on-device -- critical for healthcare, legal, financial, and personal data use cases where data cannot leave the machine.
- **Edge Deployment:** Running AI agents on edge devices (laptops, servers, IoT) for low-latency, offline-capable, cost-free operation.

## Resources
- [Ollama Documentation](https://github.com/ollama/ollama)
- [Ollama Model Library](https://ollama.com/library)
- [Nomic Embed Text](https://ollama.com/library/nomic-embed-text)
- [ChromaDB with Custom Embeddings](https://docs.trychroma.com/docs/embeddings/custom-embeddings)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-24/README.md) | [Home](../../README.md) | [Next >](../day-26/README.md)
