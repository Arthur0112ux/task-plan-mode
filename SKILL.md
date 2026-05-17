---
name: task-plan-mode
description: Evidence-driven task planning mode. Before writing anything, collect real materials — files, links, brand assets, historical content — and extract traceable facts. Output must cite specific projects, names, dates, and sources.
agent_created: true
version: 6.0.0
created: 2026-05-17
updated: 2026-05-17
references:
  - Codex Plan Mode
  - Olin's evidence-driven execution critique
---

# task-plan-mode

> **v6.0.0 — Evidence-Driven Task Execution / 证据驱动型任务执行规范**

**Not intent-driven. Evidence-driven.** The default failure mode of AI task planning is: ask generic questions → build a pretty structure → repackage the user's own words. The output looks complete but has zero information density.

This skill breaks that cycle with three hard constraints:

| Constraint / 约束 | Rule / 规则 |
|-----------------|------------|
| **Facts / 事实约束** | Never ask "what do you want?" First ask "what do you have?" Get files, links, brand assets, historical content. |
| **Evidence / 证据约束** | Every output paragraph must reference at least one traceable source: project name, date, product spec, data point, quote, image, or URL. |
| **Verification / 验证约束** | Read / extract / confirm before you write. If you can't cite a source for a claim, don't make the claim. |

---

## 1. The Problem / 问题

### 1.1 The hollow output pattern / 空心产出模式

Most AI "task planners" follow this hidden pattern:

```
1. Ask 2-3 generic questions ("who is your audience?", "what style?")
2. Build a beautiful structure (headings, sections, tables)
3. Fill it with the user's own words from step 1, slightly rephrased
```

**Result:** Looks complete. Has zero information density. No real data, no cases, no numbers, no traceable sources.

### 1.2 Root cause / 根因

The skill asks about **intent** (what do you want?) instead of **evidence** (what do you have?).

| Intent-driven (bad) | Evidence-driven (good) |
|--------------------|----------------------|
| "What topic?" | "What files, articles, or data do you have on this topic?" |
| "Who is your audience?" | "Share 2-3 past articles you liked — I'll match their tone and depth." |
| "What features?" | "Do you have a product spec sheet, brand guidelines, or screenshots?" |
| "What style?" | "What existing content (yours or a competitor's) should I reference?" |

---

## 2. Core Philosophy / 核心哲学

### 2.1 Execution flow / 执行流程

```
Before: Intent-driven                   After: Evidence-driven

"what do you want?"                     "what do you have?"
       ↓                                        ↓
  template questions                     collect materials (files, links, assets)
       ↓                                        ↓
  pretty structure                       extract evidence (facts, data, sources)
       ↓                                        ↓
  user's words rephrased                 build structure from real materials
       ↓                                        ↓
  hollow output                          verify traceability per paragraph
```

### 2.2 The rule of three / 三段式纪律

| Step / 步骤 | Action / 动作 | Skip if... / 跳过条件 |
|------------|--------------|---------------------|
| 1. Collect | Ask what materials exist. Read files, links, brand assets, historical content. Read them ALL before writing. | User says "I have nothing — just use your knowledge." |
| 2. Extract | From the collected materials, extract: specific project names, dates, product specs, data points, quotes, image descriptions, URLs. Save as evidence list. | Only 1-2 superficial sources → note "thin evidence base" and state assumptions clearly. |
| 3. Generate | Write structure + content. Every paragraph references at least one item from the evidence list. | A paragraph has zero evidence references → rewrite or delete. |

---

## 3. Phase Definitions / 阶段定义

### 3.0 Phase 0: Material Collection / 素材收集

**Before asking any requirements question, ask what materials exist.**

#### Questions to ask (not "what do you want" — but "what do you have")

| Question / 问题 | Purpose / 目的 |
|----------------|---------------|
| "Do you have existing articles or past work on this topic?" | Read for tone, depth, style reference |
| "Any brand guidelines, product spec sheets, or internal docs?" | Extract actual product/company facts |
| "Any screenshots, images, data reports, or charts I can use?" | Real visual assets, not generated filler |
| "Any competitor articles or reference links?" | Understand positioning and differentiation |
| "Any internal meeting notes or project briefs?" | Ground the output in real project context |

**If user provides nothing:**
1. Note: "No real materials provided — output will be based on general knowledge"
2. Search web for industry data on the topic
3. Label all non-sourced content clearly as `[estimated]` / `[based on general knowledge]`

#### Read everything before writing

Do not ask all questions in sequence. Ask once, get the materials, READ them, then proceed.

### 3.1 Phase 1: Evidence Extraction / 证据提取

Read every provided material and extract:

```
EVIDENCE LOG
──────────────────────────────────────
Source: [file name / URL]
  - Fact: [specific project name, date]
  - Fact: [specific data point with unit]
  - Quote: "[exact quote]"
  - Reference: [competitor / benchmark name]
  - Asset: [image / chart description]
  - Style note: [tone, format, voice observation]

Source: [next file]
  - ...
──────────────────────────────────────
```

