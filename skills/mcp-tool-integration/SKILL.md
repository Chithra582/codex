---
name: mcp-tool-integration
description: Use when bridging external Model Context Protocol (MCP) servers to extend Codex CLI with external tools, APIs, and resources.
---

# MCP Tool Integration

## Overview
Connects Codex CLI to the broader Model Context Protocol (MCP) ecosystem, enabling dynamic tool discovery and external data integration without recompilation.

## When to Use
- When integrating specialized databases, cloud platforms, or issue trackers (GitHub, Jira, Linear) into the coding loop.
- When querying custom internal developer APIs exposed as MCP endpoints.
- When reading external prompt templates or resource graphs dynamically.

## Core Capabilities
1. **Dynamic Tool Registration**: Enters external MCP tool schemas directly into Codex's active tool registry.
2. **Standardized Transports**: Supports stdio child processes and remote SSE transport channels.
3. **Transparent Execution**: Logs external tool calls and formats JSON-RPC results seamlessly into agent reasoning turns.
