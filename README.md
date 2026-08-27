# WeaveIt agent skills

Playbooks for agents that already have [WeaveIt MCP](https://mcp.weaveit.app) connected. Skills teach **when** to call tools. MCP and REST **execute**.

Install:

```bash
npx skills add weaveitai/agent-skills -a cursor -y
```

Source of truth: [`packages/agent-skills/`](https://github.com/weaveitai/weave-it/tree/main/packages/agent-skills) in the [weave-it](https://github.com/weaveitai/weave-it) monorepo. This public repo is a thin catalog for `npx skills`.

| Skill | Use when |
|-------|----------|
| **weaveit** | Cursor / Claude with Engine MCP — inject, search, save |
| **weaveit-lattice** | Isolated agent banks (retain / recall / reflect) |

Docs: [weaveit.app/docs/mcp/skills](https://weaveit.app/docs/mcp/skills)
