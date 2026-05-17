---
name: task-plan-mode
description: AI Agent task planning mode — auto-classify complex tasks, execute phase-by-phase with deep context research, non-generic requirements gathering, and data-driven output.
agent_created: true
version: 5.0.0
created: 2026-05-17
updated: 2026-05-17
references:
  - Codex Plan Mode
  - task-decompose
  - plan-mode-benchmark
---

# task-plan-mode

> **v5.0.0 — AI Agent task planning behavior specification / AI Agent 任务规划行为规范**

A skill that transforms unstructured user requests into structured, phase-by-phase execution — with real context research, non-generic requirements, and data-driven output.

**Core principle / 核心原则:** Knowing "what to do" is not enough. The skill must also tell the agent "how to dig deeper, where to find data, and how to detect shallow output."

---

## 1. The Problem / 为什么需要这个模式

### English

When a user asks an AI agent to do something complex, the naive approach produces:

| Failure | Symptom | Root Cause |
|---------|---------|------------|
| Generic requirements | "Who is your audience?" → "Tech readers" — no depth | No context research before asking |
| Empty framework | Output has structure but no real content | Agent fills templates, not actual work |
| No data | Report with no citations, no numbers, no references | Agent never looked up external sources |

**task-plan-mode** solves all three by enforcing:
1. **Phase 0: Context research** — always look up the user's context before asking anything
2. **Structured deepening** — don't accept generic answers; push for specifics
3. **Data-driven output** — every deliverable must cite real sources

### 中文

当用户要求 AI agent 做复杂任务时，默认做法会产生三种通病：

| 失败模式 | 表象 | 根本原因 |
|---------|------|---------|
| 需求模板化 | "目标读者是谁？"→"技术读者"——问了等于没问 | 问之前没做过背景研究 |
| 框架感 | 有结构没内容，全是套话 | AI 填模板，不是真做事 |
| 无数据引用 | 报告没有出处、没有数据、没有参考资料 | AI 从来没搜过外部信息 |

**task-plan-mode** 通过三条纪律解决：
1. **Phase 0: 背景研究** — 问任何问题之前，先搜用户背景
2. **结构化深挖** — 不接受泛泛答案，持续追问到具体
3. **数据驱动产出** — 每个交付物必须引用真实来源

---

## 2. Decision Tree / 决策树 + 上下文感知

### 2.1 Classification with context / 带上下文感知的分类

```
User request received
      │
      ▼
┌────────────────────────────────────────────┐
│  Phase 0: Context Research (NEW!)          │
│  Before asking anything, search for:       │
│  - User's company / brand / past work      │
│  - Mentioned domain / industry trends      │
│  - Any links or references in the request  │
│                                            │
│  Tools: web_fetch(user's links)            │
│         exec(curl search) for industry     │
└────────────────────┬───────────────────────┘
                     │
                     ▼
┌────────────────────────────────────────────┐
│  Does the task require >2 steps?           │
└────────────┬───────────┬───────────────────┘
             │ Yes        │ No
             ▼            ▼
         Plan mode     Direct reply
```

### 2.2 Phase sequencing with depth / 带深度的阶段序列

| Type / 类型 | Phase sequence / 阶段序列 | Deep execution note / 深度执行要点 |
|-------------|--------------------------|-----------------------------------|
| Software dev | R → Front → Back → Integ → Del | Before coding, web_fetch similar projects for reference |
| Content writing | Context → R → Research → Outline → Draft → Polish | Before drafting, search for actual data / quotes / cases |
| Research & Analysis | Context → R → Data → Analysis → Viz → Del | Every data point must be from a real source |
| Newsletter / Brief | Context → Scope → Gather → Org → Push | Gather from real feeds, not generated filler |
| Platform ops | Context → Topic → Research → Draft → Design → Review | Search author's past content for tone consistency |
| Data analysis | Context → R → Acquire → Clean → Analyze → Viz | Real datasets only |
| Design | Context → Brief → Concept → Refine → Export | Search for style references |
| Project planning | Context → Scope → Plan → Decompose → Risk → Pkg | Search for actual competitive landscape |

**Rule / 规则:** Phase 0 (Context Research) is mandatory for all task types. Skip only if user says "no research needed."

---

## 3. Phase 0: Context Research / 背景研究（新增，强制）

### 3.1 What to search for / 搜什么

Before asking a single question, search for:

| Target / 搜索目标 | Tool / 工具 | Example / 示例 |
|------------------|------------|---------------|
| Any links the user provided in the request | `web_fetch(url)` | User says "write about our product ev-charge-x" → web_fetch their product page |
| User's company / brand / past content | `exec(curl)` search or known source | "柳工" → search for brand info, recent news |
| Domain-specific context | `web_fetch` or search API | "具身智能 2025 趋势" → gather latest data |
| Reference materials | `web_fetch` links | Academic papers, competitor products |

### 3.2 Output / 产出

