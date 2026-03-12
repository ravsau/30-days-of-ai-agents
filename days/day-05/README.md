# Day 5: MCP - Model Context Protocol

> **Week 1: Foundations & First Agents**

## Overview
Today you'll learn the Model Context Protocol (MCP), an open standard for connecting AI models to external data sources and tools. You'll build a custom MCP server in Python that exposes a SQLite database as tools, then connect it to Claude Desktop and verify end-to-end tool discovery and execution. MCP is how the industry is standardizing the "tool layer" for agents.

## Learning Objectives
- [ ] Understand the MCP architecture: hosts, clients, servers, and transports
- [ ] Build a custom MCP server using the Python SDK with stdio transport
- [ ] Define and implement three tools: query_db, insert_record, list_tables
- [ ] Configure Claude Desktop to connect to your MCP server
- [ ] Test end-to-end tool discovery and execution through the MCP protocol

## What You'll Build
A Python MCP server that wraps a SQLite database, exposing it as three tools (query, insert, list_tables) via the MCP protocol. You'll connect it to Claude Desktop and interact with your database through natural language.

## Prerequisites
- Completed Days 1-4
- Python 3.10+
- `pip install mcp sqlite3` (sqlite3 is in the standard library)
- Claude Desktop installed (for testing the MCP connection)

## Steps

### Step 1: Understand MCP Architecture
Study the three-layer architecture: **Hosts** (Claude Desktop, IDEs) manage connections, **Clients** (inside hosts) maintain 1:1 sessions with servers, **Servers** (your code) expose tools/resources/prompts. Understand the two transports: **stdio** (local, subprocess-based -- what we'll use) and **SSE/Streamable HTTP** (remote, HTTP-based). Draw a diagram of how a tool call flows through all layers.

### Step 2: Set Up the MCP Server Skeleton
Install the MCP Python SDK: `pip install mcp`. Create `server.py` and initialize a FastMCP server instance. Define the server name and version. Set up the SQLite database with a sample schema (e.g., `products` table with id, name, price, category). Populate it with 10 sample rows.

### Step 3: Implement Three Tools
Define tools using the `@server.tool()` decorator: (1) `list_tables()` -- returns all table names in the database, (2) `query_db(sql: str)` -- executes a SELECT query and returns results as formatted text (with SQL injection protection -- only allow SELECT), (3) `insert_record(table: str, data: dict)` -- inserts a record with parameterized queries. Add clear docstrings -- MCP uses these as tool descriptions.

### Step 4: Add Resources and Prompts (Optional MCP Features)
Expose the database schema as an MCP **resource** using `@server.resource()` -- this lets the host read the schema without a tool call. Add an MCP **prompt** template that generates a data analysis prompt pre-filled with the schema. These demonstrate the full MCP capability set beyond just tools.

### Step 5: Configure Claude Desktop
Edit Claude Desktop's config file (`~/Library/Application Support/Claude/claude_desktop_config.json` on macOS). Add your server to the `mcpServers` section with the `command` set to `python` and `args` pointing to your `server.py`. Restart Claude Desktop. Verify the tools appear in the tool list (hammer icon).

### Step 6: Test End-to-End
In Claude Desktop, ask: "What tables are in the database?" (should trigger `list_tables`), "Show me all products under $50" (should trigger `query_db`), "Add a new product called Widget for $29.99 in the Gadgets category" (should trigger `insert_record`). Verify each tool call executes correctly and Claude uses the results in its responses.

## Key Concepts
- **MCP Hosts, Clients, Servers:** Hosts are applications (Claude Desktop, IDEs); clients maintain protocol sessions; servers expose capabilities. This separation enables any host to use any server.
- **Transports (stdio vs SSE):** stdio runs the server as a local subprocess (simple, secure); SSE/HTTP runs it as a remote service (scalable, shareable). Choose based on deployment needs.
- **Tool Discovery:** MCP servers advertise their tools at connection time. The host reads tool names, descriptions, and schemas dynamically -- no hardcoding required. This is the key advantage over bespoke integrations.
- **MCP Security Model:** Servers run with user-level permissions. The host shows tool calls for approval. Never expose destructive operations without confirmation. Treat MCP servers like any other code that accesses sensitive resources.

## Resources
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk)
- [Claude Desktop MCP guide](https://modelcontextprotocol.io/quickstart/user)
- [Building MCP Servers](https://modelcontextprotocol.io/quickstart/server)

## Notes
*Add your notes and learnings here...*

---
[< Previous](../day-04/README.md) | [Home](../../README.md) | [Next >](../day-06/README.md)
