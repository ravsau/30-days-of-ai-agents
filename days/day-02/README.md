# Day 2: Tool Use & Function Calling

> **Week 1: Foundations & First Agents**

## Overview
Today you'll master the native function calling mechanism in the OpenAI API, moving beyond the manual ReAct parsing from Day 1. You'll build a multi-tool agent with five distinct tools, learn to define proper JSON schemas for each, handle structured outputs with Pydantic validation, and understand the full lifecycle of a function call from schema definition to execution to response injection.

## Learning Objectives
- [ ] Define tool schemas using OpenAI's function calling format (JSON Schema)
- [ ] Implement the function calling loop: model requests a call, you execute it, feed back the result
- [ ] Build and integrate 5 tools: web search, calculator, file reader, file writer, and API caller
- [ ] Enforce structured outputs using `response_format` and Pydantic model validation
- [ ] Handle parallel tool calls and multi-turn tool conversations

## What You'll Build
A multi-tool agent that uses OpenAI's native function calling to dynamically select from 5 tools, validates all inputs and outputs with Pydantic, and can chain multiple tool calls in a single turn to answer complex questions.

## Prerequisites
- Completed Day 1 (ReAct agent)
- `pip install openai pydantic requests`
- OpenAI API key

## Steps

### Step 1: Define Tool Schemas
Create JSON Schema definitions for 5 tools using OpenAI's `tools` parameter format. Each tool needs: `name`, `description`, and `parameters` (with `type`, `properties`, `required`). Example: `search` takes `{"query": "string", "num_results": "integer"}`. Be precise in descriptions -- the model uses them to decide when to call each tool.

### Step 2: Implement the Five Tools
Build Python functions for each tool: (1) `web_search(query, num_results)` -- uses requests to hit a search API, (2) `calculate(expression)` -- evaluates math safely, (3) `read_file(filepath)` -- reads local files with error handling, (4) `write_file(filepath, content)` -- writes to disk, (5) `call_api(url, method, headers, body)` -- generic HTTP client. Create a `TOOL_MAP` dict mapping function names to callables.

### Step 3: Build the Function Calling Loop
Replace the ReAct regex parsing from Day 1 with OpenAI's native function calling. Send the `tools` parameter in the API call. When the response has `tool_calls` in the message, extract each call's `function.name` and `function.arguments` (JSON string -- parse it), execute the corresponding function from `TOOL_MAP`, and append a `tool` role message with the result. Loop until the model returns a regular `assistant` message with no tool calls.

### Step 4: Handle Parallel Tool Calls
OpenAI can return multiple `tool_calls` in a single response. Update your loop to handle this: iterate over all tool calls, execute each, and append all results before the next API call. Test with a prompt like "Read config.json and also search for the current weather in NYC" to verify parallel execution.

### Step 5: Add Pydantic Validation
Define Pydantic models for tool inputs (e.g., `SearchInput(query: str, num_results: int = 5)`) and use them to validate the parsed arguments before execution. For the final agent output, define a `AgentResponse(answer: str, confidence: float, sources: list[str])` Pydantic model and use `response_format` with a JSON schema to enforce structured output on the final response.

### Step 6: Test Edge Cases
Test: What happens when the model hallucinates a tool name that doesn't exist? When arguments fail Pydantic validation? When a tool raises an exception? Add error handling for each case -- return informative error messages back to the model so it can self-correct.

## Key Concepts
- **Function Calling:** The model outputs a structured JSON request to call a function rather than generating text. You execute the function and feed the result back. This is more reliable than parsing free-text tool calls.
- **Structured Outputs:** Using `response_format` with a JSON schema forces the model to return data in a specific shape, enabling reliable downstream processing.
- **Tool Schemas:** The JSON Schema definitions you provide are part of the prompt -- the model uses `description` fields to decide when and how to use each tool. Good descriptions are critical.
- **JSON Mode vs Function Calling:** JSON mode forces JSON output but doesn't specify structure; function calling defines exact schemas for tool interactions.

## Resources
- [OpenAI Function Calling docs](https://platform.openai.com/docs/guides/function-calling)
- [OpenAI Structured Outputs guide](https://platform.openai.com/docs/guides/structured-outputs)
- [Pydantic v2 documentation](https://docs.pydantic.dev/latest/)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-01/README.md) | [Home](../../README.md) | [Next >](../day-03/README.md)