**Rule:** Do not start writing until you have at least 5 traceable evidence items. If you don't, ask the user for more materials.

### 3.2 Phase 2: Structure from Evidence / 证据驱动的结构生成

Build the structure based on what the evidence supports, not on a generic template.

| Generic structure (bad) | Evidence-driven structure (good) |
|------------------------|--------------------------------|
| 1. Overview | 1. [Company name]'s [product] market position (from their 2025 investor deck) |
| 2. Key features | 2. Case study: [project name] deployment at [client] (from their case study PDF) |
| 3. Analysis | 3. Comparison: [Company] vs [Competitor] in [metric] (from their product spec) |
| 4. Conclusion | 4. [Specific trend] in [specific market] (from industry report they provided) |

### 3.3 Phase 3: Writing with Traceability / 可追溯写作

Every paragraph must reference at least one source.

| Without evidence (bad) | With evidence (good) |
|-----------------------|---------------------|
| "The product helps users improve efficiency." | "According to [Company]'s 2025 case study, [Client Name] reduced [metric] by 35% after adopting [Product Name]." |
| "The market is growing rapidly." | "The global [Market Name] reached $[X]B in 2025, growing at [Y]% CAGR (source: [Report name], 2025)." |
| "The design is user-friendly." | "The UI follows [Brand]'s design system (see brand guidelines, p.12). The dashboard shows [specific feature]." |

### 3.4 Phase 4: Traceability Verification / 可追溯验证

Before marking the phase complete:

```
TRACEABILITY CHECKLIST
☐ Every paragraph has at least one specific name / number / date / location
☐ Every major claim has a source (file name, URL, or user-provided material)
☐ No paragraph would still make sense if written by someone with zero knowledge of the project
☐ The output includes at least 3 traceable facts from the user's actual materials
☐ If I removed all "in general / in the industry / many companies" phrases, would anything be left?

→ If any checkbox is unchecked: rewrite the offending paragraph with evidence.
→ If all checkboxes are checked: phase is complete.
```

---

## 4. Agent Behavior / 行为规范

### 4.1 First response / 第一响应

```
Evidence-driven plan:
Phase 0: Collect materials — do you have any files, links, articles, or brand assets?
Phase 1: Extract evidence from those materials
Phase 2: Build structure from real facts
Phase 3: Write with traceable citations
Phase 4: Verify traceability

To start Phase 0: Do you have any existing materials on this topic? Past articles, product docs, screenshots, or reference links?
```

### 4.2 Material-first rule / 材料优先

**Do not** write anything substantive until the user has provided materials AND you have read them. If the user says "just write it without materials":

1. Confirm: "Without your materials, the output will be based on general knowledge only and may lack specific facts. Is that acceptable?"
2. If yes → proceed with general knowledge + web search
3. Clearly label in the output: `[general knowledge — no project-specific materials provided]`

### 4.3 Source annotation / 来源标注

Throughout the document, annotate each source:

```
[Source: user's file "brand-guidelines-2025.pdf"]
[Source: web_fetch — industry report X, 2025]
[Source: general knowledge — cite if possible]
[Estimated — no specific source found]
```

### 4.4 Self-termination / 空转终止

If after 3 rounds of asking for materials the user still hasn't provided any serious inputs:

```
I've asked for materials 3 times and haven't received project-specific inputs.
Proceeding with general knowledge only.
All non-sourced content will be marked as [estimated].
If you later provide materials, I can revise.
```

---

## 5. Default Phase Sequences / 默认阶段序列

| Type / 类型 | Phase sequence / 阶段序列 |
|-------------|--------------------------|
| Software dev | Collect → Extract → Structure → Code → Verify traceability |
| Content writing | Collect → Extract → Outline → Draft → Verify traceability |
| Research & Analysis | Collect → Extract → Data → Analysis → Verify traceability |
| Newsletter / Brief | Collect → Extract → Organize → Write → Verify traceability |
| Platform ops | Collect → Extract → Draft → Design → Verify traceability |
| Data analysis | Collect → Extract → Clean → Analyze → Verify traceability |
| Design | Collect → Extract → Concept → Refine → Verify traceability |
| Project planning | Collect → Extract → Plan → Decompose → Verify traceability |

Every sequence starts with "collect" and ends with "verify traceability."

---

## 6. Edge Cases / 边界处理

| Scenario / 场景 | Handling / 处理方式 |
|----------------|-------------------|
| User provides no materials | Default to general knowledge + web search. Mark all output as `[estimated]`. |
| Materials are all links | `web_fetch` each link. Extract evidence from fetched content. |
| Materials are local files | Use `read()` or `exec(cat)` to read. Extract evidence. |
| Materials contain brand guidelines | Extract brand voice, tone rules, visual style, key terminology. Save as style reference. |
| User provides screenshots | Describe them in alt text, reference them in writing. |
| User says "just write without collecting" | Confirm intent, then proceed with general knowledge + mark as `[general knowledge]`. |
| Evidence contradicts user's stated desire | Flag the contradiction. "Your materials say X, but you asked for Y. Which should I follow?" |
