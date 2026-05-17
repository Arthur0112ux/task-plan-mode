# task-plan-mode — Plan Mode for AI Agents 🎯

<p align="center">
  <a href="https://github.com/Arthur0112ux/task-plan-mode/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"></a>
  <a href="https://github.com/Arthur0112ux/task-plan-mode/stargazers"><img src="https://img.shields.io/github/stars/Arthur0112ux/task-plan-mode?style=flat" alt="GitHub Stars"></a>
  <a href="https://clawhub.ai/skills/task-plan-mode"><img src="https://img.shields.io/badge/clawhub-available-brightgreen" alt="ClawHub"></a>
</p>

> **Give your AI Agent the same capability as Codex Plan Mode**
>
> When users propose a complex task, the agent automatically enters planning mode, creates an independent workspace in memory, guides users step by step to clarify requirements, and automatically exits when enough information is gathered to begin execution.

[English](./README_EN.md) · [中文](./README.md) · [SKILL](./SKILL.md) · [Examples](./examples/)

**One-command install:**
```bash
npx clawhub@latest install task-plan-mode
```

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

### Install

```bash
# Option 1: ClawHub (recommended)
npx clawhub@latest install task-plan-mode

# Option 2: Clone
git clone https://github.com/Arthur0112ux/task-plan-mode.git

# Option 3: Manual
# Download SKILL.md from GitHub and place in your skills directory
```

### Usage

No configuration needed. The agent works automatically:

```
User: Help me build a used-book trading mini-program
  ↓ Agent detects → complex task
  ↓ Enters Plan Mode
  ↓ Creates workspace → ~/memory/used-book-app/
Agent: Who is this for?
User: University students
Agent: Top 3 features?
User: Listing and browsing books
Agent: Login method?
User: WeChat OAuth
  ↓ Info sufficient → auto exit Plan Mode
  ↓ Generates plan.md
  ↓ Begins execution
```

---

## 📚 File Structure

| File | Description |
|------|-------------|
| [SKILL.md](./SKILL.md) | Core OpenClaw agent skill |
| [README.md](./README.md) | Chinese overview |
| [README_EN.md](./README_EN.md) | English overview |
| [examples/](./examples/) | Usage scenarios |
| [docs/](./docs/) | Detailed documentation |

---

## 🤝 Contributing

- ⭐ Star the repo
- 🐛 Open an Issue
- 🔀 Submit a PR

See [CONTRIBUTING.md](./CONTRIBUTING.md)

---

## 📜 License

[MIT](./LICENSE) — Free to use, modify, and distribute
