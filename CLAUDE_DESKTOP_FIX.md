# Claude Desktop n8n-MCP Configuration Fix

This guide will help you fix the n8n-MCP errors in Claude Desktop after reinstallation.

## The Problem

After reinstalling Claude Desktop, the MCP server configuration for n8n-mcp is either missing or incorrectly configured, causing errors on startup.

## The Solution

### Step 1: Locate Your Claude Desktop Config Directory

The location depends on your operating system:

- **Windows**: `%APPDATA%\Claude\`
- **macOS**: `~/Library/Application Support/Claude/`
- **Linux**: `~/.config/Claude/`

### Step 2: Copy the Configuration File

1. Navigate to the Claude Desktop config directory identified in Step 1
2. Copy the `claude_desktop_config.json` file from this repository to that directory
3. If a `claude_desktop_config.json` file already exists, you have two options:
   - **Option A**: Replace it with the new file (backup the old one first!)
   - **Option B**: Merge the configurations by copying the "n8n-mcp" section into your existing config

### Step 3: Verify Your N8N API Key (Already Configured)

The `claude_desktop_config.json` file in this repository already has your n8n API key configured. No changes needed unless you want to update it.

If you need to update your API key in the future:
1. Open the `claude_desktop_config.json` file in the Claude Desktop config directory
2. Find the line: `"N8N_API_KEY": "..."`
3. Replace it with your new n8n API key from https://dmyaitt.app.n8n.cloud

To get a new API key:
- Log in to your n8n instance at https://dmyaitt.app.n8n.cloud
- Go to Settings → API
- Create or copy your API key

### Step 4: Ensure Node.js and npx are Installed

The n8n-mcp server requires Node.js to run. Make sure you have Node.js installed:

1. Open a terminal/command prompt
2. Run: `node --version`
3. Run: `npx --version`

If these commands fail, install Node.js from https://nodejs.org/ (LTS version recommended)

### Step 5: Restart Claude Desktop

1. Completely quit Claude Desktop (not just close the window)
2. Restart Claude Desktop
3. The n8n-MCP server should now load without errors

## Verification

To verify the configuration is working:

1. Open Claude Desktop
2. Check that there are no MCP error messages on startup
3. The n8n-mcp server should be available for use

## Troubleshooting

### Error: "command not found: npx"
- Install or reinstall Node.js from https://nodejs.org/

### Error: "n8n-mcp package not found"
- The npx command with `-y` flag should auto-install the package
- If it doesn't work, manually install: `npm install -g n8n-mcp`

### Error: "API authentication failed"
- Double-check your N8N_API_KEY is correct
- Verify you can access https://dmyaitt.app.n8n.cloud
- Ensure the API key has the necessary permissions

### Still getting errors?
- Check the Claude Desktop logs (usually in the same config directory)
- Ensure the JSON syntax in claude_desktop_config.json is valid
- Try removing the n8n-mcp entry temporarily to isolate the issue

## Configuration File Reference

The complete configuration file includes both MCP servers and should look like this:

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": [
        "-y",
        "n8n-mcp"
      ],
      "env": {
        "MCP_MODE": "stdio",
        "LOG_LEVEL": "error",
        "DISABLE_CONSOLE_OUTPUT": "true",
        "N8N_API_URL": "https://dmyaitt.app.n8n.cloud",
        "N8N_API_KEY": "your_actual_api_key_here"
      }
    },
    "n8n-workflows": {
      "command": "node",
      "args": ["C:\\Users\\Owner\\n8n-workflows-mcp\\server.js"]
    }
  }
}
```

**Note**: The configuration includes two MCP servers:
1. **n8n-mcp**: Official n8n MCP server using npx (connects to your n8n cloud instance)
2. **n8n-workflows**: Custom local workflow MCP server

If you only need the n8n-mcp server, you can remove the "n8n-workflows" section.

## Date Updated

October 24, 2025
