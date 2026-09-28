# MCP setup (Cursor / Claude)

1. Create a Unshadow account and an MCP API key at [Integrations](https://unshadow.dev/integrations). Copy `unshadow_…` once. Optionally bind the key to a **project** so reads/writes stay in that pool.
2. Add to `~/.cursor/mcp.json` or project `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "weave": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.unshadow.dev"],
      "headers": {
        "Authorization": "Bearer unshadow_YOUR_KEY"
      }
    }
  }
}
```

On Windows, prefer the `headers` object (avoid spaces in CLI `--header` args). Direct URL config also works:

```json
{
  "mcpServers": {
    "weave": {
      "url": "https://mcp.unshadow.dev",
      "headers": {
        "Authorization": "Bearer unshadow_YOUR_KEY"
      }
    }
  }
}
```

3. Restart Cursor. Auth is the API key, not dashboard cookies.

**Claude.ai:** custom connector URL `https://mcp.unshadow.dev` → **Use Anthropic’s hosted client metadata** → leave Client ID/secret empty → Connect. Revoke later at [Integrations](https://unshadow.dev/integrations#claude-oauth).

Docs: [Cursor setup](https://unshadow.dev/docs/mcp/cursor-setup)
