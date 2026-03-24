---
title: Introduction
description: What is ai-gent and how does it work?
---

ai-gent is an open-source framework for building AI agents that can reason, plan, and use tools to accomplish goals autonomously.

## Key Concepts

- **Agent** — An autonomous system that takes a goal and works toward it using an LLM, tools, and memory
- **Tool** — A function an agent can call (API requests, file I/O, code execution, database queries)
- **Router** — Decides which LLM to use for each task (local for simple, cloud for complex)
- **Memory** — Persistent context across agent steps (conversation history, vector store)

## Architecture

```
User Goal
  → Agent (LLM reasoning loop)
    → Tool calls (APIs, files, code)
    → Memory (context, embeddings)
    → Router (local vs cloud LLM)
  → Result
```

## Design Principles

1. **Local-first**: Prefer local models. Use cloud as fallback, not default.
2. **Tool-native**: Agents are only as useful as their tools. Make tools easy to define.
3. **Observable**: Every agent step is logged and traceable.
4. **Simple**: No magic. You can read and understand the entire framework.

## Next Steps

Follow the [Quick Start](/guides/quickstart/) to build your first agent.
