# Day 23: Data Analysis Agent

> **Week 4: Specialized Agents & Capstone**

## Overview
Today you'll build a data analysis agent that connects to a Postgres database, answers natural language questions by generating and executing SQL, automatically creates charts from the results, and writes plain-English insight summaries. The agent introspects the schema so it always generates valid queries.

## Learning Objectives
- [ ] Connect to Postgres and perform automatic schema introspection
- [ ] Implement natural language to SQL translation with query validation
- [ ] Auto-generate charts (bar, line, scatter, pie) from query results using matplotlib/plotly
- [ ] Extract and summarize insights in plain English
- [ ] Build an iterative refinement loop for failed or suboptimal queries

## What You'll Build
A conversational data analysis agent that takes questions like "What were our top 10 products by revenue last quarter?" and returns validated SQL, a rendered chart, and a written insight summary -- all from a live Postgres database.

## Prerequisites
- PostgreSQL database with sample data (or use the provided seed script)
- Python 3.11+ with `psycopg2`, `sqlalchemy`, `matplotlib`, `plotly`, `pandas`
- OpenAI or Anthropic API key
- Basic SQL knowledge

## Steps

### Step 1: Connect to Postgres with Schema Introspection
Use SQLAlchemy to connect to the database. Build a schema introspector that extracts table names, column names/types, primary keys, foreign keys, and sample rows. Format this as a compact schema reference the LLM can use.

### Step 2: Implement NL-to-SQL with Validation
Take a natural language question, combine it with the schema reference, and generate SQL. Validate the query before execution: check for syntax errors, ensure referenced tables/columns exist, reject destructive operations (DROP, DELETE, UPDATE). Use parameterized queries to prevent injection.

### Step 3: Add Chart Generation
Analyze query results to determine the best chart type (bar for comparisons, line for time series, pie for proportions, scatter for correlations). Generate the chart with matplotlib or plotly, including proper labels, titles, and formatting. Save as PNG or interactive HTML.

### Step 4: Build Insight Extraction
Feed the query results back to the LLM to generate a 2-3 sentence insight summary. Highlight key findings: trends, outliers, comparisons, and actionable takeaways. Include specific numbers from the data.

### Step 5: Create Iterative Refinement Loop
If a query fails (syntax error, timeout, empty results), capture the error and feed it back to the agent for correction. If results seem wrong (e.g., negative revenue), prompt the agent to verify and regenerate. Allow up to 3 refinement attempts before reporting the issue to the user.

## Key Concepts
- **NL-to-SQL:** Translating natural language questions into valid SQL by providing the LLM with schema context (table structures, relationships, sample data) so it generates accurate queries.
- **Schema-Aware Generation:** Introspecting the database schema at runtime so the agent always references real tables and columns, dramatically reducing hallucinated SQL.
- **Chart Generation:** Automatically selecting and rendering the appropriate visualization type based on the shape and semantics of the query results.
- **Insight Extraction:** Using an LLM to interpret raw query results and produce human-readable summaries that highlight what matters.
- **Iterative Refinement:** A feedback loop where failed queries are debugged and regenerated, mimicking how a human analyst would iterate on a query.

## Resources
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [Matplotlib Gallery](https://matplotlib.org/stable/gallery/)
- [Plotly Python Documentation](https://plotly.com/python/)
- [Text-to-SQL Research (BIRD Benchmark)](https://bird-bench.github.io/)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-22/README.md) | [Home](../../README.md) | [Next >](../day-24/README.md)
