---
title: Quick Start
description: Build your first ai-gent agent in 5 minutes.
---

This guide walks you through creating a simple agent that answers questions using a local LLM.

## Prerequisites

- [Ollama](https://ollama.ai) installed and running
- A model pulled (e.g., `ollama pull qwen3:8b`)
- Node.js 20+ or Python 3.11+

## Installation

```bash
# Coming soon — the framework is under active development
npm install @ai-gent/core
```

## Your First Agent

```typescript
import { Agent, OllamaProvider } from '@ai-gent/core';

const agent = new Agent({
  provider: new OllamaProvider({
    model: 'qwen3:8b',
    baseUrl: 'http://localhost:11434',
  }),
  tools: [],
  systemPrompt: 'You are a helpful assistant.',
});

const result = await agent.run('What is the capital of France?');
console.log(result);
```

## Adding Tools

Tools give your agent superpowers. Here's a simple web search tool:

```typescript
import { Agent, OllamaProvider, defineTool } from '@ai-gent/core';

const searchTool = defineTool({
  name: 'web_search',
  description: 'Search the web for information',
  parameters: {
    query: { type: 'string', description: 'Search query' },
  },
  execute: async ({ query }) => {
    // Your search implementation here
    return `Results for: ${query}`;
  },
});

const agent = new Agent({
  provider: new OllamaProvider({ model: 'qwen3:8b' }),
  tools: [searchTool],
});
```

## Using LiteLLM Router

For hybrid local/cloud routing:

```typescript
import { Agent, LiteLLMProvider } from '@ai-gent/core';

const agent = new Agent({
  provider: new LiteLLMProvider({
    baseUrl: 'http://localhost:4000/v1',
    apiKey: 'your-litellm-key',
    model: 'local-general', // Routes via LiteLLM
  }),
});
```

## Next Steps

- Read about the [Architecture](/concepts/architecture/) to understand how agents work internally
- Check the [API Reference](/reference/api/) for all available options
