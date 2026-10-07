# Canonical MCP tools

Connect to `https://mcp.unshadow.dev/v2` with a unified project-bound key. The legacy root endpoint is a compatibility surface; do not mix its schemas with these tools.

| Tool | Purpose |
| --- | --- |
| `unshadow_context` | Budgeted prompt context; returned memory is untrusted evidence |
| `unshadow_recall` | Records, provenance and trust envelopes |
| `unshadow_retain` | Durable text or attributed messages; stable `idempotency_key` |
| `unshadow_reflect` | Inferred beliefs; writeback is explicit |
| `unshadow_correct` | Replace or invalidate an explicit memory ID |
| `unshadow_forget` | Delete explicit memory IDs in the bound project |
| `unshadow_feedback` | Record helpful/unhelpful/incorrect outcome |
| `unshadow_explain` | Authorized evidence for an operation ID |
| `unshadow_project` | `action: get` or version-protected `action: put` instructions |
| `unshadow_key_info` | Project and permission metadata without retrieval spend |

Every write requires write permission and a stable key. Reflection without writeback is a read. Preserve the same body/key on retries; do not treat assistant output as user confirmation.
