---
name: weaveit-lattice
description: >-
  WeaveIt Lattice agent bank — retain/recall/reflect with trust envelopes on an
  isolated project. Use when the user wants autonomous-agent memory (Hermes,
  OpenClaw, Cursor stop-hook), not Engine search/save for personal capture.
---

# WeaveIt Lattice

Lattice is **agent memory**, not Engine REST/MCP for scripts. Engine tools (`memory_search`, `weave_inject_context`) stay for personal capture and n8n. This skill is for an isolated **bank** bound to a project key.

Docs: [Lattice](https://weaveit.app/docs/lattice) · [Integrations](https://weaveit.app/docs/integrations)

## Isolation

1. User creates a project (e.g. `Hermes bank`) and a `read_write` key **bound to that project**.
2. Do not reuse a Capture-pool (Sift / Ambient / Trace) key unless they intend to mix.
3. Capture is visible on recall only if they [link](https://weaveit.app/integrations#sandbox-links) that project into the bank.

## Lookup

- Prefer **`lattice_recall`** (`purpose`: `answer` | `tool_arg` | `reflect`). Trust envelopes: `certify` / `advisory` / `warn` / `block`.
- Packed context: `lattice_recall` with `format: "context"` or `lattice_reflect` for prefetch + optional synthesized beliefs.
- Before executing a tool, `lattice_recall({ purpose: "tool_arg", memory_ids })` and require `grounding_ok`.
- `lattice_explain` for an `operation_id`. `lattice_bank` for mission / directives.

Do not dump Engine `memory_search` into an agent bank session when Lattice MCP is connected.

## Remember / wrap-up

- Send a **delta** with `lattice_retain` (new text + `prev_hash` / `conversation_key`). Do not paste the full transcript.
- Cursor stop-hook (`packages/lattice-cursor-hook`) may already retain the last turn — extra `lattice_retain` only for durable facts the hook missed.
- `lattice_feedback` after using memories (`useful` / `wrong` / `stale` / `irrelevant`).
- `lattice_correct` expires ids; `lattice_forget` deletes ids **in this bank only**.

## Secrets

Memories classified `secret` must not enter context. Do not retain OTPs, passwords, or API keys.

More: [references/lattice.md](references/lattice.md)
