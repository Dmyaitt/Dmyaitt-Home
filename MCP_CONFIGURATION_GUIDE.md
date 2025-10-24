# n8n MCP Server Configuration Guide

This guide explains how to set up and configure the n8n MCP (Model Context Protocol) server for Claude Code integration.

## Overview

The n8n MCP server enables Claude Code to interact with your n8n workflow automation platform through 41 specialized tools for workflow management, execution monitoring, and automation control.

## Prerequisites

✅ **All prerequisites are installed:**
- Node.js v22.20.0
- npm 10.9.3
- n8n-mcp@2.21.1 (globally installed)
- better-sqlite3@12.4.1 (for FTS5 support)

## Configuration Files

### 1. Project-Level Configuration

**File:** `.mcp.json` (in project root)

This file contains your MCP server configuration with API credentials. It should **NOT** be committed to git.

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "n8n-mcp",
      "args": [],
      "env": {
        "MCP_MODE": "stdio",
        "LOG_LEVEL": "error",
        "DISABLE_CONSOLE_OUTPUT": "true",
        "N8N_API_URL": "https://dmyaitt.app.n8n.cloud",
        "N8N_API_KEY": "your_actual_api_key"
      }
    }
  }
}
```

### 2. User-Level Configuration

**File:** `~/.config/claude-code/mcp.json`

Same format as project-level, applies to all Claude Code sessions for your user account.

### 3. Project Settings (Optional)

**File:** `.claude/settings.json`

Can also contain MCP server configurations that override or extend other settings.

## Setup Instructions

### Step 1: Clone the Configuration

```bash
# Copy the example configuration
cp .mcp.json.example .mcp.json

# Edit with your credentials
nano .mcp.json
```

### Step 2: Configure Your API Key

Replace `YOUR_API_KEY_HERE` with your actual n8n API key:

1. Go to your n8n instance: https://dmyaitt.app.n8n.cloud
2. Navigate to Settings → API Keys
3. Generate a new API key
4. Copy it to your `.mcp.json` file

### Step 3: Verify Installation

Test that n8n-mcp can start successfully:

```bash
# Set environment variables
export N8N_API_URL=https://dmyaitt.app.n8n.cloud
export N8N_API_KEY=your_api_key_here

# Test the server (should run without errors)
timeout 3 n8n-mcp 2>&1 | grep -E "(Successfully|health check|tools)"
```

You should see:
- ✅ Successfully initialized better-sqlite3 adapter
- ✅ MCP server initialized with 41 tools
- ✅ Database health check passed: 541 nodes loaded
- ✅ n8n Documentation MCP Server running on stdio transport

### Step 4: Restart Claude Code

**IMPORTANT:** MCP servers are loaded at startup. You must:

1. **Completely exit** Claude Code (not just end the conversation)
2. **Restart** the application
3. Wait for initialization to complete

### Step 5: Verify MCP Tools are Available

After restart, check if n8n tools are loaded:

```bash
# Look for n8n MCP tools in the environment
env | grep -i n8n

# Or check the Claude Code logs
tail -f /tmp/claude-code.log | grep -i mcp
```

Expected tools (41 total):
- `mcp__n8n__list_workflows`
- `mcp__n8n__execute_workflow`
- `mcp__n8n__get_workflow`
- `mcp__n8n__search_nodes`
- ... and 37 more

## Security Best Practices

### Git Ignore Configuration

The `.gitignore` file protects sensitive data:

```gitignore
# MCP Configuration with secrets
.mcp.json
.claude/settings.json

# Environment variables
.env
.env.local

# API Keys and credentials
*.key
*.pem
credentials.json
```

### Safe Sharing

To share your MCP configuration with team members:

1. ✅ **DO** commit `.mcp.json.example`
2. ✅ **DO** document the setup process
3. ❌ **DON'T** commit `.mcp.json` with real API keys
4. ❌ **DON'T** commit `.env` files

### Environment Variables (Alternative)

Instead of storing credentials in `.mcp.json`, you can use environment variables:

```bash
# Add to your ~/.bashrc or ~/.zshrc
export N8N_API_URL=https://dmyaitt.app.n8n.cloud
export N8N_API_KEY=your_api_key_here
```

Then reference in `.mcp.json`:
```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "n8n-mcp",
      "args": [],
      "env": {
        "MCP_MODE": "stdio",
        "N8N_API_URL": "${N8N_API_URL}",
        "N8N_API_KEY": "${N8N_API_KEY}"
      }
    }
  }
}
```

## Troubleshooting

### MCP Server Not Loading

**Problem:** n8n MCP tools not available after restart

**Solutions:**
1. Check configuration file exists: `cat ~/.config/claude-code/mcp.json`
2. Verify JSON syntax: `python3 -m json.tool < .mcp.json`
3. Test server manually: `timeout 3 n8n-mcp 2>&1`
4. Check Claude Code logs: `grep -i mcp /tmp/claude-code.log`

### Database Health Check Failed

**Problem:** `Error: no such module: fts5`

**Solution:** Install better-sqlite3 with native bindings:
```bash
npm install -g better-sqlite3
```

### API Connection Errors

**Problem:** 403 Forbidden or connection errors

**Solutions:**
1. Verify API key is correct and active
2. Check API URL is correct: `https://dmyaitt.app.n8n.cloud`
3. Test API manually:
```bash
curl -H "X-N8N-API-KEY: your_key" https://dmyaitt.app.n8n.cloud/api/v1/workflows
```

### Hosted Environment Limitations

If running in a managed/hosted Claude Code environment:
- User-level `~/.config/claude-code/mcp.json` may not be supported
- Project-level `.mcp.json` might be required
- Contact your administrator for MCP configuration options

## Available n8n MCP Tools

Once configured, Claude Code will have access to:

### Workflow Management
- Create, read, update, delete workflows
- List all workflows
- Search workflows by name or tag
- Activate/deactivate workflows

### Execution Management
- Execute workflows manually or with parameters
- Monitor workflow executions
- View execution history and logs
- Retry failed executions

### Node Documentation
- Search n8n nodes (541 available)
- Get detailed node documentation
- Browse node categories
- Find nodes by functionality

### Advanced Features
- Credential management
- Webhook configuration
- Template workflow browsing
- Workflow import/export

## Configuration History

- **2025-10-24:** Initial n8n MCP configuration
  - Installed n8n-mcp@2.21.1 globally
  - Installed better-sqlite3@12.4.1 for FTS5 support
  - Created project-level configuration
  - Set up security protections

## Support

For issues or questions:
- **Claude Code Docs:** https://docs.claude.com/en/docs/claude-code/mcp
- **n8n MCP GitHub:** https://github.com/czlonkowski/n8n-mcp
- **Project Issues:** See MCP_SETUP.md for additional context

## References

- Original setup: [MCP_SETUP.md](./MCP_SETUP.md)
- Example config: [.mcp.json.example](./.mcp.json.example)
- Environment template: [.env.example](./.env.example)
