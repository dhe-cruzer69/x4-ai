# x4-ai Architecture

## Goal

Decouple application code from any single model provider.

## Layers

```
Application
    ↓
x4-ai API (generate / stream / embed / tool / evaluate)
    ↓
Provider Adapters (OpenAI, Anthropic, Gemini, Local)
    ↓
Safety + Observability + Cost accounting
```

## Design rules

- Thin, stable public API
- Provider-specific details stay inside adapters
- Structured output and tool-calling are first-class
- Retries, fallbacks, and model routing are supported
- Token and cost tracking available
