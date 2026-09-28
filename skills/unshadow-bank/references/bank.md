# Agent bank tools

| MCP tool | HTTP | Notes |
|----------|------|-------|
| `unshadow_bank_retain` | POST `/bank/retain` | Delta write; 32k max; 409 on checkpoint mismatch |
| `unshadow_bank_recall` | POST `/bank/recall` | Envelopes + records; optional `format: context` |
| `unshadow_bank_reflect` | POST `/bank/reflect` | Recall + mission → inferred beliefs; writeback needs write key |
| `unshadow_bank_feedback` | POST `/bank/feedback` | Decision receipt |
| `unshadow_bank_correct` | POST `/bank/correct` | Expire ids (`MEMORY_CORRECTED`) |
| `unshadow_bank_forget` | POST `/bank/forget` | Delete ids in this sandbox |
| `unshadow_bank_explain` | POST `/bank/explain` | Events for `operation_id` |
| `unshadow_bank` | GET/POST `/bank` | Mission / directives |
