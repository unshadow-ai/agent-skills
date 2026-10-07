# Capture workflow

Save explicit user requests and authorized durable preferences/decisions through `unshadow_retain`. Example: `{text:"Synthetic preference: use pnpm", source_type:"manual_entry", idempotency_key:"event-123:retain"}`. Retry the identical payload with the identical key. Use separate keys for different operations. Preserve role attribution for message arrays; assistant claims remain inferred.

Automatic turn capture is off unless the operator explicitly opts in. If a Cursor hook owns capture, do not automatically send message arrays or conversation ingestion; manual durable text saves remain available. Skip secrets, OTPs, credentials, greetings and ephemeral noise.

`unshadow_correct({memory_id, replacement, idempotency_key})` replaces a statement; explicit `invalidate:true` invalidates it instead. `unshadow_forget({memory_ids, idempotency_key})` deletes actual IDs. Read-only credentials reject writes. Conflicts require inspecting the original event/payload rather than changing keys to force a second effect.
