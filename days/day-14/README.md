# Day 14: Claude Agent SDK + Computer Use

> **Week 2: Framework Mastery**

## Overview
Anthropic's Claude offers two powerful agent capabilities: extended thinking for transparent multi-step reasoning, and computer use for direct browser/desktop automation. Today you'll build two agents — one that uses extended thinking to solve complex analytical problems with visible chain-of-thought, and another that controls a browser to automate web tasks via screenshots and mouse/keyboard actions.

## Learning Objectives
- [ ] Build an agent with extended thinking enabled for complex, multi-step reasoning tasks
- [ ] Implement computer use for browser automation with screenshot capture and action execution
- [ ] Understand tool_use message blocks and how Claude interleaves reasoning with actions

## What You'll Build
(1) An extended thinking agent that breaks down complex research questions, shows its reasoning chain, and uses tools to gather data before synthesizing an answer. (2) A computer use agent that opens a browser, navigates to a website, fills out a form, and extracts confirmation data — all via screenshot analysis and programmatic input.

## Prerequisites
- Anthropic API key with Claude 3.5 Sonnet or Claude 3.7 Sonnet access
- Python 3.11+
- Docker (for computer use sandbox)
- `anthropic` Python SDK

## Steps

### Step 1: Install SDK and Configure Extended Thinking
Install `anthropic`. Create a client and make a request with `thinking={"type": "enabled", "budget_tokens": 10000}`. Observe the `thinking` blocks in the response alongside `text` blocks. Parse and display the reasoning chain.

### Step 2: Build an Extended Thinking Agent with Tools
Define tools (web search, calculator, code execution). Implement the agent loop: send message -> check for `tool_use` blocks -> execute tools -> send results back. Extended thinking runs before each tool call, giving you visibility into why the agent chose each action.

### Step 3: Set Up Computer Use Environment
Pull the Anthropic computer use Docker container. Configure the sandbox with a browser, screen resolution, and API access. Understand the three computer use tools: `computer_20241022` (mouse/keyboard), `text_editor_20241022`, and `bash_20241022`.

### Step 4: Build a Browser Automation Agent
Send a task to Claude with computer use tools enabled. The agent takes a screenshot, analyzes the screen, decides on mouse clicks or keyboard input, and sends actions. Implement the loop: screenshot -> Claude analyzes -> action -> screenshot -> repeat until task complete.

### Step 5: Implement Form Filling Automation
Target a specific web form. The agent navigates to the URL, identifies form fields from screenshots, fills them with provided data, submits, and extracts the confirmation. Handle edge cases: pop-ups, loading states, CAPTCHA detection (graceful failure).

## Key Concepts
- **Extended Thinking:** Claude's ability to perform visible chain-of-thought reasoning before responding, controlled by a token budget. The thinking is returned in separate `thinking` blocks.
- **Computer Use:** Claude analyzes screenshots and generates mouse/keyboard actions to control a computer, enabling automation of any GUI-based task.
- **tool_use Blocks:** Structured message blocks where Claude requests to invoke a tool, containing the tool name and input parameters. The agent loop processes these and returns results.
- **Screenshot Analysis:** Claude receives base64-encoded screenshots and reasons about UI elements, text, layout, and interactive components to determine next actions.
- **Browser Automation Loop:** A cycle of capture (screenshot) -> analyze (Claude vision) -> act (mouse/keyboard) -> verify (next screenshot) that drives autonomous web interaction.

## Resources
- [Anthropic Claude SDK](https://docs.anthropic.com/en/docs/agents-and-tools/claude-agent-sdk)
- [Extended Thinking Documentation](https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking)
- [Computer Use Guide](https://docs.anthropic.com/en/docs/agents-and-tools/computer-use)
- [Computer Use Docker Setup](https://github.com/anthropics/anthropic-quickstarts/tree/main/computer-use-demo)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-13/README.md) | [Home](../../README.md) | [Next >](../day-15/README.md)
