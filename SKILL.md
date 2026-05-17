---
name: task-plan-mode
description: When an agent receives a complex task, it enters plan mode: auto-classifies the task type, reveals an execution plan, and executes phase by phase with progress reporting.
agent_created: true
version: 3.2.0
created: 2026-05-17
updated: 2026-05-17
references:
  - Codex Plan Mode
  - task-decompose
---

# task-plan-mode

> **Specification v3.2.0 — AI Agent task planning behavior.**

When a user proposes a task involving >2 steps, missing critical context, or an ambiguous goal, the agent self-triggers into **plan mode**: it classifies the task, outputs a phase breakdown, and executes sequentially—one phase at a time—with a completion report after each.

No explicit approval step is required. The plan is presented inline with the first response.

---

## 1. Trigger Conditions

### 1.1 Automatic triggers

| Pattern | Example |
|---------|---------|
| Complex verb + deliverable noun | "Build a second-hand book trading mini-app" |
| >2 implicit steps | "Write a report on EV battery trends" |
| Missing scope/audience/context | "Help me make something about AI" |
| Domain-specific keywords | "Design a landing page / Analyze the market" |

### 1.2 Manual triggers

- `plan mode`
- `帮我拆解`
- `先规划一下`

---

## 2. Task Type Reference

The agent classifies the task against this table and executes the matching phase sequence.

### 2.1 Software Development

| Phase | Actions | Output | Completion Criteria |
|-------|---------|--------|--------------------|
| Requirements | Define target audience, feature list, tech stack | plan.md + feature spec | Core features + tech choices confirmed |
| Frontend | Implement UI structure, interactions, styling | Source files | Core pages renderable |
| Backend | API design, data model, business logic | Backend code + API docs | Core endpoints functional |
| Integration | Frontend-backend wiring, smoke testing | Test report + run guide | Build runs without error |
| Delivery | Documentation, packaging | README + deploy guide | User can operate independently |

### 2.2 Content Writing

| Phase | Actions | Output | Completion Criteria |
|-------|---------|--------|--------------------|
| Requirements | Define audience, thesis, length, tone | plan.md | Writing direction confirmed |
| Research | Search, collect references, extract data | Reference doc | Material ready |
| Outline | Structure, chapter breakdown | Outline doc | Chapter structure confirmed |
| Draft | Write chapters sequentially | Full draft | Draft complete |
| Polish | Format, proofread, add visuals | Final doc | Ready to publish |

### 2.3 Research & Analysis

| Phase | Actions | Output | Completion Criteria |
|-------|---------|--------|--------------------|
| Requirements | Define research question, scope, methodology | plan.md | Research plan confirmed |
| Data collection | Gather industry data, policy, trends | Data summary | Key data points acquired |
| Analysis | Structured breakdown, comparison, conclusions | Report body | Analysis complete |
| Visualization | Charts, graphs, supporting images | Visuals + captions | Visuals ready |
| Delivery | Final review, formatting | Final report | Deliverable |

### 2.4 Newsletter / Daily Briefing

| Phase | Actions | Output | Completion Criteria |
|-------|---------|--------|--------------------|
| Requirements | Define topic scope, coverage | Scope confirmed | Topic clear |
| Gather | Search latest information | Item list | 5-8 items collected |
| Organize | Categorize, summarize, comment | Brief body | Content complete |
| Push | Deliver to user | Message | Delivered |

### 2.5 Content Platform Operations

| Phase | Actions | Output | Completion Criteria |
|-------|---------|--------|--------------------|
| Topic selection | Define angle, hook | Topic brief | Direction confirmed |
| Research | Data, cases, references | Reference doc | Material ready |
| Draft | Write body | Article draft | Draft complete |
| Design | Cover image, inline visuals, layout | Formatted article | Ready to publish |
| Review | Check links, formatting, typos | Final review | All clear |

### 2.6 Data Analysis & Visualization

| Phase | Actions | Output | Completion Criteria |
|-------|---------|--------|--------------------|
| Requirements | Define analysis goal, data sources | plan.md | Goal confirmed |
| Acquisition | Download, scrape, query | Dataset | Data acquired |
| Cleaning | Format, handle anomalies | Cleaned data | Ready to analyze |
| Analysis | Statistics, comparison, modeling | Results | Conclusions drawn |
| Visualization | Charts, dashboards | Visuals + annotations | Presentable |

### 2.7 Design

| Phase | Actions | Output | Completion Criteria |
|-------|---------|--------|--------------------|
| Requirements | Goals, style references, use cases | Design brief | Direction confirmed |
| Concept | Creative direction, initial approach | Concept draft | Direction selected |
| Refinement | Polish colors, typography, details | Final design | Detail complete |
| Delivery | Source files, exports, specs | Design package | Ready to use |

### 2.8 Project Planning

| Phase | Actions | Output | Completion Criteria |
|-------|---------|--------|--------------------|
| Requirements | Goals, scope, constraints | Project brief | Scope defined |
| Design | Architecture, roadmap, resource estimate | Plan doc | Feasible plan |
| Decomposition | Milestones, assignments, timeline | Execution plan | Actionable |
| Risk assessment | Edge cases, fallbacks | Risk register | Known risks addressed |
| Delivery | Complete plan package | Final plan | Ready for review |

---

## 3. First Response Behavior

Upon receiving a complex task, the agent:

1. Matches the task to one of the 8 types above
2. Outputs the phase plan **and** the first requirement question in a single response

### Format

```
Phase plan:
1. [Phase name] — [what it covers]
2. ...
N. [Phase name]

Starting with Phase 1: [first question to user]?
```

### Rules

- Do not pause to ask "may I proceed?"—the plan is informative, not negotiative
- If the user disagrees, they will naturally interrupt
- Default: proceed as planned

---

## 4. Phase Execution

### 4.1 Requirements gathering

- One question per turn
- Maximum 2 follow-ups per question—if the user cannot answer, provide a default and mark as `confirmed_by_default`

### 4.2 Phase completion report

After each phase, the agent outputs:

```
[Phase N/M done] — [phase name]
Output: [file or output name]
Next: [Phase N+1]
Phase: N/M
```

### 4.3 Completion criteria

**A phase is complete when:**
- Its output artifact has been produced
- The completion criteria from section 2 have been met
- The user can verify the output

**The full task is complete when:**
- All phases are `done`
- The final deliverable is usable without further processing
- The user has been notified

---

## 5. Workspace (when used)

Optional workspace structure for persistent planning artifacts:

```
.plan-mode/
├── plan.md
├── requirements/
├── phase-output/
└── deliverables/
```
