# Day 10: MILESTONE - YetiBot

> **Week 2: Framework Mastery**

## Overview
This is your first capstone. You'll combine everything from Days 1-9 into YetiBot: a full ReAct agent built from scratch (no frameworks) with 5 tools, streaming terminal output, Pydantic structured responses, and a 30-test evaluation suite. This is your proof that you understand agent internals -- before you move to higher-level frameworks, you can build the whole stack yourself.

## Learning Objectives
- [ ] Architect a production-quality ReAct agent with clean separation of concerns
- [ ] Implement 5 tools with proper error handling, timeouts, and validation
- [ ] Build a streaming terminal UI that shows reasoning, tool calls, and results in real-time
- [ ] Enforce structured output schemas using Pydantic for reliable downstream processing
- [ ] Create a comprehensive 30-test eval suite and benchmark agent performance

## What You'll Build
YetiBot -- a complete ReAct agent with 5 tools (web search, calculator, file I/O, code execution, API calls), streaming terminal output with color-coded reasoning traces, Pydantic-validated structured responses, and a 30-case eval suite that measures accuracy, cost, and latency.

## Prerequisites
- Completed Days 1-9
- `pip install openai pydantic requests rich tiktoken`
- OpenAI API key
- All concepts from the first 9 days

## Steps

### Step 1: Design the Architecture
Plan YetiBot's module structure: `yetibot/agent.py` (ReAct loop), `yetibot/tools.py` (all 5 tools), `yetibot/memory.py` (conversation buffer), `yetibot/schemas.py` (Pydantic models), `yetibot/ui.py` (streaming terminal UI), `yetibot/config.py` (settings and API keys), `eval/runner.py` (eval harness), `eval/dataset.json` (30 test cases). Define clear interfaces between modules. Draw the data flow: user input -> agent loop -> tool execution -> streaming output.

### Step 2: Implement the ReAct Loop
Build the core agent loop in `agent.py` using raw OpenAI API calls (not the Agents SDK). The loop: (1) constructs messages with system prompt + conversation history, (2) calls OpenAI with `tools` parameter and `stream=True`, (3) parses tool calls from the streamed response, (4) executes tools, (5) appends results and loops, (6) terminates when the model produces a final response with no tool calls. Add a max-iterations limit (15) and a token budget (50,000 tokens per conversation).

### Step 3: Build 5 Tools with Production Patterns
Implement each tool with: input validation (Pydantic), timeout handling, error recovery, and structured return types. (1) **web_search(query, num_results)** -- SerpAPI or DuckDuckGo with result caching, (2) **calculate(expression)** -- safe math evaluation using `ast.literal_eval` (reject dangerous expressions), (3) **read_file(path) / write_file(path, content)** -- sandboxed to a `./workspace/` directory (path traversal protection), (4) **execute_code(language, code)** -- Python code execution in a subprocess with 10-second timeout and output capture, (5) **call_api(url, method, headers, body)** -- HTTP client with allowlist of domains, timeout, and response truncation.

### Step 4: Build Streaming Terminal UI
Use the `rich` library to build a live terminal UI. Display: (1) `[Thinking]` with the model's reasoning in dim gray, (2) `[Tool Call]` with the tool name and arguments in yellow, (3) `[Tool Result]` with the output in cyan (truncated to 500 chars), (4) `[Answer]` with the final response in bold white. Stream tokens as they arrive from the API. Add a token counter and cost estimate in the status bar. Use `rich.live.Live` for smooth updating.

### Step 5: Add Pydantic Output Schemas
Define structured output schemas for different query types: `FactualAnswer(answer: str, confidence: float, sources: list[str])`, `Comparison(items: list[str], criteria: list[str], matrix: dict, winner: str, reasoning: str)`, `StepByStep(steps: list[Step], final_result: str)`. The agent detects the query type and uses the appropriate schema in its final response via OpenAI's `response_format` parameter. Validate the parsed response against the Pydantic model.

### Step 6: Create the 30-Test Eval Suite
Build `eval/dataset.json` with 30 test cases across 6 categories (5 each): (1) factual lookup (require web_search), (2) math problems (require calculate), (3) file operations (require read/write), (4) code tasks (require execute_code), (5) API integration (require call_api), (6) multi-tool chains (require 2+ tools in sequence). Each case: `{id, input, expected_output, required_tools, category, difficulty}`. Build the eval runner from Day 7's harness, adding: tool-call accuracy (did it use the right tools?), step efficiency (how many loops?), and structured output compliance (did the response match the schema?).

### Step 7: Benchmark and Report
Run the full 30-test suite. Generate a report with: overall accuracy (target: >80%), accuracy by category, average cost per task, p50/p95 latency, tool usage patterns (which tools are called most?), failure analysis (why did failing tests fail?). Identify the top 3 failure modes and document potential fixes. Save the report as your baseline -- you'll compare against it when you rebuild YetiBot with frameworks later.

## Key Concepts
- **ReAct Architecture:** The agent alternates between reasoning (thinking about what to do) and acting (calling tools). This interleaving is what makes agents more capable than single-pass LLM calls -- they can plan, execute, observe, and adapt.
- **Tool Orchestration:** Managing multiple tools requires: consistent interfaces, error handling that feeds back to the model, input validation, security sandboxing, and timeout management. Each tool is a potential failure point.
- **Streaming:** Streaming tokens as they arrive makes agents feel responsive even when they take 30+ seconds. It also enables real-time debugging -- you can see the agent's reasoning before it finishes.
- **Evaluation as Engineering Practice:** The eval suite is not an afterthought -- it's the compass that guides agent development. Every design decision should be validated against evals. If you can't measure it, you can't improve it.

## Resources
- [ReAct paper](https://arxiv.org/abs/2210.03629)
- [Rich library documentation](https://rich.readthedocs.io/)
- [OpenAI Streaming guide](https://platform.openai.com/docs/guides/streaming)
- [Pydantic v2 documentation](https://docs.pydantic.dev/latest/)
- Days 1-9 of this series (your own code is the best reference)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../../days/day-09/README.md) | [Home](../../README.md) | [Next >](../../days/day-10/README.md)
