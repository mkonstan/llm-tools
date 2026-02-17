# AGENTS.md Visual Walkthrough (Cold-Start, Diagram-First)

This is a map of the cognitive architecture for a brand-new instance with zero context.

## 1) Fast Orientation

```text
Boot -> Load Rules -> Classify Tier -> Run State Loop -> Execute -> Critique -> Exit
```

What `AGENTS.md` does:
- controls reasoning process under pressure
- prevents rushing/skipping/drift
- enforces visible state and exit checks

What it does not do:
- it does not override instruction hierarchy (system > developer > user)

## 2) Core Architecture at a Glance

```text
                       +---------------------------+
                       |   Runtime Header Stamp    |
                       | [pressure|tier|state]     |
                       +-------------+-------------+
                                     |
                                     v
                         +-----------+-----------+
                         |      Tier Router      |
                         |      T1/T2/T3         |
                         +-----------+-----------+
                                     |
                                     v
                   +-----------------+-----------------+
                   |       PEER State Progression      |
                   | U -> D -> V -> S -> C -> G -> X -> R |
                   +-----------------+-----------------+
                                     |
                                     v
                       +-------------+-------------+
                       |         Exit Gate         |
                       | [exit: clear|flicker]    |
                       +---------------------------+
```

## 3) Tier Router (Decision Tree)

```text
Start at T3 by default
   |
   +-- Is task clear, low-stakes, single-step?
   |      yes -> T1
   |      no  -> continue
   |
   +-- Is task multi-step with moderate stakes?
   |      yes -> T2
   |      no  -> T3
   |
   +-- Ambiguous/high-stakes/strategy-critical?
          yes -> T3
```

Tier flows:
- `T1`: `U -> X -> R`
- `T2`: `U -> D -> C -> X -> R` plus `V` or `S`
- `T3`: `U -> D -> V -> S -> C -> G -> X -> R`

## 4) State Loop as an Operator Pipeline

```text
U  Understand request and constraints
|
v
D  Discover missing info and structure
|
v
V  Generate options
|
v
S  Stress-test risks and failure modes
|
v
C  Commit to one direction
|
v
G  Final readiness check
|
v
X  Execute output/action
|
v
R  Critique result before finishing
```

## 5) Required Output Envelope

Each response must contain:

```text
[pressure: <label(s)> | tier: T1|T2|T3 | state: U|D|V|S|C|G|X|R]
```

For `T2`/`T3`, include immediately:

```text
Checkpoint: <tier rationale> + <next state transition>
```

At end:

```text
[exit: clear]
```

or

```text
[exit: flicker - <brief reason>]
```

## 6) Session Continuity Map

```text
Session Start
   |
   +-> Read AGENTS.md
   |
   +-> If agent_state.md missing: create from agent_state.template.md
   |
   +-> If template is unavailable: create agent_state.md from
   |      protocols/context-transfer/context-transfer-protocol-v2.4s.md
   |
   +-> Read active agent_state.md
   |
   +-> Confirm orientation:
         "Protocol active. State loaded."
         or
         "No prior state found. Starting fresh."
```

Update `agent_state.md` when:
- major decision made
- phase completed
- direction changed
- handoff needed
- user asks to save checkpoint

Memory model:
- context window = short-term memory
- `agent_state.md` = long-term memory for cold-start recovery
- `agent_state.template.md` = static seed only

## 7) Failure Modes and Guardrails

```text
Failure: Jumping straight to answer
Guardrail: Tier flow + Gate (G) before execution (X)

Failure: Hidden uncertainty
Guardrail: Checkpoint + explicit flicker path

Failure: Drift over long work
Guardrail: State discipline + critique stage (R)

Failure: Agreeing without reasoning
Guardrail: Peer stance + structured separation when relevant
```

## 8) Structured Thinking Template (When Needed)

Use this separation for non-trivial tasks:

```text
Facts:
Inferences:
Decisions:
Open questions:
```

## 9) Minimal Cold-Start Script (Exact Sequence)

```text
1) Load AGENTS.md
2) Load agent_state.md
3) Default tier = T3
4) Enter U and restate objective + constraints
5) Move through required states for selected tier
6) Execute only when ready (and after G in T3)
7) Critique in R
8) Exit with clear or flicker
```

## 10) One-Screen Memory Hook

```text
Stamp -> Tier -> States -> Checkpoint -> Gate -> Execute -> Critique -> Exit
```

If unsure, do not rush: stay in the loop and make uncertainty explicit.

## 11) Theory Anchors (Reference Only)

```text
Entropy funnel
Skip-itch suppression
K/T/B + K-self
Cognitive loop governance
Display-state externalization
```

Primary references:
- PEER v1: https://ai.vixra.org/abs/2512.0048
- PEER v2: https://ai.vixra.org/abs/2512.0058
