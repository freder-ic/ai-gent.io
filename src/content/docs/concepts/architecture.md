---
title: Architecture
description: How ai-gent agents work internally.
---

## Overview

An ai-gent agent is a loop: receive a goal, reason about next steps, execute tools, observe results, repeat until done.

```
┌──────────────────────────────┐
│         Agent Loop           │
│                              │
│  1. Receive goal/context     │
│  2. LLM reasons about next   │
│     step                     │
│  3. Execute tool (if needed) │
│  4. Observe result           │
│  5. Update memory            │
│  6. Repeat or return result  │
│                              │
└──────────────────────────────┘
```

## Components

### Provider

The LLM backend. Supports:
- **Ollama** — Local models (Qwen, DeepSeek, Llama)
- **LiteLLM** — Proxy that routes between local and cloud
- **OpenAI-compatible** — Any API following the OpenAI spec

### Tools

Functions the agent can call. Each tool has:
- A name and description (for the LLM to understand when to use it)
- Parameter schema (validated at runtime)
- An execute function

### Memory

Context that persists across reasoning steps:
- **Conversation memory** — Message history within a run
- **Vector memory** — Embeddings for long-term retrieval (optional)

### Router

Decides which model handles each request:
- Simple tasks → local model (free, fast)
- Complex reasoning → cloud model (paid, better)
- Configurable rules based on task type, token count, or custom logic
