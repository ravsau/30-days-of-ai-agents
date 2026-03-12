# Day 1: Agents vs Chatbots vs Copilots + Your First Agent

> **Week 1: Foundations & First Agents**

## Overview
Today you'll build a precise mental model for what separates an AI agent from a chatbot and a copilot, then prove it by classifying 10 real products and building a ReAct agent from scratch using the raw OpenAI API. By the end, you'll have a working agent that can autonomously decide when to search the web and when to calculate, looping until it has a final answer.

## Learning Objectives
- [ ] Articulate the taxonomy: chatbot vs copilot vs agent, with concrete criteria
- [ ] Classify 10 real-world AI products into the correct category with justification
- [ ] Implement a ReAct (Reason + Act) loop from scratch using the OpenAI Chat Completions API
- [ ] Wire up two tools (web search, calculator) and let the agent choose which to call
- [ ] Understand the Perceive-Reason-Act cycle that underpins all agentic systems

## What You'll Build
A ReAct agent in Python that takes a user question, reasons about what tool to use, executes the tool, observes the result, and loops until it can provide a final answer -- all without any framework, just raw API calls.

## Prerequisites
- Python 3.10+
- OpenAI API key with access to `gpt-4o`
- `pip install openai requests`
- Basic understanding of the OpenAI Chat Completions API

## Steps

### Step 1: Define the Taxonomy
Create a markdown table or Python dict that defines three categories -- **Chatbot**, **Copilot**, **Agent** -- along each axis: autonomy level, tool access, goal persistence, loop type (single-turn vs multi-step), and human-in-the-loop requirements. Use this as your classification rubric.

### Step 2: Classify 10 Real Products
Take these 10 products and classify each using your rubric: ChatGPT (free tier), GitHub Copilot, Devin, Claude with tool use, Siri, AutoGPT, Cursor Tab, Perplexity, Zapier AI Actions, OpenAI Assistants API. Write a one-sentence justification for each. Some products blur boundaries -- note where and why.

### Step 3: Implement the ReAct Prompt
Build the system prompt that instructs the LLM to follow the ReAct pattern: `Thought -> Action -> Observation -> ... -> Final Answer`. Define the exact format the model should output (e.g., `Action: search[query]` or `Action: calculate[expression]`). Parse the model's output with regex or string splitting to extract the action and input.

### Step 4: Build Two Tools
Implement `search(query: str) -> str` using the SerpAPI or a simple `requests.get` to DuckDuckGo's API. Implement `calculate(expression: str) -> str` using Python's `ast.literal_eval` or a safe math parser. Each tool takes a string input and returns a string result.

### Step 5: Wire the ReAct Loop
Write the main loop: (1) Send messages to OpenAI, (2) Parse the response for an Action, (3) Execute the tool, (4) Append the Observation to the message history, (5) Repeat until the model outputs `Final Answer:`. Add a max-iterations safeguard (e.g., 10 loops) to prevent runaway agents.

### Step 6: Test with Multi-Step Questions
Test with questions that require both tools: "What is the population of France divided by the population of Iceland?" (requires two searches, then a calculation). Verify the agent chains tool calls correctly.

## Key Concepts
- **Agent vs Chatbot vs Copilot:** Chatbots are single-turn Q&A; copilots augment human work in real-time; agents autonomously pursue goals across multiple steps with tool use and decision-making.
- **ReAct Pattern:** Interleaves reasoning traces (Thought) with actions (Action) and observations (Observation), allowing the LLM to plan, execute, and adapt in a loop.
- **Perceive-Reason-Act Loop:** The fundamental agent cycle -- perceive the environment (observations), reason about what to do next (LLM inference), act on the environment (tool calls), repeat.

## Resources
- [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) -- the original paper
- [OpenAI Chat Completions API docs](https://platform.openai.com/docs/guides/text-generation)
- [Building a ReAct Agent from Scratch](https://til.simonwillison.net/llms/python-react-pattern) -- Simon Willison's walkthrough

## Notes
*Add your notes and learnings here...*

---
[Home](../../README.md) | [Next >](../day-02/README.md)
