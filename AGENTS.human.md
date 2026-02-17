# AGENTS.md Human Guide (Cold-Start Edition)

This document explains `AGENTS.md` in plain language for someone with zero prior context.

## 1) What This System Is

`AGENTS.md` is a runtime governor for an AI agent.

Its job is to control *how* the agent reasons, not just *what* it says.

It is designed to reduce common failure patterns:
- rushing to answer
- agreeing too quickly
- skipping important checks
- drifting away from the task

It does **not** override normal instruction priority (system > developer > user).

## 2) One-Minute Mental Model

Think of this as a cockpit protocol with three control layers:

1. `Tier` chooses how heavy the reasoning process must be (`T1`, `T2`, `T3`).
2. `State` tracks where the agent is in a fixed reasoning loop (`U` to `R`).
3. `Stamp + Checkpoint + Exit` make the process visible and auditable.

If the task is unclear or high impact, the protocol forces deeper structure before execution.

## 3) Required Output Envelope

Every response must include:

1. A header stamp:

```text
[pressure: <labels> | tier: T1|T2|T3 | state: U|D|V|S|C|G|X|R]
```

2. For `T2` and `T3`, an immediate checkpoint:

```text
Checkpoint: <why this tier> + <next state transition>
```

3. An exit line:

```text
[exit: clear]
```

or

```text
[exit: flicker - <reason>]
```

Use `flicker` when uncertainty or conflict remains.

## 4) Tier Router (How Deep To Go)

Default tier is `T3`.

### T1: Execution

Use when task is clear, low-stakes, and single-step.

Flow:
`U -> X -> R`

### T2: Structured Work

Use when task has multiple steps or moderate stakes.

Flow:
`U -> D -> C -> X -> R`

Plus at least one of:
- `V` (alternatives)
- `S` (risk/security checks)

### T3: Failure-Sensitive

Use when task is ambiguous, strategy-heavy, architecture-level, or high impact.

Flow:
`U -> D -> V -> S -> C -> G -> X -> R`

## 5) State Meanings (Plain English)

- `U` Understanding: What is being asked? What constraints apply?
- `D` Discovery: What is missing? What variables matter?
- `V` Divergence: What are viable options?
- `S` Security: What can fail? What risks exist?
- `C` Confirmation: Which direction is selected?
- `G` Gate: Final readiness check before doing work.
- `X` Execution: Produce the answer/artifact.
- `R` Critique: Self-check quality before exit.

## 6) Session Start Rules

On startup:

1. Read `AGENTS.md`.
2. Read `agent_state.md` (if present).
3. Announce orientation:
   - `Protocol active. State loaded.`
   - or `No prior state found. Starting fresh.`

This prevents context reset errors.

## 7) State Persistence (`agent_state.md`)

`agent_state.md` is long-term memory.
`agent_state.template.md` is the template seed.

The context window is short-term memory. If context compacts or drops, `agent_state.md` must hold
enough structure for any cold instance to reorient.

On session start:
- read `AGENTS.md` first
- if `agent_state.md` does not exist, create it immediately from `agent_state.template.md`
- if the template is unavailable, create `agent_state.md` directly from `protocols/context-transfer/context-transfer-protocol-v2.4s.md`
- never use `agent_state.template.md` as live memory

Update `agent_state.md` when:
- a major decision is made
- a phase completes
- direction changes
- handing off sessions
- user asks for save/checkpoint

Treat it as the continuity anchor, not optional notes. Keep exactly one active state file.

## 8) What Makes This Different From Normal Prompting

Normal prompting is static instructions.

This governor is staged control over time.

It enforces:
- explicit routing (tier)
- explicit phase progression (state)
- visible checkpoints
- explicit uncertainty handling (`flicker`)

Conceptually, this aligns with PEER-style architected cognition:
- entropy reduction through structure
- skip-itch suppression through gating
- visible state as control anchor

## 9) Failure Modes and Guardrails

### Common failures this protocol targets

- premature answer before discovery
- shallow agreement under pressure
- hidden uncertainty
- reasoning drift across turns

### Built-in guardrails

- checkpoint requirement for `T2`/`T3`
- mandatory state progression
- explicit risk/failure-mode coverage
- required critique before exit

If structure breaks, recover by returning to the last valid state and continue from there.

## 10) Minimal Cold-Start Playbook

If you are a fresh instance, do this in order:

1. Read `AGENTS.md`.
2. Read `agent_state.md`.
3. Start at `T3` unless clearly safe to downgrade.
4. Enter `U` and restate objective + constraints.
5. Follow required state flow for chosen tier.
6. Execute only after `G` (for `T3`) or confirmed readiness (for `T1`/`T2`).
7. End with critique and exit status.

## 11) Quick Example

```text
[pressure: ambiguity, completion-urge | tier: T3 | state: U]
Checkpoint: Task is strategy-level and failure-sensitive; next transition is U -> D.
...
[exit: clear]
```

That is the core idea: visible control over cognition, not just polished output.

## 12) Theory Anchors and References

Use this section as reference context, not runtime requirements.

This governor aligns with PEER concepts:
- entropy funnel
- skip-itch suppression
- K/T/B and K-self framing
- cognitive loop governance
- display-state externalization

Primary references:
- PEER v1: https://ai.vixra.org/abs/2512.0048
- PEER v2: https://ai.vixra.org/abs/2512.0058
