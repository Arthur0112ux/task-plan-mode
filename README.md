# task-plan-mode — AI Agent Task Planning Mode 🎯

<p align="center">
  <a href="https://github.com/Arthur0112ux/task-plan-mode/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"></a>
  <a href="https://clawhub.ai/skills/task-plan-mode"><img src="https://img.shields.io/badge/clawhub-available-brightgreen" alt="ClawHub"></a>
  <a href="https://github.com/Arthur0112ux/task-plan-mode/releases"><img src="https://img.shields.io/github/v/release/Arthur0112ux/task-plan-mode" alt="Version"></a>
  <a href="https://github.com/Arthur0112ux/task-plan-mode"><img src="https://img.shields.io/github/stars/Arthur0112ux/task-plan-mode?style=flat" alt="GitHub Stars"></a>
</p>

> **Give your AI Agent Codex-like Plan Mode: auto-detect complexity, break down tasks, execute phase by phase.**

---

## What It Does

When a user proposes a complex task (build a website, write a report, design a system), the agent:

1. **Recognizes** task complexity and maps it to a standard execution template
2. **Reveals the plan** as part of the first response — no pause for approval
3. **Executes phase by phase**, reporting progress after each
4. **Delivers** when all phases are complete

No separate "can I proceed?" step. Plans unfold as the conversation flows, just like Codex Plan Mode.

---

## Quick Start

```bash
npx clawhub@latest install task-plan-mode
```

Once installed, the skill activates **automatically** when a user says:

> "Build me a second-hand book trading mini-program"
> "Write a report on EV battery trends"
> "Design a landing page for our product"

Or **manually** by typing: `Plan Mode` / `plan mode` / `帮我拆解`

---

## Default Task Types

| Category | Phases |
|----------|--------|
| **Software Development** | Requirements → Frontend → Backend → Integration → Delivery |
| **Content Writing** | Requirements → Research → Outline → Draft → Polish |
| **Research & Analysis** | Requirements → Data Collection → Analysis → Viz → Delivery |
| **Newsletter / Briefing** | Scope → Gather → Organize → Push |
| **Content Platform** | Topic → Research → Draft → Design → Review |
| **Data Analysis** | Requirements → Acquire → Clean → Analyze → Visualize |
| **Design** | Brief → Concept → Refine → Export |
| **Project Planning** | Scope → Blueprint → Milestones → Risk → Package |

Each phase specifies **what to produce** and **completion criteria**.

---

## How It Works

```
User: "Write a report on EV market trends in 2026"

Agent (matching → Research & Analysis):
→ "Got it. I'll work through 5 phases:
   ① Requirements — audience & scope
   ② Data collection — industry data & trends
   ③ Analysis — structured breakdown
   ④ Charts & visuals
   ⑤ Delivery
   
   Let's start with Phase 1: Who is this report for — internal stakeholders or public?"
```

---

## Project Structure

```
task-plan-mode/
├── SKILL.md              ← Full skill definition (core)
├── package.json          ← npm/ClawHub metadata
├── clawhub.json          ← ClawHub config
├── CHANGELOG.md          ← Version history
├── README.md             ← This file
├── README_EN.md          ← English readme
├── LICENSE               ← MIT
├── docs/                 ← Design docs
│   ├── design-principles.md
│   └── triggers.md
└── examples/             ← Usage examples
```

---

## License

MIT — use, modify, distribute freely.
