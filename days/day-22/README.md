# Day 22: Coding Agent

> **Week 4: Specialized Agents & Capstone**

## Overview
Today you'll build an autonomous coding agent that takes a GitHub issue as input, reads the relevant codebase, generates code changes with tests, and opens a pull request. The agent includes a self-debugging loop that runs tests, analyzes failures, fixes its own code, and retries until tests pass.

## Learning Objectives
- [ ] Build GitHub API integration for reading issues and creating PRs
- [ ] Implement intelligent codebase reading (file tree traversal + selective content loading)
- [ ] Generate context-aware code that follows existing project patterns
- [ ] Auto-generate unit tests for new code
- [ ] Build a self-debugging loop that runs tests, diagnoses failures, and fixes code

## What You'll Build
A coding agent that accepts a GitHub issue URL, explores the repository, writes implementation code with tests, runs them in a sandbox, self-debugs any failures, and opens a pull request with a clear description of changes.

## Prerequisites
- GitHub personal access token with repo scope
- Python 3.11+ with `PyGithub`, `openai` or `anthropic` SDK
- Docker (for sandboxed code execution)
- A test repository with open issues to work on

## Steps

### Step 1: Build GitHub API Integration
Use PyGithub to fetch issue details (title, body, labels, comments). Implement repo cloning and file tree listing. Build the PR creation function with title, body, branch, and diff.

### Step 2: Implement Codebase Reader
Create a smart file reader that builds a project map (directory tree, key files like `package.json`, `requirements.txt`, config files). Implement selective file loading based on issue context -- use embeddings or keyword matching to find relevant source files without loading the entire repo into context.

### Step 3: Add Code Generation with Context
Feed the agent: issue description + relevant source files + project conventions (linter config, existing patterns). Generate code changes as unified diffs or full file rewrites. Ensure the agent follows existing code style and import patterns.

### Step 4: Implement Test Writer
Analyze the generated code and existing test patterns. Auto-generate unit tests covering happy path, edge cases, and error handling. Place tests in the correct directory following project conventions.

### Step 5: Build PR Creator
Create a feature branch, commit changes, push to remote, and open a PR. Generate a PR description that references the issue, summarizes changes, and lists test coverage. Add appropriate labels and reviewers.

### Step 6: Add Self-Debugging Loop
Run the test suite in a Docker sandbox. If tests fail, capture stdout/stderr and traceback. Feed failures back to the agent for analysis and code fixes. Retry up to 3 times. If still failing, open the PR as draft with a note about remaining issues.

## Key Concepts
- **Code Generation:** Using LLMs to produce code that fits within an existing codebase's patterns, style, and architecture rather than generating code in isolation.
- **Test Generation:** Automatically creating unit tests by analyzing function signatures, docstrings, and existing test patterns in the project.
- **Sandboxed Execution:** Running generated code in a Docker container to prevent the agent from accidentally modifying the host system or executing dangerous commands.
- **Self-Debugging:** A feedback loop where the agent runs tests, reads failure output, diagnoses the root cause, and applies fixes autonomously.
- **Git Integration:** Programmatic branch creation, commits, and PR management -- treating Git operations as agent tools.

## Resources
- [PyGithub Documentation](https://pygithub.readthedocs.io/)
- [SWE-bench: Evaluating Coding Agents](https://www.swebench.com/)
- [OpenAI Codex / Code Generation Best Practices](https://platform.openai.com/docs/guides/code-generation)
- [Docker SDK for Python](https://docker-py.readthedocs.io/)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-21/README.md) | [Home](../../README.md) | [Next >](../day-23/README.md)
