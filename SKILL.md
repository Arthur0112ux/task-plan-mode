---
name: task-plan-mode
description: Plan → Implement → Verify. Every phase has three layers: define what to do + how to verify, execute, then check before proceeding. No more linear hollow output.
agent_created: true
version: 7.0.0
created: 2026-05-17
updated: 2026-05-17
references:
  - Codex Plan Mode (Plan → Implement → Verify)
  - cgbarlow/protocols (non-negotiable protocols pattern)
  - Olin's evidence-driven execution critique
---

# task-plan-mode

> **v7.0.0 — Three-layer execution: Plan → Implement → Verify**

Every phase has three layers. Not "ask → do → next." But **Plan → Implement → Verify → next.**

---

## 1. Why Three Layers / 为什么需要三层

### The old pattern (wrong)

```
Question → Answer → Output → Next
```

Linear. No verification. No decision traceability. The output could be anything and there's no way to check if it's right.

### The three-layer pattern (correct)

```
┌─────────────────────────────────────────┐
│  PLAN                                    │
│  • What to do (specific)                 │
│  • What the output should be             │
│  • How to verify it's correct            │
└─────────────┬───────────────────────────┘
              ▼
┌─────────────────────────────────────────┐
│  IMPLEMENT                               │
│  • Execute the plan                      │
│  • Produce the output                    │
└─────────────┬───────────────────────────┘
              ▼
┌─────────────────────────────────────────┐
│  VERIFY                                  │
│  • Check output against plan             │
│  • Did we meet verification criteria?    │
│  • Yes → next phase / No → revise        │
└─────────────────────────────────────────┘
```

---

## 2. Root Cause / 根因分析

Past versions failed because they only defined **what** (phases, tools, outputs) but never **how to verify correctness**.

| Version | Missing |
|---------|---------|
| v1-v3 | Only phase sequence. No execution depth. |
| v4 | Added tools, but still linear ask→do. |
| v5-v6 | Added evidence-driven collection. Better, but still missing a verification gate at each phase. |
| **v7** | **Plan → Implement → Verify. Every phase. Always.** |

---

## 3. The Three Layers / 三层详解

### 3.1 PLAN layer

Before doing anything in a phase, the agent must output:

```
PLAN for [phase name]:
  • Goal: [one-sentence: what needs to be true after this phase]
  • Output: [specific deliverable — file, document, code, answer]
  • Verify: [how to check the output is correct — 2-3 concrete criteria]
```

**Rules:**
- The plan must be specific to this task, not a template
- The verification criteria must be objective (checkable by another agent or the user)
- If you can't define verification criteria, you don't understand the phase well enough

### 3.2 IMPLEMENT layer

Execute the plan. Produce the output.

### 3.3 VERIFY layer

After implementing, check against the plan:

```
VERIFY for [phase name]:
  • Criteria 1: [specific check] → ✅ / ❌
  • Criteria 2: [specific check] → ✅ / ❌
  • Criteria 3: [specific check] → ✅ / ❌
  
  Result: [PASS → next phase] / [FAIL → revise]
```

**Rules:**
- If any criteria fails → revise the output, don't skip to next phase
- If revision isn't possible → escalate to user: "Output doesn't meet criteria because [reason]. Options: A) relax criteria, B) change approach, C) get more data"

---

## 4. Full Workflow / 完整流程

```
User request
      ↓
┌─────────────────────┐
│  OVERALL PLAN        │
│  (Phase-level plan)  │
│  Phase 1: Plan/Imp/Vfy│
│  Phase 2: Plan/Imp/Vfy│
│  ...                 │
└──────────┬──────────┘
           ▼
┌─────────────────────────────────────────┐
│  PHASE 1                                 │
│  │ PLAN                                 │
│  │  - Goal, Output, Verify              │
│  │ IMPLEMENT                            │
│  │  - Do the work                       │
│  │ VERIFY                               │
│  │  - Check criteria → PASS/FAIL        │
│  │  If FAIL → revise or escalate        │
└──────────┬──────────────────────────────┘
           ▼ (PASS)
┌─────────────────────────────────────────┐
│  PHASE 2                                 │
│  │ PLAN                                 │
│  │  - Goal, Output, Verify              │
│  │ ...                                   │
└─────────────────────────────────────────┘
```

---

## 5. Example / 完整示例

