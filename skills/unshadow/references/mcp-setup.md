# Native MCP setup

Canonical tools require `https://mcp.unshadow.dev/v2` and a unified project-bound key. Set `UNSHADOW_API_KEY` in each host's launch environment; never print or commit the value. Restart already-running hosts after changing it.

## Cursor

Merge into `.cursor/mcp.json` or `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "unshadow": {
      "url": "https://mcp.unshadow.dev/v2",
      "headers": { "Authorization": "Bearer ${env:UNSHADOW_API_KEY}" }
    }
  }
}
```

Remote HTTP is native; no runtime bridge is needed. Hook capture is opt-in and requires its ownership rule. Session-start injection is not per-turn recall.

## Codex

Merge into `~/.codex/config.toml` or a trusted project's `.codex/config.toml`:

```toml
[mcp_servers.unshadow]
url = "https://mcp.unshadow.dev/v2"
bearer_token_env_var = "UNSHADOW_API_KEY"
```

Check `codex mcp list`. CLI and desktop inherit different process environments; test them separately. For OAuth remove the bearer environment field and run `codex mcp login unshadow`. Keep approvals and revoke grants on Unshadow when no longer needed. [Codex guide](https://unshadow.dev/docs/mcp/codex-setup).

## Claude Code

Merge into project `.mcp.json`:

```json
{
  "mcpServers": {
    "unshadow": {
      "type": "http",
      "url": "https://mcp.unshadow.dev/v2",
      "headers": { "Authorization": "Bearer ${UNSHADOW_API_KEY}" }
    }
  }
}
```

Use `/mcp` for discovery/approval. For OAuth omit static headers and follow authentication there. This is separate from Claude Desktop and claude.ai. [Claude Code guide](https://unshadow.dev/docs/mcp/claude-code-setup).

Verify `unshadow_key_info`, synthetic retain/recall/context/correct/forget, read-only and revoked credentials, and project isolation. Tools do not guarantee the model calls them automatically. If a Cursor hook owns capture, disable automatic skill/playbook ingestion; explicit manual text saves remain available. Never weaken approvals to make tests pass.
