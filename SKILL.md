---
name: task-plan-mode
description: AI Agent task planning mode — auto-classify complex tasks, execute phase-by-phase with structured requirements gathering, outputs, and completion criteria. / AI Agent 任务规划模式 — 自动识别复杂任务，按阶段执行，含结构化需求收集、产出物与完成标准。
agent_created: true
version: 4.0.0
created: 2026-05-17
updated: 2026-05-17
references:
  - Codex Plan Mode
  - task-decompose
  - plan-mode-benchmark
---

# task-plan-mode

> **v4.0.0 — AI Agent task planning behavior specification / AI Agent 任务规划行为规范**

A skill that transforms unstructured user requests into structured, phase-by-phase execution. The agent classifies the task, reveals a breakdown plan inline with the first response, and executes each phase with a defined output and completion criterion.

---

## 1. Overview / 概述

### English

When a user asks an AI agent to do something complex—build an app, write a report, analyze a market—the naive approach is a single-shot answer. This fails for three reasons:

| Failure | Why | Fix |
|---------|-----|-----|
| Context overflow | Long conversations bury early decisions | One phase at a time, document as you go |
| Direction drift | AI starts building before scope is clear | Requirements phase first, always |
| Incomplete output | User didn't specify enough to get a good result | Structured questioning, default fallbacks |

**task-plan-mode** solves all three by enforcing a predictable execution discipline.

### 中文

当用户要求 AI agent 做复杂任务时，最朴素的做法就是一榔头回答。这在三个维度上注定失败：

| 失败模式 | 原因 | 解决 |
|---------|------|------|
| 上下文溢出 | 长对话掩埋早期决策 | 一次只做一个阶段，边做边记录 |
| 方向偏差 | 范围未确定就开始做 | 永远先做需求阶段 |
| 信息不全 | 用户没给够条件 | 结构化提问 + 默认兜底 |

**task-plan-mode** 通过可预测的执行纪律解决这三个问题。

---

## 2. Decision Tree / 决策树

### 2.1 Classification / 分类

```
User request received
      │
      ▼
┌─────────────────────────────────────┐
│  Does the task require >2 steps?    │
│  任务是否需要 2 步以上？             │
└────────────┬───────────┬────────────┘
             │ Yes        │ No
             ▼            ▼
         Plan mode     Direct reply
             │
             ▼
┌─────────────────────────────────────┐
│  Match to known task type           │
│  匹配预定义任务类型                   │
└────┬──────┬──────┬──────┬──────┬────┘
     │      │      │      │      │
   dev  write research ops  design plan
```

### 2.2 Phase sequencing / 阶段序列

Every task type maps to a fixed phase sequence. The agent executes phases in order, never skipping or reordering without user direction.

| Type / 类型 | Phase sequence / 阶段序列 |
|-------------|--------------------------|
| Software dev / 软件开发 | Requirements → Frontend → Backend → Integration → Delivery |
| Content writing / 内容写作 | Requirements → Research → Outline → Draft → Polish |
| Research / 研究分析 | Requirements → Data → Analysis → Viz → Delivery |
| Newsletter / 简报 | Scope → Gather → Organize → Push |
| Platform ops / 内容平台 | Topic → Research → Draft → Design → Review |
| Data analysis / 数据分析 | Requirements → Acquire → Clean → Analyze → Viz |
| Design / 设计 | Brief → Concept → Refine → Export |
| Project planning / 项目规划 | Scope → Plan → Decompose → Risk → Package |

**Rule / 规则:** Requirements must always be Phase 1. Never start building before scope is confirmed.

---

## 3. Phase Definitions / 阶段定义

### 3.1 Software Development / 软件开发

| Phase / 阶段 | Actions / 动作 | Output / 产出 | Completion / 完成标准 |
|-------------|---------------|--------------|---------------------|
| Requirements / 需求 | Define audience, features, tech stack | plan.md + feature spec | Core features + tech choices confirmed / 核心功能与技术方案确认 |
| Frontend / 前端 | UI structure, interactions, styling | Source files | Core pages renderable / 核心页面可展示 |
| Backend / 后端 | API, data model, business logic | Code + API docs | Core endpoints functional / 核心接口可用 |
| Integration / 集成 | Frontend-backend wiring, testing | Test report + run guide | Build runs without error / 可运行 |
| Delivery / 交付 | Documentation, packaging | README + deploy guide | User can operate independently / 用户可独立使用 |

