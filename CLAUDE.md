# 30 Days of AI Agents

## Project Overview
A 30-day challenge building AI agents from foundations to production. Published on CloudYeti (YouTube) and Udemy.

## Structure
- `days/day-NN/` - Daily builds (01-29, excluding milestones)
- `capstones/day-0N0-codename/` - 3 milestone projects (Days 10, 20, 30)
- `diagrams/` - Architecture diagrams
- `assets/` - Cheatsheets, templates

## Day File Format
Each day folder contains:
- `README.md` - Topic, learning objectives, step-by-step instructions
- `starter/` - Starting code for learners to complete
- `solution/` - Complete working solution
- `tests/` - pytest tests to validate the solution

## Conventions
- Python 3.12+ for most days, TypeScript for MCP server days
- All code must include type hints
- Every solution must have at least 1 passing test
- Day numbering: 2-digit zero-padded (day-01, day-02... day-29)
- Capstone naming: `day-0N0-codename` (lowercase, hyphenated)

## Frameworks Covered
LangGraph, CrewAI, OpenAI Agents SDK, Claude Agent SDK, Google ADK, n8n

## Protocols Covered
MCP (Model Context Protocol), A2A (Agent-to-Agent)

## Key Rules
- Every day has a hands-on build (no theory-only days)
- Days 10, 20, 30 are milestone capstone projects
- Cost for learners should stay under $15 total (use free tiers, Ollama for local)
- All API keys go in .env (never committed)
- Each day is dense: 1 day here = what was 3 days in the 100-day version
