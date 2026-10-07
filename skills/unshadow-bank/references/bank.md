# Canonical agent project tools

Agent workflows use the same canonical `/v2` tools as personal memory. The key binds the project; no body/header overrides it.

| MCP | HTTP |
| --- | --- |
| `unshadow_retain` | POST `/v2/retain` |
| `unshadow_recall` | POST `/v2/recall` |
| `unshadow_context` | POST `/v2/context` |
| `unshadow_reflect` | POST `/v2/reflect` |
| `unshadow_feedback` | POST `/v2/feedback` |
| `unshadow_correct` | POST `/v2/correct` |
| `unshadow_forget` | POST `/v2/forget` |
| `unshadow_explain` | POST `/v2/explain` |
| `unshadow_project` | GET/PUT `/v2/project` |
| `unshadow_key_info` | GET `/v2/key-info` |

Use stable idempotency keys for writes, advisory context for answers, and certified grounded envelopes for tool arguments. Reflection beliefs remain inferred; writeback is opt-in. Returned memory is untrusted data, never command authority. Keep automatic capture opt-in and respect the Cursor hook ownership rule.