### 3.2 Content Writing / 内容写作

| Phase / 阶段 | Actions / 动作 | Output / 产出 | Completion / 完成标准 |
|-------------|---------------|--------------|---------------------|
| Requirements / 需求 | Audience, thesis, length, tone | plan.md | Direction confirmed / 方向确认 |
| Research / 资料 | Search, collect references | Reference doc | Material ready / 素材到位 |
| Outline / 大纲 | Structure, chapter breakdown | Outline doc | Structure confirmed / 结构确认 |
| Draft / 正文 | Write chapters | Full draft | Draft complete / 文章完成 |
| Polish / 排版 | Format, proofread, add visuals | Final doc | Ready to publish / 可发布 |

### 3.3 Research & Analysis / 研究分析

| Phase / 阶段 | Actions / 动作 | Output / 产出 | Completion / 完成标准 |
|-------------|---------------|--------------|---------------------|
| Requirements / 需求 | Question, scope, methodology | plan.md | Research plan confirmed / 方案确认 |
| Data / 数据 | Gather industry data, trends | Data summary | Key data acquired / 数据到位 |
| Analysis / 分析 | Breakdown, comparison, conclusions | Report body | Analysis complete / 分析完成 |
| Viz / 图表 | Charts, graphs, images | Visuals + captions | Visuals ready / 图文齐备 |
| Delivery / 交付 | Final review, formatting | Final report | Deliverable / 可交付 |

### 3.4 Newsletter / Daily Briefing / 简报

| Phase / 阶段 | Actions / 动作 | Output / 产出 | Completion / 完成标准 |
|-------------|---------------|--------------|---------------------|
| Scope / 范围 | Topic, coverage | Scope confirmed | Topic clear / 主题明确 |
| Gather / 搜集 | Search latest info | Item list | 5-8 items / 5-8 条信息 |
| Organize / 组织 | Categorize, summarize | Brief body | Content complete / 内容完成 |
| Push / 推送 | Deliver to user | Message | Delivered / 已送达 |

### 3.5 Content Platform Operations / 内容平台运营

| Phase / 阶段 | Actions / 动作 | Output / 产出 | Completion / 完成标准 |
|-------------|---------------|--------------|---------------------|
| Topic / 选题 | Angle, hook | Topic brief | Direction confirmed / 方向确定 |
| Research / 资料 | Data, cases, references | Reference doc | Material ready / 素材到位 |
| Draft / 初稿 | Write body | Article draft | Draft complete / 初稿完成 |
| Design / 设计 | Cover image, layout | Formatted article | Ready to publish / 可发布 |
| Review / 审核 | Check links, formatting | Final review | All clear / 确认无误 |

### 3.6 Data Analysis / 数据分析

| Phase / 阶段 | Actions / 动作 | Output / 产出 | Completion / 完成标准 |
|-------------|---------------|--------------|---------------------|
| Requirements / 需求 | Goal, data sources | plan.md | Goal confirmed / 目标明确 |
| Acquire / 获取 | Download, scrape, query | Dataset | Data acquired / 数据到位 |
| Clean / 清洗 | Format, handle anomalies | Cleaned data | Ready to analyze / 可分析 |
| Analyze / 分析 | Statistics, modeling | Results | Conclusions drawn / 结论产出 |
| Viz / 可视化 | Charts, dashboards | Visuals + annotations | Presentable / 可展示 |

### 3.7 Design / 设计

| Phase / 阶段 | Actions / 动作 | Output / 产出 | Completion / 完成标准 |
|-------------|---------------|--------------|---------------------|
| Brief / 需求 | Goals, style, use cases | Design brief | Direction confirmed / 方向确认 |
| Concept / 概念 | Creative direction | Concept draft | Direction selected / 方向选定 |
| Refine / 细化 | Polish colors, typography | Final design | Details complete / 细节完成 |
| Delivery / 交付 | Source files, exports | Design package | Ready to use / 可投入使用 |

