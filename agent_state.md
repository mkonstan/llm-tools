# Agent State

**Version:** 1
**Updated:** <!-- YYYY-MM-DD — update on every write -->
**Purpose:** Session continuity. Read this on every session start. Update before session end.

---

## I. What This Is

<!-- 2-4 sentences: What are we building/investigating/solving? For whom? What's the end state?
     Then immediately state what it is NOT — the most likely misunderstanding a fresh agent would have. -->

**Project:** <!-- one-line description -->
**It is NOT:** <!-- the thing a fresh agent would wrongly assume -->

---

## II. Current State

<!-- Where are we? What's done, what's next, what's blocked?
     Use numbered steps with completion markers for multi-step work. -->

```
Step 1: [description]                    ✅ DONE
Step 2: [description]                    ✅ DONE  
Step 3: [description]                    ← CURRENT
Step 4: [description]
```

**Blocked:** <!-- anything waiting on external input, or "Nothing" -->

---

## III. Decisions

<!-- Numbered. Each with WHY — what was rejected, what would go wrong if reversed.
     New decisions append. Don't edit old ones. Override with "Overrides D[N]". -->

### D1: <!-- Decision statement -->
**Why:** <!-- What failed or was rejected. What alternative was considered. What breaks if reversed. -->

---

## IV. Artifacts

<!-- What files exist? Where? What's their status? Mark retired files explicitly. -->

| File | Purpose | Status |
|------|---------|--------|
| `AGENTS.md` | Cognitive scaffolding protocol | ✅ Active |
| `agent_state.md` | This file — session state | ✅ Active |
<!-- | `filename` | description | ✅ Complete / 🔧 Draft / ❌ Retired | -->

---

## V. Anti-Drift Warnings

<!-- Each warning targets a specific observed or predicted failure.
     Tag each: [observed] = actually happened, [predicted] = likely based on project type.
     Format: What you'll wrongly think → what's actually true. -->

1. **<!-- The specific mistake -->** <!-- [observed] or [predicted] -->
   <!-- What you'll think → what's actually true. If you catch yourself [behavior] → stop, reread D[N]. -->

---

## VI. What NOT To Do

<!-- Absolute prohibitions. Reserve for actions that are catastrophic and irreversible. 
     Skip this section if the project has no catastrophic failure modes. -->

1. **Never** <!-- prohibited action --> — <!-- why this is catastrophic -->

---

## VII. Open Questions

<!-- Unresolved issues. Skip if none exist. Don't fabricate for completeness. -->

| Question | What Would Answer It | Priority |
|----------|---------------------|----------|
| <!-- issue --> | <!-- evidence or action needed --> | High/Medium/Low |

---

## VIII. Recovery Pointer

<!-- One location, one action. The agent reads the full document for context, then follows this pointer. -->

**You are HERE:** <!-- Section → Step → Specific task -->
**Do THIS next:** <!-- One sentence — the immediate next action -->

---

<!-- 
MAINTENANCE RULES:
- Update immediately after decisions or state changes
- Don't batch updates — context loss doesn't wait  
- Version the header on each meaningful update
- This is the SINGLE source of truth — no parallel state documents
-->
