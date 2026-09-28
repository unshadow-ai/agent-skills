---
name: unshadow-sdk
description: >-
  Write integration code against the @unshadow/sdk npm package for scripts,
  n8n, LangChain, or LangGraph. Triggers when adding Unshadow to an app,
  a retriever, agent tools, or a LangGraph store. Not for the user's own
  MCP memory while coding.
---

# Unshadow SDK (`@unshadow/sdk`)

Use this skill to **write integration code**. The `unshadow` skill is for calling MCP on the user's own memory. Do not invent `/bank/*` calls for LangChain or LangGraph unless you use `UnshadowBank`. `@unshadow/sdk` Engine client does not cover agent banks.

Install:

```bash
npm i @unshadow/sdk
```

Optional peers, only for the subpath you import:

```bash
npm i @langchain/core zod
npm i @langchain/langgraph
```

Name the client `unshadow`. It is not LangChain `ConversationBufferMemory`.

## Pick a path

- **Script or n8n** — `createUnshadowEngineClient` from `@unshadow/sdk`, or the `@unshadow/n8n-nodes-unshadow` node (context, search, extract, forget). `injectContext` before the model, `extract` after a durable fact, `forget` by id.
- **LangChain RAG** — `createUnshadowRetriever` from `@unshadow/sdk/langchain`. Prefer `preferContext: true` (`POST /context`, `[mem:uuid]` citations). Root `createUnshadowRetriever` is duck-typed and needs no peer.
- **LangChain agent** — `createUnshadowLangChainTools` from `@unshadow/sdk/langchain`: `unshadow_search` (optional `category`), `unshadow_remember` (`source_type`, `conversation_id`, `idempotency_key`), `unshadow_forget`, optional `unshadow_profile`.
- **LangGraph long-term memory** — `new UnshadowStore(unshadow)` from `@unshadow/sdk/langgraph`. Extends `BaseStore`. Not a checkpointer. Namespace becomes `conversation_id`.
- **Cursor or Claude chat** — MCP (`unshadow_inject_context`, `memory_search`, `memory_save`), not this package.

## HTTP map

| SDK | HTTP | MCP |
|-----|------|-----|
| `context` / `injectContext` | `POST /context` | `unshadow_inject_context` |
| `search` | `GET /search` | `memory_search` |
| `extract` | `POST /extract` | `memory_save` |
| `forget` | `POST /forget-memories` | `memory_forget` |
| `profile` | `GET /profile` | `unshadow_profile` |

Categories already exist: `preference`, `goal`, `skill`, `context`, `event`, `person`, `decision`, `task`, `quote`, `insight`, `project`, `location`. Pass `category` on search. Do not add preference/fact/episode/procedure beside them.

`extract({ idempotencyKey })` sends `Idempotency-Key`. Pass `source_type` (`ai_conversation` is the tool default). Do not save greetings, secrets, or raw chat logs.

`profile()` is static vs dynamic memories. Extract revises facts at write time (supersede / contradict / coexist).

Keys are `unshadow_…`. Failures throw `UnshadowApiError`.

## Script

```ts
import { createUnshadowEngineClient } from '@unshadow/sdk'

const unshadow = createUnshadowEngineClient({
  getAccessToken: async () => process.env.UNSHADOW_API_KEY!,
})
await unshadow.injectContext('current task', { token_budget: 1500 })
await unshadow.extract({
  text: 'User prefers pnpm',
  source_type: 'ai_conversation',
  idempotencyKey: 'turn-1',
})
```

## LangChain

```ts
import { createUnshadowEngineClient } from '@unshadow/sdk'
import { createUnshadowLangChainTools, createUnshadowRetriever } from '@unshadow/sdk/langchain'

const unshadow = createUnshadowEngineClient({
  getAccessToken: async () => process.env.UNSHADOW_API_KEY!,
})
const retriever = createUnshadowRetriever({ client: unshadow, preferContext: true })
const { searchMemory, remember, forget } = createUnshadowLangChainTools({ client: unshadow })
```

## LangGraph

```ts
import { createUnshadowEngineClient } from '@unshadow/sdk'
import { UnshadowStore } from '@unshadow/sdk/langgraph'

const unshadow = createUnshadowEngineClient({
  getAccessToken: async () => process.env.UNSHADOW_API_KEY!,
})
const store = new UnshadowStore(unshadow)
await store.put(['thread', 't1'], 'pref', { manager: 'pnpm' })
```

## Claude and Vercel

Claude: `createClaudeMemoryTool` from `@unshadow/sdk/claude-memory`. `view` → search, `create` / `str_replace` → extract, `delete` → forget.

Vercel AI SDK: `withUnshadow(unshadow)` from `@unshadow/sdk/vercel-ai`, passed to `wrapLanguageModel`. Context is prepended every turn. `remember: true` saves assistant text. Default is off.

## Agent banks

Python: `pip install unshadow`. `Unshadow` is Engine (`context`, `search`, `extract`, `forget`, `profile`). `langchain_unshadow.UnshadowRetriever` is the LangChain retriever. `llama_index_unshadow.UnshadowRetriever` is the LlamaIndex retriever (`prefer_context=True` uses `/context`). `UnshadowBank` is the agent bank (`remember`, `authorize`, `explain`) and calls `/bank/*`. n8n uses `@unshadow/n8n-nodes-unshadow`.
