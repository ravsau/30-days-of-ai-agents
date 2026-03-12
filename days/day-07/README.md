# Day 7: Agent Evaluation & Testing

> **Week 1: Foundations & First Agents**

## Overview
Today you'll build an evaluation harness for AI agents -- the most underrated skill in agent engineering. You'll create a dataset of 20 test cases, implement an automated eval runner, add LLM-as-judge scoring, and track cost and latency metrics. Without evals, you're flying blind: every change to your agent is a guess. After today, every change is measurable.

## Learning Objectives
- [ ] Design an evaluation dataset with 20 diverse input/expected-output pairs
- [ ] Build an automated eval runner that executes test cases and captures outputs
- [ ] Implement LLM-as-judge scoring with rubric-based evaluation
- [ ] Track cost (tokens, dollars) and latency (time-to-first-token, total time) per task
- [ ] Generate a structured eval report with pass rates, scores, and regressions

## What You'll Build
An eval harness that runs 20 test cases against any agent, scores each output using an LLM judge, tracks cost and latency, and generates a JSON + markdown report -- reusable for any agent you build in this series.

## Prerequisites
- Completed Days 1-6 (bring your Day 1 or Day 2 agent for testing)
- `pip install openai tiktoken pandas tabulate time`
- OpenAI API key

## Steps

### Step 1: Design the Eval Dataset
Create `eval_dataset.json` with 20 test cases across categories: (1) 5 factual questions with verifiable answers, (2) 5 multi-step reasoning questions requiring tool use, (3) 5 edge cases (ambiguous queries, unanswerable questions, adversarial inputs), (4) 5 format-specific tasks (e.g., "respond in JSON", "list exactly 3 items"). Each case has: `id`, `input`, `expected_output`, `category`, `difficulty`, `required_tools`.

### Step 2: Build the Eval Runner
Create an `EvalRunner` class that: (1) loads the dataset, (2) for each test case, calls your agent function with the input, (3) captures the output, wall-clock time, and token usage (from the API response), (4) stores results in a list of `EvalResult` objects. Add retry logic for API failures and a progress bar. Run tests sequentially (not parallel) for consistent latency measurement.

### Step 3: Implement LLM-as-Judge Scoring
Build a `judge(input, expected, actual) -> Score` function that sends the triplet to `gpt-4o` with a scoring rubric: correctness (0-5), completeness (0-5), format compliance (0-5). Use a structured output schema to ensure the judge returns `{correctness: int, completeness: int, format: int, reasoning: str}`. Average the three dimensions for a final score per test case. Measure inter-rater reliability by running the judge 3 times and checking agreement.

### Step 4: Add Cost and Latency Tracking
For each test case, track: (1) input tokens, output tokens, total tokens, (2) estimated cost using OpenAI's pricing (define a `PRICING` dict per model), (3) wall-clock time (start to finish), (4) number of tool calls made, (5) number of LLM calls (loop iterations). Aggregate into: total cost for the eval suite, average cost per task, p50/p95 latency.

### Step 5: Generate the Eval Report
Build a `generate_report(results)` function that outputs: (1) a JSON file with all raw results, (2) a markdown summary with tables showing: overall pass rate (score >= 4/5), score distribution by category, cost breakdown, latency percentiles, and the 3 worst-performing test cases with analysis. Include a "regression" section that compares against a previous run if a baseline file exists.

### Step 6: Run and Iterate
Execute the full eval suite against your Day 2 agent. Analyze the report: Which categories perform worst? Are failures due to retrieval, reasoning, or tool use? Pick the 3 worst cases, hypothesize fixes, implement them, and re-run. Compare the two reports to verify improvement. This is the agent development loop.

## Key Concepts
- **Task Completion Rate:** The percentage of test cases where the agent produces a correct, complete answer. The single most important agent metric.
- **LLM-as-Judge:** Using a strong LLM to evaluate another LLM's output against a rubric. More scalable than human eval, but requires careful prompt engineering to avoid biases (position bias, verbosity bias).
- **Cost-per-Task:** Total API cost divided by number of tasks completed. Critical for production agents -- a 10x improvement in quality means nothing if cost goes from $0.01 to $5.00 per task.
- **Regression Testing:** Comparing eval results across agent versions to catch performance degradation. Always run evals before and after changes.

## Resources
- [OpenAI Evals framework](https://github.com/openai/evals)
- [Braintrust eval platform](https://www.braintrustdata.com/)
- [Judging LLM-as-a-Judge](https://arxiv.org/abs/2306.05685) -- the MT-Bench paper
- [Hamel Husain's eval guide](https://hamel.dev/blog/posts/evals/)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-06/README.md) | [Home](../../README.md) | [Next >](../day-08/README.md)
