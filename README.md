# Unshadow agent skills

A **skill** decides when to use memory. **MCP** invokes the operation. Application code can skip MCP and call the **SDK**, which talks to Engine (`/context`, `/search`, `/extract`) or Agent Bank (`/bank/*`).

| Surface | Role |
|---------|------|
| **unshadow** skill | Teaches when to use Engine MCP (`unshadow_inject_context`, `memory_search`, `memory_save`). Judgment only — does not store or search. |
| **unshadow-bank** skill | Teaches when to retain, recall, reflect, correct, forget, and read/update mission via `unshadow_bank`. MCP executes. |
| **@unshadow/sdk** / `pip install unshadow` | Developer library. `createUnshadowEngineClient` / `Unshadow` → Engine. `UnshadowBank` → `/bank/*`. LangChain and LangGraph use the SDK, not MCP. |
| **[unshadow-ai/agent-skills](https://github.com/unshadow-ai/agent-skills)** | Distribution catalog for `npx skills add` — not a runtime API, MCP server, or SDK. |

Install:

```bash
npx skills add unshadow-ai/agent-skills -a cursor -y
```

Source of truth is `packages/agent-skills` in the Unshadow monorepo. The public repo is synced by the Mirror agent-skills workflow (`AGENT_SKILLS_DEPLOY_TOKEN`).

Docs: [unshadow.dev/docs/mcp/skills](https://unshadow.dev/docs/mcp/skills)
