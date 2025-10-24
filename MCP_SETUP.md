# n8n MCP Server Configuration

This document describes the n8n MCP (Model Context Protocol) server configuration that has been set up for this project.

## Configuration Details

**Server Name:** n8n-mcp

**Command:** npx n8n-mcp

**Environment Variables:**
- `MCP_MODE`: stdio
- `LOG_LEVEL`: error
- `DISABLE_CONSOLE_OUTPUT`: true
- `N8N_API_URL`: https://dmyaitt.app.n8n.cloud
- `N8N_API_KEY`: [Configured]

## Configuration Location

The MCP server configuration has been added to:
```
~/.config/claude-code/mcp.json
```

This is a user-level configuration that enables Claude Code to interact with your n8n instance.

## Usage

Once configured, Claude Code will automatically connect to the n8n MCP server and have access to the n8n API tools and resources.

To verify the server is running:
```bash
claude mcp list
```

## Date Configured

October 24, 2025
