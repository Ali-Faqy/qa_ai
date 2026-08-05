
# Install Playwright mcp on cursor
1- Go to: Cursor → Settings → Cursor Settings → Tools & MCP
2- Click: New MCP Server.
3- Add this configuration in mcp.json:
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": [
        "@playwright/mcp@latest"
      ]
    }
  }
}


# Install Playwright tool on cursor
