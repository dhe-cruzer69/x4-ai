# x4-ai

**Provider-agnostic AI abstraction layer**

Unified `generate` / `stream` / `embed` / `tool` / `evaluate` API across OpenAI, Anthropic, Gemini, and local models.

Part of [ARIEX4Ops / X4](https://github.com/dhe-cruzer69).

## Goal

```python
from x4.ai import X4AI

ai = X4AI()
response = await ai.generate(
    model="openai/gpt-4o",
    messages=[{"role": "user", "content": "..."}],
    tools=[...],
)
```

Switch providers without rewriting application code.

## Status

v0.1 foundation.

## Related

- [x4-agents](https://github.com/dhe-cruzer69/x4-agents)
- [x4-core](https://github.com/dhe-cruzer69/x4-core)
- [omniforge](https://github.com/dhe-cruzer69/omniforge) (local-first inspiration)

## License

Apache-2.0

## Support

[GitHub Sponsors](https://github.com/sponsors/dhe-cruzer69)
