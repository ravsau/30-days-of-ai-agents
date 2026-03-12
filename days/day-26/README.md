# Day 26: AWS for AI Agents

> **Week 4: Specialized Agents & Capstone**

## Overview
Today you'll deploy an AI agent on AWS using managed services: Bedrock for LLM inference, Lambda for tool functions, Step Functions for orchestration, DynamoDB for state and memory, and API Gateway for a REST endpoint. This is the cloud-native approach to production agent deployment.

## Learning Objectives
- [ ] Create a Bedrock agent with tool definitions (action groups)
- [ ] Implement Lambda functions for each agent tool
- [ ] Build Step Functions workflow for multi-step orchestration
- [ ] Use DynamoDB for conversation state and agent memory
- [ ] Expose the agent via API Gateway and test end-to-end

## What You'll Build
A serverless AI agent deployed on AWS: Bedrock handles LLM reasoning, Lambda functions execute tools, Step Functions orchestrates multi-step workflows, DynamoDB stores state and memory, and API Gateway provides a REST API -- all fully managed, auto-scaling, pay-per-use.

## Prerequisites
- AWS account with Bedrock model access enabled (Claude or Llama)
- AWS CLI configured with appropriate IAM permissions
- Python 3.11+ with `boto3`
- Basic familiarity with AWS Lambda and IAM roles
- [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html) (optional but recommended)

## Steps

### Step 1: Create Bedrock Agent with Tools
Enable model access in Bedrock (Claude 3 Haiku or Sonnet). Define action groups with OpenAPI schemas for your tools (e.g., lookup_order, check_inventory, send_notification). Create the Bedrock agent and attach the action groups.

### Step 2: Implement Lambda Functions for Each Tool
Write a Lambda function for each tool: `lookup_order` queries DynamoDB, `check_inventory` calls an external API, `send_notification` publishes to SNS. Package and deploy each function with the correct IAM role and permissions.

### Step 3: Build Step Functions Workflow
Create a Step Functions state machine that orchestrates a multi-step agent workflow: receive request -> invoke Bedrock agent -> execute tool calls -> check if more steps needed -> return response. Add error handling, retries, and timeout states.

### Step 4: Add DynamoDB for State and Memory
Create DynamoDB tables for conversation history (partition key: session_id, sort key: timestamp) and agent memory (partition key: user_id). Implement read/write operations in Lambda. Add TTL for automatic conversation cleanup.

### Step 5: Expose via API Gateway
Create a REST API in API Gateway with a POST endpoint. Connect it to the Step Functions state machine via a synchronous integration. Add API key authentication and usage plans. Configure CORS for web client access.

### Step 6: Test End-to-End
Send requests to the API Gateway endpoint and verify the full flow: API Gateway -> Step Functions -> Bedrock -> Lambda tools -> DynamoDB -> response. Test with multiple conversation turns to verify state persistence.

## Key Concepts
- **Bedrock Agents:** AWS's managed service for building agents with foundation models. Handles prompt engineering, tool routing, and response generation with built-in guardrails.
- **Lambda Tool Functions:** Serverless functions that execute agent tools. Each tool is an independent Lambda with its own IAM role, scaling, and error handling.
- **Step Functions Orchestration:** Visual workflow engine that coordinates multi-step agent execution with branching, retries, error handling, and parallel execution.
- **DynamoDB State:** NoSQL database for conversation history and agent memory. Single-digit millisecond reads, auto-scaling, and TTL for data lifecycle management.
- **API Gateway:** Managed API layer providing authentication, rate limiting, usage plans, and CORS -- the front door to your agent.

## Resources
- [AWS Bedrock Agents Documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html)
- [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [AWS Step Functions Developer Guide](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)
- [DynamoDB Best Practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-25/README.md) | [Home](../../README.md) | [Next >](../day-27/README.md)
