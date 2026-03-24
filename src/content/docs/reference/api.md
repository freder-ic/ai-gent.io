---
title: API Reference
description: Core API reference for ai-gent.
---

:::note
ai-gent is under active development. This API reference reflects the planned v0.1 interface.
:::

## Agent

The main class for creating and running agents.

```typescript
new Agent(config: AgentConfig)
```

### AgentConfig

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `provider` | `Provider` | Yes | LLM provider instance |
| `tools` | `Tool[]` | No | Available tools |
| `systemPrompt` | `string` | No | System prompt for the agent |
| `maxSteps` | `number` | No | Maximum reasoning steps (default: 10) |
| `memory` | `Memory` | No | Memory implementation |

### Methods

#### `agent.run(goal: string): Promise<AgentResult>`

Execute the agent with a goal. Returns the final result after the reasoning loop completes.

#### `agent.stream(goal: string): AsyncGenerator<AgentStep>`

Stream individual reasoning steps as they happen.

## defineTool

Helper to create type-safe tools.

```typescript
defineTool(config: ToolConfig): Tool
```

### ToolConfig

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `name` | `string` | Yes | Unique tool identifier |
| `description` | `string` | Yes | What the tool does (shown to LLM) |
| `parameters` | `object` | Yes | JSON Schema for parameters |
| `execute` | `function` | Yes | Implementation function |

## Providers

### OllamaProvider

```typescript
new OllamaProvider({
  model: string,
  baseUrl?: string, // default: http://localhost:11434
})
```

### LiteLLMProvider

```typescript
new LiteLLMProvider({
  model: string,
  baseUrl: string,
  apiKey?: string,
})
```