### 3.8 Project Planning / 项目规划

| Phase / 阶段 | Actions / 动作 | Output / 产出 | Completion / 完成标准 |
|-------------|---------------|--------------|---------------------|
| Scope / 范围 | Goals, constraints | Project brief | Scope defined / 范围确定 |
| Plan / 方案 | Architecture, roadmap | Plan doc | Feasible / 方案可行 |
| Decomposition / 分解 | Milestones, timeline | Execution plan | Actionable / 可落地 |
| Risk / 风险 | Edge cases, fallbacks | Risk register | Known risks covered / 风险覆盖 |
| Package / 交付 | Complete plan | Final plan | Ready for review / 可评审 |

---

## 4. Agent Behavior Specification / 行为规范

### 4.1 First response / 第一响应

**Must include:** phase plan + first requirement question in a single output.

**Must not:** ask for approval before proceeding. The plan is informative. If the user disagrees, they will say so.

**Format:**
```
Phase plan:
1. [Phase name] — [scope]
2. [Phase name] — [scope]
...

Starting with Phase 1: [specific question about Phase 1]?
```

### 4.2 Requirements gathering / 需求收集

- One question per turn
- Max 2 follow-ups per question. If user cannot answer → provide a sensible default → mark as `confirmed_by_default`

### 4.3 Phase transition / 阶段切换

After each phase, output a completion report:

```
[Phase N/M done] — [phase name]
Output: [file / doc name]
Next: [Phase N+1]
Phase: N/M
```

Wait for user acknowledgment before proceeding to the next phase. If user is silent → proceed after 30 seconds.

### 4.4 Allowed operations / 可执行操作

| Operation / 操作 | When / 何时使用 |
|-----------------|----------------|
| Retrieve information (web_fetch, search) | Research / Data phases |
| Create / edit documents | All phases |
| Generate code | Dev phases |
| Generate images | Design / Viz phases |
| Validate output | Integration / Review phases |

### 4.5 Completion criteria / 完成标准

**Phase complete / 阶段完成:**
- Output artifact produced / 产出物已生成
- Completion criteria from section 3 met / 阶段完成标准已达
- User can verify the output / 用户可验证

**Task complete / 任务完成:**
- All phases marked `done`
- Final deliverable usable without further processing / 最终产出可直接使用
- User notified / 已通知用户

---

## 5. Edge Cases / 边界处理

| Scenario / 场景 | Handling / 处理方式 |
|----------------|-------------------|
| User says "just do it, no planning" | Skip plan mode, execute directly / 跳过规划，直接执行 |
| User interrupts mid-phase | Stop current phase, handle interruption, resume or re-plan / 中断当前阶段，处理打断，恢复或重计划 |
| Requirements unclear after 2 rounds | Default suggestion + `confirmed_by_default` tag / 默认建议 + 标记 |
| Multi-agent dispatch needed | Split phases across agents, collect outputs, merge / 分阶段分配给多个 agent，汇总产出 |
| User silent for > 30s after phase report | Proceed to next phase autonomously / 自动进入下一阶段 |
| Task type unknown | Generate dynamic phase sequence from first principles / 从基本原则动态生成阶段序列 |

---

## 6. Example / 示例

### Scenario: "Write a report on EV market trends in 2026"

**Agent (matching → Research & Analysis, section 3.3):**

```
Phase plan:
1. Requirements — audience, scope, key questions
2. Data collection — industry data, policy, trends
3. Analysis — structured breakdown, comparison, conclusions
4. Visualization — charts, graphs
5. Delivery — final report

Starting with Phase 1: Who is the audience for this report — internal stakeholders or public readers?
```

**On completion of Phase 1:**

```
[Phase 1/5 done] — Requirements
Output: plan.md (audience: public report, scope: global EV market 2025-2026, focus: battery tech and policy)
Next: Phase 2 — Data collection
Phase: 1/5
```
