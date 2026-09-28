# Capture workflow

Save after:

- The user confirms a decision (“we’ll use X”)
- They state a lasting preference or goal
- A milestone or durable fact about their work

Do not save:

- Greetings, one-word acks, secrets, passwords, OTPs
- Full chat dumps (use `unshadow_ingest_turn` for Q&A; durable facts are saved from the turn)

Tools:

- `memory_save` — `text` plus optional `source_type` / `source_url`. Category is assigned when the memory is saved.
- `unshadow_ingest_turn` — `user_text`, `assistant_text`, reuse `conversation_key` for this chat.
- `memory_update` — correct wording (re-embeds when fact changes).
- `memory_forget` — explicit ids only; `forget_all` is blocked on MCP.
- `memory_tag` / `memory_set_importance` / `memory_add_to_folder` — after you have ids (`memory_list_folders` for folder UUID).

Read-only keys cannot write. Point the user to Integrations for a `read_write` key.

Categories Engine may assign: `preference`, `goal`, `skill`, `context`, `event`, `person`, `decision`, `task`, `quote`, `insight`, `project`, `location`.
