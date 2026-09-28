# Engine MCP tools (hosted `mcp.unshadow.dev`)

Live count is **32** registered tools including deprecated `get_user_memory`. Prefer the names below.

## Retrieval

| Tool | Use |
|------|-----|
| `unshadow_inject_context` | Prompt-ready pack for the current topic |
| `unshadow_context` | Same `/context` with explicit budget fields |
| `memory_search` | Structured lookup / debug |
| `memory_get` | Full memory JSON by id |
| `memory_search_by_date` | Hybrid search + `since`/`until` |
| `memory_get_related` | Graph neighbors |
| `memory_history` | Version timeline |
| `memory_list` | Recent list (`category` optional) |
| `memory_list_folders` | Folder `{ id, name }` |
| `memory_folder_contents` | Memories in a folder UUID |
| `unshadow_profile` | Profile slice |
| `unshadow_memory_surface` | Proactive high-importance suggestions |
| `get_user_memory` | Deprecated — use inject or search |

## Write / manage

| Tool | Use |
|------|-----|
| `memory_save` | Extract + store a fact |
| `unshadow_ingest_turn` | Archive Q&A then extract |
| `memory_update` | Patch fact (re-embeds) |
| `memory_forget` | Delete listed ids |
| `memory_tag` | Merge tags |
| `memory_set_importance` | 0–1 importance |
| `memory_add_to_folder` | Set `folder_id` |
| `memory_verify_source` | Raw row by id (prefer `memory_get`) |

## Account

`weave_export_data`, `weave_privacy_settings`, `weave_digest`

## Agent bank (`unshadow_bank_*`)

Only for agent banks. See the **unshadow-bank** skill. Use the project key for that bank.

Write tools need a `read_write` key.
