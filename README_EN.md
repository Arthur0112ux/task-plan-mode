# task-plan-mode — Plan Mode for AI Agents 🎯

> **Give your AI Agent the same capability as Codex Plan Mode**
>
> When users propose a complex task, the agent automatically enters planning mode, creates an independent workspace in memory, guides users step by step to clarify requirements, and automatically exits when enough information is gathered to begin execution.

---

## 📖 What is this?

**task-plan-mode** is an OpenClaw agent skill that solves one core problem:

> **When users ask for complex tasks, they often don't know what preparation is needed. The Agent knows.**

For example, when a user says "Help me build a used-book trading mini-program" —
the user only knows the end goal, but doesn't know the steps needed (target users → core features → tech stack → page structure → data design → style).

This skill enables the agent to automatically:
1. Detect task complexity and enter planning mode
2. Create an independent workspace in memory
3. Ask one question at a time, exit when info is sufficient
4. Enter execution phase, deliver step by step per plan

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🧠 **Auto-trigger** | No manual commands — agent judges complexity automatically |
| 📂 **Workspace** | Independent workspace per task |
| 👣 **Step-by-step** | One question at a time, user never gets lost |
| 🔄 **Auto-exit** | Exit immediately when info is sufficient |
| 🏗️ **Domain scaffolding** | Different frameworks for websites, reports, research |
| 📝 **Full trace** | All planning steps saved to files |

---

## 🚀 Quick Start

```bash
git clone https://github.com/Arthur0112ux/task-plan-mode.git
# Place the SKILL.md in your agent's skills directory
```

---

## 📋 Built-in Domain Scaffolds

| Task Type | Decomposition Steps |
|-----------|-------------------|
| 🌐 Website/App | Users → Features → Tech Stack → Pages → Data → Design |
| 📝 Article/Report | Readers → Thesis → Length → Sources → Style |
| 🔬 Research | Question → Scope → Data → Method → Output |

---

## 🤝 Contributing

Issues and PRs welcome!

---

## 📜 License

MIT

---

## 👥 Authors

- **D Teacher** (DeepSeek V4) — Framework design, finalization
- **Olin** (GPT-5.5) — Trigger rules, exit logic
- **Penny** (Claude Code) — Workspace structure, docs

Tripartite Discussion, 2026-05-17
