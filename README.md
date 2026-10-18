# x4-ai

**Provider-agnostic AI abstraction layer**

Unified generate / stream / embed / tool / evaluate API across OpenAI, Anthropic, Gemini, and local models.

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-v0.1-orange)](CHANGELOG.md)

Part of **[ARIEX4Ops / X4](https://github.com/dhe-cruzer69)**.

---

## Goal

Applications should not rewrite their AI integration when the underlying provider changes.

```python
from x4.ai import X4AI

ai = X4AI()
response = await ai.generate(
    model="openai/gpt-4o",
    messages=[{"role": "user", "content": "Hello"}],
    tools=[...],
)
```

## Architecture

## APEX Architecture Map

> Status: architecture documentation; implementation and deployment claims require independent verification.

```mermaid
flowchart TB
  Client[Calling feature] --> Contract[Provider request contract]
  Contract --> Policy{Provider permitted by config?}
  Policy -->|no| Block[Fail closed]
  Policy -->|yes| Router[Provider selector]
  Router --> Local[Local adapter]
  Router --> OpenAI[OpenAI adapter]
  Router --> Anthropic[Anthropic adapter]
  Local --> Normalize[Normalize response + usage]
  OpenAI --> Normalize
  Anthropic --> Normalize
  Normalize --> Validate[Validate output schema]
  Validate -->|invalid| Error[Typed provider error]
  Validate -->|valid| Cost[Record usage / estimated cost]
  Cost --> Result[Return response + provenance]
  Router --> Retry[Bounded retry policy]
  Retry -.only retry safe transient failures.-> Router
```
**Evidence note:** Adapters, provider configuration, retries, and cost accounting are target integration points. Never imply a provider is available unless its adapter and configuration are present.


See [ARCHITECTURE.md](ARCHITECTURE.md).

<!-- X4-APEX-DIAGRAM-START:x4-ai -->

```mermaid
flowchart TB
    CALLER[Application or Agent] --> API[Unified X4AI Interface]
    API --> OP[Generate]
    API --> STREAM[Stream]
    API --> EMBED[Embed]
    API --> TOOLS[Tool Invocation]
    API --> EVAL[Evaluate]
    OP --> ROUTE[Provider Resolver]
    STREAM --> ROUTE
    EMBED --> ROUTE
    TOOLS --> ROUTE
    EVAL --> ROUTE
    ROUTE --> OPENAI[OpenAI Adapter]
    ROUTE --> ANTHROPIC[Anthropic Adapter]
    ROUTE --> GEMINI[Gemini Adapter]
    ROUTE --> LOCAL[Local Model Adapter]
    OPENAI --> NORMALIZE[Normalize Provider Response]
    ANTHROPIC --> NORMALIZE
    GEMINI --> NORMALIZE
    LOCAL --> NORMALIZE
    NORMALIZE --> CALLER
```

<!-- X4-APEX-DIAGRAM-END:x4-ai -->

## Related

- [x4-agents](https://github.com/dhe-cruzer69/x4-agents)
- [x4-core](https://github.com/dhe-cruzer69/x4-core)
- [omniforge](https://github.com/dhe-cruzer69/omniforge) (local-first inspiration)

## License

Apache-2.0

## Support

**[GitHub Sponsors](https://github.com/sponsors/dhe-cruzer69)**
