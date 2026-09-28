---
name: unshadow-bank
description: >-
  Unshadow agent bank — retain/recall/reflect with trust envelopes on a
  project. Use when the user wants autonomous-agent memory (Hermes,
  OpenClaw, Cursor stop-hook), not personal search and save.
---

# Unshadow agent bank

Use this skill for an **agent bank** bound to a project key. Personal search and save stay on `memory_search` and `unshadow_inject_context`.

Docs: [Agent Bank](https://unshadow.dev/docs/lattice) · [Integrations](https://unshadow.dev/docs/integrations)

## Setup

1. User creates a project (e.g. `Hermes bank`) and a `read_write` key **bound to that project**.
2. Use that key for the bank. Do not reuse a Sift, Ambient, or Trace key unless they intend to mix memories.

## Lookup

- Prefer **`unshadow_bank_recall`** (`purpose`: `answer` | `tool_arg` | `reflect`). Trust envelopes: `certify` / `advisory` / `warn` / `block`.
- Packed context: `unshadow_bank_recall` with `format: "context"` or `unshadow_bank_reflect` for prefetch + optional synthesized beliefs.
- Before executing a tool, `unshadow_bank_recall({ purpose: "tool_arg", memory_ids })` and require `grounding_ok`.
- `unshadow_bank_explain` for an `operation_id`. `unshadow_bank` for mission / directives.

Do not dump `memory_search` into an agent bank session when the bank MCP tools are connected.

## Remember / wrap-up

- Send a **delta** with `unshadow_bank_retain` (new text + `prev_hash` / `conversation_key`). Do not paste the full transcript.
- A Cursor stop-hook may already retain the last turn — extra `unshadow_bank_retain` only for durable facts the hook missed.
- `unshadow_bank_feedback` after using memories (`useful` / `wrong` / `stale` / `irrelevant`).
- `unshadow_bank_correct` expires ids; `unshadow_bank_forget` deletes ids **in this bank only**.

## Secrets

Memories classified `secret` must not enter context. Do not retain OTPs, passwords, or API keys.

More: [references/bank.md](references/bank.md)
