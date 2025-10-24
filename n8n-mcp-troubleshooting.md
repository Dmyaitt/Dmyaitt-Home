# n8n-MCP Server Troubleshooting Guide

## Problem
MCP server "n8n-mcp" fails to connect with error: "Server disconnected"

## Root Causes Identified

### 1. Database Health Check Failure
- **better-sqlite3** native bindings not compiled when using `npx -y n8n-mcp`
- Falls back to **sql.js** which lacks FTS5 (Full-Text Search 5) support
- Health check expects FTS5, causing server crash with: `Error: no such module: fts5`

### 2. n8n Cloud API Issues
- API endpoint returns **403 Forbidden**
- Possible causes:
  - API key expired or incorrect
  - Insufficient permissions on the API key
  - n8n Cloud may have different authentication requirements

## Solutions

### Option 1: Use Docker (RECOMMENDED - Most Reliable)

Docker includes properly compiled binaries and avoids the sqlite3 binding issues.

**Update your Claude Code settings to:**
```json
{
  "n8n-mcp": {
    "command": "docker",
    "args": [
      "run",
      "-i",
      "--rm",
      "--init",
      "-e", "MCP_MODE=stdio",
      "-e", "LOG_LEVEL=error",
      "-e", "DISABLE_CONSOLE_OUTPUT=true",
      "-e", "N8N_API_URL=https://dmyaitt.app.n8n.cloud",
      "-e", "N8N_API_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiI5MzQ1MzUxZC0wYmYyLTQ0NmMtYjYyNi02OTI0MDY5Nzk0MDUiLCJpc3MiOiJuOG4iLCJhdWQiOiJwdWJsaWMtYXBpIiwiaWF0IjoxNzYxMjc1NzQyfQ.kRsX7x7v9OHaKV9tMn2xtFoav8TDIl0D-CWqxud4O4E",
      "ghcr.io/czlonkowski/n8n-mcp:latest"
    ]
  }
}
```

**Pull the Docker image first:**
```bash
docker pull ghcr.io/czlonkowski/n8n-mcp:latest
```

### Option 2: Use Basic Configuration (No n8n API)

If you only need n8n documentation tools and don't need to manage workflows via API, use the basic config:

```json
{
  "n8n-mcp": {
    "command": "npx",
    "args": ["-y", "n8n-mcp"],
    "env": {
      "MCP_MODE": "stdio",
      "LOG_LEVEL": "error",
      "DISABLE_CONSOLE_OUTPUT": "true"
    }
  }
}
```

**Note**: This still may have database issues with npx. Consider Docker instead.

### Option 3: Fix n8n API Authentication

The 403 error suggests authentication issues. To fix:

1. **Verify API Key**:
   - Go to your n8n Cloud instance: https://dmyaitt.app.n8n.cloud
   - Navigate to: Settings → API → API Keys
   - Check if your API key is still valid
   - Verify it has the necessary permissions

2. **Generate New API Key** (if needed):
   - Create a new API key with full permissions
   - Update the `N8N_API_KEY` in your MCP configuration

3. **Check API URL Format**:
   - Should be: `https://dmyaitt.app.n8n.cloud` (without `/api/v1`)
   - The n8n-mcp server adds the API path automatically

### Option 4: Use Globally Installed Version

I've already installed n8n-mcp globally on this system, which may work better:

```json
{
  "n8n-mcp": {
    "command": "n8n-mcp",
    "args": [],
    "env": {
      "MCP_MODE": "stdio",
      "LOG_LEVEL": "error",
      "DISABLE_CONSOLE_OUTPUT": "true",
      "N8N_API_URL": "https://dmyaitt.app.n8n.cloud",
      "N8N_API_KEY": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiI5MzQ1MzUxZC0wYmYyLTQ0NmMtYjYyNi02OTI0MDY5Nzk0MDUiLCJpc3MiOiJuOG4iLCJhdWQiOiJwdWJsaWMtYXBpIiwiaWF0IjoxNzYxMjc1NzQyfQ.kRsX7x7v9OHaKV9tMn2xtFoav8TDIl0D-CWqxud4O4E"
    }
  }
}
```

## Immediate Action Items

1. **FIRST**: Try the Docker solution (Option 1) - most reliable
2. **If Docker fails**: Check and regenerate your n8n API key
3. **If API issues persist**: Use basic configuration without API (Option 2)
4. **Alternative**: Use globally installed version (Option 4)

## Testing the Configuration

After updating your Claude Code settings:

1. Restart Claude Code
2. Try attaching to the n8n-mcp server
3. If it connects, test with: "Show me information about the HTTP Request node"
4. If it still fails, check Claude Code logs for detailed error messages

## Environment Variables Reference

- `MCP_MODE=stdio` - Required for Claude Code integration
- `LOG_LEVEL=error` - Reduce log verbosity (use `debug` for troubleshooting)
- `DISABLE_CONSOLE_OUTPUT=true` - Prevent console output issues
- `N8N_API_URL` - Your n8n instance URL (without /api/v1 suffix)
- `N8N_API_KEY` - Your n8n API key from Settings → API

## Additional Notes

- The n8n-mcp package version 2.21.1 is the latest (released 2025-10-23)
- The Docker image is optimized (82% smaller than typical n8n images)
- Documentation tools work even without n8n API credentials
- Management tools (create/update workflows) require valid API credentials
