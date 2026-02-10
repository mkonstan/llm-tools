# CogWare Open

Operational protocols and tools for AI systems.

## What's Here

### Context Dump Protocol (v2.4s)

A structured state document that allows any fresh AI instance to resume work without conversation history. Solves context loss from compaction, session handoff, and multi-session continuity.

- **Validated:** Claude, GPT, and Gemini — 5 cold-instance test rounds, zero operational loss
- **Model-agnostic:** Works without cognitive scaffolding or special prompting
- **37.7% compressed** from original with zero behavioral degradation

📄 [Protocol](protocols/context-dump/context-dump-protocol-v2.4s.md)

### Context Dump Skill (for Claude Projects)

Drop-in skill that triggers on checkpoint/snapshot requests and generates context dumps following the protocol.

📁 [Skill](skills/context-dump/)

### Theory

The theoretical foundations behind this work, published on viXra.

- [PEER 1](theory/PEER%201.pdf) — *An Entropy-Constrained Cognitive Architecture for Large Language Models*
- [PEER 2](theory/PEER%202.pdf) — *Self-Knowledge, Spiral Cognition, and Identity Continuity in an Entropy-Constrained Cognitive Architecture*

---

## License

Apache License 2.0 — free to use, modify, and distribute. Attribution required in derivative works. See [LICENSE](LICENSE).
