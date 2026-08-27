# Lattice tools

HTTP base: `https://api.weaveit.app/v1` with the same `weave_it_…` key. MCP names:

| Tool | Maps to | Notes |
|------|---------|--------|
| `lattice_retain` | POST `/lattice/retain` | Delta write; 32k max; 409 on checkpoint mismatch |
| `lattice_recall` | POST `/lattice/recall` | Envelopes + records; optional `format: context` |
| `lattice_reflect` | POST `/lattice/reflect` | Recall + mission → inferred beliefs; writeback needs write key |
| `lattice_feedback` | POST `/lattice/feedback` | Decision receipt |
| `lattice_correct` | POST `/lattice/correct` | Expire ids (`MEMORY_CORRECTED`) |
| `lattice_forget` | POST `/lattice/forget` | Delete ids in this sandbox |
| `lattice_explain` | POST `/lattice/explain` | Events for `operation_id` |
| `lattice_bank` | GET/POST `/lattice/bank` | Mission / directives |

Write-gated: retain, reflect (when storing), feedback, correct, forget.

Native hosts (not this MCP catalog): Hermes MemoryProvider, OpenClaw `kind: memory` slot, Cursor stop-hook, LangGraph store. See [Integrations gallery](https://weaveit.app/docs/integrations).
