---
name: unshadow-bank
description: >-
  Unshadow agent bank — retain/recall/reflect with trust envelopes on an
  isolated project. Use when the user wants autonomous-agent memory (Hermes,
  OpenClaw, Cursor stop-hook), not Engine search/save for personal capture.
---

# Unshadow agent bank

An agent bank is **agent memory**, not Engine REST/MCP for scripts. Engine tools (`memory_search`, `unshadow_inject_context`) stay for personal capture and n8n. This skill is for an isolated **bank** bound to a project key.

Docs: [Agent banks](https://unshadow.dev/docs/lattice) · [Integrations](https://unshadow.dev/docs/integrations)

## Isolation

1. User creates a project (e.g. `Hermes bank`) and a `read_write` key **bound to that project**.
2. Do not reuse a Capture-pool (Sift / Ambient / Trace) key unless they intend to mix.
3. Capture is visible on recall only if they [link](https://unshadow.dev/integrations#sandbox-links) that project into the bank.

## Lookup

- Prefer **`unshadow_bank_recall`** (`purpose`: `answer` | `tool_arg` | `reflect`). Trust envelopes: `certify` / `advisory` / `warn` / `block`.
- Packed context: `unshadow_bank_recall` with `format: "context"` or `unshadow_bank_reflect` for prefetch + optional synthesized beliefs.
- Before executing a tool, `unshadow_bank_recall({ purpose: "tool_arg", memory_ids })` and require `grounding_ok`.
- `unshadow_bank_explain` for an `operation_id`. `unshadow_bank` for mission / directives.

Do not dump Engine `memory_search` into an agent bank session when the bank MCP tools are connected.

## Remember / wrap-up

- Send a **delta** with `unshadow_bank_retain` (new text + `prev_hash` / `conversation_key`). Do not paste the full transcript.
- Cursor stop-hook (`packages/lattice-cursor-hook`) may already retain the last turn — extra `unshadow_bank_retain` only for durable facts the hook missed.
- `unshadow_bank_feedback` after using memories (`useful` / `wrong` / `stale` / `irrelevant`).
- `unshadow_bank_correct` expires ids; `unshadow_bank_forget` deletes ids **in this bank only**.

## Secrets

Memories classified `secret` must not enter context. Do not retain OTPs, passwords, or API keys.

More: [references/bank.md](references/bank.md)
