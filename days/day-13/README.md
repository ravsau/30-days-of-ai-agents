# Day 13: CrewAI

> **Week 2: Framework Mastery**

## Overview
CrewAI takes a role-based approach to multi-agent systems — you define agents with roles, goals, and backstories, then assemble them into a crew with a defined process. Today you'll build a content creation crew with four specialized agents working together through a hierarchical process with delegation and long-term memory.

## Learning Objectives
- [ ] Define CrewAI agents with distinct roles, goals, backstories, and tool assignments
- [ ] Create tasks with dependencies and expected outputs for structured workflows
- [ ] Configure hierarchical process execution with delegation and agent memory

## What You'll Build
A content creation crew with four agents — Researcher, Writer, Editor, and SEO Optimizer — that takes a topic and produces a polished, SEO-optimized article. The crew uses hierarchical process management with a manager agent delegating work and long-term memory for cross-session learning.

## Prerequisites
- Python 3.11+
- OpenAI API key (CrewAI default) or other LLM provider
- Basic understanding of multi-agent concepts from Week 1

## Steps

### Step 1: Install CrewAI and Set Up Project
Install `crewai` and `crewai-tools`. Use `crewai create crew content_crew` to scaffold a project. Configure your LLM provider in the environment.

### Step 2: Define Four Agents
Create agents with specific personas: a `Researcher` (goal: find accurate, comprehensive information), `Writer` (goal: create engaging long-form content), `Editor` (goal: ensure clarity, grammar, and flow), and `SEO Optimizer` (goal: maximize search visibility). Assign relevant tools (search, scrape) to each.

### Step 3: Create Tasks with Dependencies
Define tasks: `research_task` (output: research brief), `writing_task` (depends on research, output: draft article), `editing_task` (depends on writing, output: polished article), `seo_task` (depends on editing, output: final optimized article with meta tags). Set `expected_output` for each.

### Step 4: Configure Hierarchical Process
Set `process=Process.hierarchical` on the Crew, which creates a manager agent that delegates and coordinates. Compare with `Process.sequential` to understand the tradeoffs. Enable `memory=True` for long-term crew memory across runs.

### Step 5: Run the Crew and Analyze Output
Execute with `crew.kickoff(inputs={"topic": "..."})`. Observe the delegation chain, inter-agent communication, and final output. Review the task outputs at each stage and assess quality compared to a single-agent approach.

## Key Concepts
- **Agent:** An autonomous unit with a role, goal, backstory, and optional tools. The backstory shapes the agent's persona and decision-making style.
- **Task:** A unit of work assigned to an agent with a description, expected output, and optional dependencies on other tasks.
- **Crew:** A team of agents working together on a set of tasks with a defined process (sequential or hierarchical).
- **Sequential vs Hierarchical Process:** Sequential runs tasks in order; hierarchical adds a manager agent that dynamically delegates and coordinates.
- **Delegation:** In hierarchical mode, agents can delegate subtasks to other agents they deem better suited, enabling emergent collaboration.
- **Memory:** CrewAI supports short-term (within run), long-term (across runs), and entity memory for persistent knowledge.

## Resources
- [CrewAI Documentation](https://docs.crewai.com/)
- [CrewAI GitHub](https://github.com/crewAIInc/crewAI)
- [CrewAI Tools](https://docs.crewai.com/concepts/tools)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-12/README.md) | [Home](../../README.md) | [Next >](../day-14/README.md)
