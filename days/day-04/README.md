# Day 4: RAG Agents

> **Week 1: Foundations & First Agents**

## Overview
Today you'll build a retrieval-augmented generation agent that can answer questions over a corpus of PDF documents. You'll go beyond naive RAG by adding Cohere reranking and implementing agentic RAG -- where the agent can iteratively refine its queries, decide when it needs more information, and self-correct when retrieved context is insufficient.

## Learning Objectives
- [ ] Load and chunk PDF documents using multiple chunking strategies
- [ ] Embed chunks with OpenAI and store them in ChromaDB
- [ ] Implement a retrieval pipeline with hybrid search (semantic + keyword)
- [ ] Add Cohere reranking to improve retrieval precision
- [ ] Build an agentic RAG loop where the agent self-corrects queries and decides when to stop

## What You'll Build
A RAG agent that ingests a folder of PDFs, chunks and embeds them, retrieves relevant passages with reranking, and uses an agentic loop to refine queries when initial results are insufficient -- all producing grounded, cited answers.

## Prerequisites
- Completed Days 1-3
- `pip install openai chromadb cohere pypdf pydantic`
- OpenAI API key + Cohere API key (free tier works)
- 3-5 PDF documents to test with (research papers, documentation, etc.)

## Steps

### Step 1: Load and Chunk PDFs
Use `pypdf` to extract text from PDF files. Implement three chunking strategies: (1) fixed-size chunks (512 tokens with 50-token overlap), (2) recursive character splitting (split on `\n\n`, then `\n`, then `. `, then ` `), (3) semantic chunking (embed sentences, group by similarity). Compare output quality from each strategy on your documents.

### Step 2: Embed and Store in ChromaDB
Embed each chunk using `text-embedding-3-small`. Store in ChromaDB with metadata: `{source_file, page_number, chunk_index, chunk_method}`. Create a persistent collection so you don't re-embed on every run. Implement a simple deduplication check using document IDs based on content hashes.

### Step 3: Implement Retrieval with Hybrid Search
Build a `retrieve(query, k=10)` function that: (1) does semantic search via ChromaDB's embedding similarity, (2) does keyword search using ChromaDB's `where_document` filter with `$contains`, (3) merges results using reciprocal rank fusion (RRF). Return the top-k unique chunks with their scores and metadata.

### Step 4: Add Cohere Reranking
Take the top-20 results from hybrid search and pass them through Cohere's `rerank` endpoint with the original query. This reranker uses a cross-encoder model that's far more accurate than embedding cosine similarity for relevance scoring. Keep the top-5 reranked results. Compare answer quality with and without reranking.

### Step 5: Build the Agentic RAG Loop
Instead of one-shot retrieval, build an agent that: (1) generates an initial search query from the user question, (2) retrieves and evaluates results, (3) if results are insufficient (the LLM says "I don't have enough information"), reformulates the query and searches again, (4) repeats up to 3 times, (5) generates a final answer with citations (`[Source: filename, p.X]`). Use a system prompt that instructs the model to be honest about uncertainty.

### Step 6: Evaluate Retrieval Quality
Create 10 question-answer pairs from your documents (questions you know the answer to). Run each through the pipeline and measure: (1) retrieval recall (did the right chunk appear in top-5?), (2) answer correctness (LLM-as-judge comparison to ground truth), (3) citation accuracy (does the cited source actually contain the answer?).

## Key Concepts
- **Chunking Strategies:** How you split documents dramatically affects retrieval quality. Too small = lost context; too large = diluted relevance. Overlap prevents information loss at boundaries.
- **Embeddings:** Dense vector representations of text that capture semantic meaning. Similar texts have similar embeddings, enabling semantic search beyond keyword matching.
- **Reranking:** A second-stage model that scores query-document pairs more accurately than embedding similarity. Cross-encoders see query and document together, enabling deeper relevance assessment.
- **Agentic RAG:** The agent controls the retrieval process -- deciding what to search for, evaluating results, and iterating. This closes the gap between naive RAG and human research behavior.

## Resources
- [Cohere Rerank API docs](https://docs.cohere.com/reference/rerank)
- [ChromaDB querying guide](https://docs.trychroma.com/guides/querying)
- [Reciprocal Rank Fusion explained](https://plg.uwaterloo.ca/~gvcormac/cormacksigir09-rrf.pdf)
- [Self-RAG: Learning to Retrieve, Generate, and Critique](https://arxiv.org/abs/2310.11511)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-03/README.md) | [Home](../../README.md) | [Next >](../day-05/README.md)