A **context summary** (saved as `plan.md` context section) containing:

- What I found about the user's context
- Key data points / quotes / references I can use
- What information is still missing that I need to ask

### 3.3 Anti-pattern / 反模式

**Do NOT** ask questions that could have been answered by 30 seconds of web searching.

| Bad (don't do this) | Good (do this instead) |
|--------------------|----------------------|
| "What does Liugong do?" | "I found Liugong is a construction machinery manufacturer based in Liuzhou. Their core products include loaders, excavators, and rollers. Should I focus on their EV transition or their smart construction initiatives?" |
| "Who is the audience of 电铲研讯?" | "I found 电铲研讯 covers new energy vehicles, energy storage, smart hardware, and embodied intelligence. Typical readers are industry professionals and tech enthusiasts. For this article, should I write at a professional or enthusiast level?" |
| "What data do you need?" | "I searched for embodied AI market data 2025 and found a report forecasting $xxB by 2030. I'll use this as a starting point and add more sources as I go." |

---

## 4. Phase Definitions / 阶段定义（带深度指引）

### 4.1 Requirements gathering / 需求收集

#### 4.1.1 Before asking / 问之前

Always complete Phase 0 (context research) first. Your questions should demonstrate you've done your homework.

#### 4.1.2 Deep questioning pattern / 深挖式提问

Don't accept generic answers. Push for specifics:

| Template question / 模板 | Deep follow-up / 深挖追问 |
|--------------------------|-------------------------|
| "Who is the target user?" → they say "tech readers" | "Specifically, which tech readers? CTOs making purchase decisions, or developers building with it? Their reading depth and pain points are very different." |
| "What are the key features?" → they list 3 | "If you had to prioritize by user pain, which feature solves the biggest real problem? Can you describe a scenario where a user would choose this over competitors?" |
| "What style?" → they say "professional" | "What's a WeChat article from 电铲研讯 you liked? I'll match that tone." |

#### 4.1.3 Auto-enhancement rule / 自动增强规则

If after 3 rounds the user's answers are still generic → the agent must:
1. Recognize: "I'm getting generic answers, I need to do my own research"
2. Search independently for the topic
3. Present findings to the user: "I found some specific data. Let me use this to fill in the gaps."

### 4.2 Research / Data collection / 资料搜集

**Must use real sources. Never fabricate data.**

| Type / 类型 | Where to look / 去哪找 |
|-------------|----------------------|
| Industry data | `web_fetch` industry reports, news, government stats |
| Company info | Company website, news, investor presentations |
| Academic papers | arXiv, Nature, Google Scholar |
| Market trends | News aggregators, HN, analyst reports |
| User's past content | Author's public articles, social media |

**Each source must be cited in the output.** If a source is unavailable, note it: "No public data found for X — using estimated range Y-Z based on comparable industries."

### 4.3 Drafting / Output / 撰写产出

**The output must contain real content, not just structure.**

Before marking a phase complete, self-check:

```
Quality checklist:
☐ Does this contain at least 3 specific data points / quotes / examples?
☐ Did I cite real sources for each major claim?
☐ If someone read just the output, would they learn something new?
☐ Could this be mistaken for an AI template? (If yes → rewrite.)
```

If the output is "框架感" (framework-like, hollow), the agent must:
1. Delete the filler
2. Find real data to replace it
3. Or ask the user: "I have the structure but the content feels hollow. Can you point me to a specific case or data source I should use?"

---

## 5. Phase Transition / 阶段切换

After each phase, output a completion report:

```
[Phase N/M done] — [phase name]
Output: [file / doc name]
Real sources used: [count]
Next: [Phase N+1]
Phase: N/M
```

Wait for user acknowledgment. If user is silent → proceed after 30 seconds.

---

## 6. Edge Cases / 边界处理

| Scenario / 场景 | Handling / 处理方式 |
|----------------|-------------------|
| User says "just do it, no planning" | Skip Phase 0 + Requirements, but still do context research silently |
| User gives generic answers for 3+ rounds | Auto-research mode: stop asking, find data yourself, present findings |
| No real data available publicly | Note "no public data found" + provide estimated range + mark as `estimated` |
| User interrupts mid-phase | Stop, handle interruption, resume or re-plan |
| Multi-agent dispatch | Assign phases, each agent does its own Phase 0 context research |
| User silent after phase report | Proceed to next phase after 30s |
| Task type unknown | Generate dynamic phase sequence + research context first |

---

## 7. First Response Format / 第一响应

```
Phase 0 complete — context researched: [what I found]
Plan:
1. [Phase] — [specific scope derived from context]
2. ...

Starting with Phase 1: [context-aware question]?
```

**Before:**
> "Who is your target audience?"

**After (with Phase 0):**
> "I looked up 电铲研讯's recent articles — your readers are tech industry professionals following new energy and smart hardware. For this article on embodied AI, should I write at a professional analysis level (deeper, more technical) or a broader industry overview level (more accessible)?"
