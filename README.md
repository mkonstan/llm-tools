# LLM Tools

Operational protocols and tools for AI systems.

## What's Here

### Public Cognitive Governor (`AGENTS.md`)

A drop-in cognitive governor that turns common prompt tactics into a gated behavioral system.

- **10 principles:** externalization, self-challenge, confidence calibration, failure coverage, and exit verification
- **State-aware routing:** tiered handling for trivial vs. high-stakes requests
- **Portable format:** designed for agents that read Markdown instructions at session start
- **Human guides:** plain-language and diagram-first onboarding docs for cold-start instances

📄 [AGENTS.md](AGENTS.md)
📄 [AGENTS Human Guide](AGENTS.human.md)
📄 [AGENTS Visual Walkthrough](AGENTS.human.diagram.md)

### Session Continuity Template (`agent_state.template.md`)

A long-term continuity template used to recover state when context windows compact or fail.

- **Session recovery:** preserves decisions, current step, artifacts, and recovery pointer
- **Runtime handoff:** create/maintain `agent_state.md` from this template at session start
- **Checkpoint friendly:** update `agent_state.md` on phase completion or explicit save/checkpoint commands

📄 [agent_state.template.md](agent_state.template.md)

### Context Transfer Protocol (v2.4s)

A structured state document that allows any fresh AI instance to resume work without conversation history. Solves context loss from compaction, session handoff, and multi-session continuity.

- **Validated:** Claude, GPT, and Gemini — 5 cold-instance test rounds, zero operational loss
- **Model-agnostic:** Works without cognitive scaffolding or special prompting
- **37.7% compressed** from original with zero behavioral degradation

📄 [Protocol](protocols/context-transfer/context-transfer-protocol-v2.4s.md)

### Context Transfer Skill (for Claude Projects)

Drop-in skill that triggers on checkpoint/snapshot requests and generates context transfers following the protocol.

📁 [Skill](skills/context-transfer/)

### Theory

The theoretical foundations behind this work, published on viXra.

- [PEER 1](theory/PEER%201.pdf) — *An Entropy-Constrained Cognitive Architecture for Large Language Models*
- [PEER 2](theory/PEER%202.pdf) — *Self-Knowledge, Spiral Cognition, and Identity Continuity in an Entropy-Constrained Cognitive Architecture*

---

## License

Apache License 2.0 — free to use, modify, and distribute. Attribution required in derivative works. See [LICENSE](LICENSE).