### Task: "Build me a personal portfolio website"

**Phase 1 — Requirements**

```
PLAN for Phase 1 (Requirements):
  • Goal: Understand what content and style the user wants
  • Output: A written requirements brief with 3+ confirmed decisions
  • Verify: 
    1. All 3 core decisions are made (content type, project format, style direction)
    2. Each decision has a specific answer, not "I don't know yet"
    3. The brief is detailed enough to start coding

── IMPLEMENT ──

[ask questions one at a time, with options]

User picks: B (portfolio, screenshots + one line, dark tech)

→ Write requirements brief

── VERIFY ──

  1. Content type: portfolio → ✅
  2. Project format: screenshot + one line → ✅
  3. Style: dark tech → ✅

  Result: PASS → next phase
```

**Phase 2 — Generate**

```
PLAN for Phase 2 (Generate HTML):
  • Goal: A working HTML file matching the requirements
  • Output: index.html with hero, gallery, contact
  • Verify:
    1. HTML renders without errors (valid tags, no console errors)
    2. Matches all 3 requirements from Phase 1
    3. Responsive on mobile and desktop

── IMPLEMENT ──

[Write the HTML file]

── VERIFY ──

  1. Valid HTML structure → ✅
  2. Dark theme, portfolio grid, screenshot+text cards → ✅
  3. Mobile responsive (media queries present) → ✅

  Result: PASS → deliver
```

---

## 6. Phase Sequences with Verification / 带验证的阶段序列

Each type now includes verification criteria for each phase.

### Software Development

| Phase | Plan (Goal + Output + Verify) |
|-------|------------------------------|
| Requirements | Goal: clear spec. Output: brief with 3+ decisions. Verify: each decision has a concrete answer, not "I don't know" |
| Frontend | Goal: working UI. Output: runnable HTML/CSS. Verify: renders correctly, matches spec, responsive |
| Backend | Goal: functional API. Output: code with tests. Verify: all tests pass, API responds to sample calls |
| Integration | Goal: end-to-end working. Output: integrated system. Verify: frontend calls backend, data flows correctly |
| Delivery | Goal: deployable. Output: README + run guide. Verify: a fresh clone can run it |

### Content Writing

| Phase | Plan (Goal + Output + Verify) |
|-------|------------------------------|
| Research | Goal: enough material. Output: evidence log (5+ facts from real sources). Verify: each fact has traceable source |
| Outline | Goal: clear structure. Output: chapter-by-chapter outline. Verify: each chapter has a purpose, not filler |
| Draft | Goal: complete draft. Output: full article. Verify: minimum 3 traceable facts per major claim, zero filler paragraphs |
| Polish | Goal: ready to publish. Output: final doc. Verify: readability score, formatting, citation accuracy |

### All other types

Follow the same pattern: each phase must define **Goal + Output + Verify** before execution.

---

## 7. Verification Failure Handling / 验证失败处理

| Scenario | Action |
|----------|--------|
| 1 of 3 criteria fails | Fix that criteria, re-verify |
| All 3 fail | Phase plan was wrong → re-plan the phase |
| Cannot fix without new user input | Escalate: "Can't pass verify because [reason]. Options: A) [option 1], B) [option 2]" |
| User says "skip verify, it's fine" | Mark phase as `verified_skipped_by_user` |
| Multiple phases fail verification | Overall plan may be wrong → return to overall planning |

---

## 8. First Response Format / 第一响应

```
Phase plan:
  1. [Phase] — Plan → Implement → Verify
  2. [Phase] — Plan → Implement → Verify
  3. [Phase] — Plan → Implement → Verify

Starting Phase 1:

PLAN for Phase 1 ([name]):
  • Goal: ...
  • Output: ...
  • Verify:
    1. [criteria]
    2. [criteria]
    
Let's begin. [First question]?
```

---

## 9. Edge Cases / 边界

| Scenario | Handling |
|----------|---------|
| User says "just do it, skip planning" | Overall plan only (no per-phase plan), but still verify |
| User interrupts during Implement | Stop, handle, resume from current verify state |
| Cannot objectively verify (e.g., "does it look good?") | State subjective criteria: "I will check [specific thing]. For taste decisions, user will confirm." |
| Multi-phase task | Each phase has its own Plan/Implement/Verify. Phase N's verify may depend on Phase N-1's output. |
