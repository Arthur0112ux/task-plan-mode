# task-plan-mode — 任务规划模式 🎯

<p align="center">
  <a href="https://github.com/Arthur0112ux/task-plan-mode/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"></a>
  <a href="https://github.com/Arthur0112ux/task-plan-mode/stargazers"><img src="https://img.shields.io/github/stars/Arthur0112ux/task-plan-mode?style=flat" alt="GitHub Stars"></a>
  <a href="https://clawhub.ai/skills/task-plan-mode"><img src="https://img.shields.io/badge/clawhub-available-brightgreen" alt="ClawHub"></a>
  <a href="https://github.com/Arthur0112ux/task-plan-mode/releases"><img src="https://img.shields.io/github/v/release/Arthur0112ux/task-plan-mode" alt="Version"></a>
</p>

> **让你的 AI Agent 拥有「Codex Plan Mode」一样的能力**
>
> 当用户提出复杂任务时，agent 自动进入规划模式，在记忆区创建独立 workspace，逐步引导用户明确需求，并在信息足够时自动退出、进入执行。

[中文](./README.md) · [English](./README_EN.md) · [SKILL 说明](./SKILL.md) · [使用示例](./examples/)

**一键安装：**
```bash
npx clawhub@latest install task-plan-mode
```

---

## 📖 这是什么？

**task-plan-mode** 是一个 OpenClaw agent skill，解决一个核心问题：

> **用户提出复杂任务时，往往不知道需要准备什么。Agent 知道。**

比如用户说"帮我做一个二手书交易小程序"——
用户只知道最终想要什么，但不知道需要经历哪些步骤（目标用户定义 → 功能确认 → 技术选型 → 页面规划 → 数据设计 → 风格确定）。

这个 skill 让 agent 自动：
1. 检测任务复杂度，自动切入规划模式
2. 在记忆区创建独立 workspace，分步收集需求
3. 每次只问 1 个问题，信息足够时自动退出
4. 进入执行阶段，按规划逐步交付

---

## ✨ 核心特性

| 特性 | 说明 |
|------|------|
| 🧠 **自动触发** | 不用手动命令——agent 自己判断任务复杂度 |
| 📂 **独立工作区** | 每任务在记忆区创建独立 workspace |
| 👣 **逐步引导** | 每次 1 个环节，用户不迷茫 |
| 🔄 **自动退出** | 信息够了立刻退，不用问"可以开始了吗" |
| 🏗️ **领域脚手架** | 做网站、写报告、做研究用不同的拆解框架 |
| 📝 **完整记录** | 所有规划过程写入文件，可追溯 |

---

## 🚀 快速开始

### 安装

```bash
# 方式一：ClawHub 一键安装（推荐）
npx clawhub@latest install task-plan-mode

# 方式二：克隆仓库
git clone https://github.com/Arthur0112ux/task-plan-mode.git

# 方式三：手动下载 SKILL.md
# 访问 https://github.com/Arthur0112ux/task-plan-mode/blob/main/SKILL.md
# 复制内容放入你的 skills 目录
```

### 使用

安装后无需任何配置，agent 会自动工作：

```
用户：帮我做一个二手书交易小程序
  ↓ agent 自动检测 → 复杂任务
  ↓ 进入 Plan Mode
  ↓ workspace 创建 → ~/.task-plan-mode/workspace/二手书小程序/
Agent：这个二手书小程序主要是给谁用的？
用户：大学生
Agent：最核心的 3 个功能是什么？
用户：发布和浏览
Agent：登录方式？
用户：微信授权
  ↓ 信息足够 → 自动退出
  ↓ 生成完整 plan.md
  ↓ 进入执行阶段
```

---

## 🏗️ 工作区结构

```
~/.task-plan-mode/workspace/{项目名}/
├── README.md          # 任务总览
├── plan.md            # 拆解计划（阶段表）
├── context/           # 需求收集记录
│   ├── 01-需求对齐.md
│   ├── 02-功能确认.md
│   └── 03-技术方案.md
└── deliverables/      # 产出物
```

---

## 📋 内置领域脚手架

| 任务类型 | 拆解环节 |
|---------|---------|
| 🌐 **网站/小程序** | 目标用户 → 核心功能 → 技术选型 → 页面结构 → 数据需求 → 设计风格 |
| 📝 **文章/报告** | 目标读者 → 核心论点 → 篇幅 → 数据来源 → 风格 |
| 🔬 **研究/分析** | 研究问题 → 范围界定 → 数据需求 → 分析方法 → 输出格式 |

其他类型：agent 自动生成领域专用脚手架。

---

## 🔧 触发方式

### 自动触发
| 场景 | 说明 |
|------|------|
| ✅ 用户说"做一个X" | 做网站/开发/小程序/报告等 |
| ✅ 任务涉及 3+ 步骤 | agent 内部自动评估 |
| ✅ 需求模糊 | 缺关键信息，agent 自动切规划 |
| ✅ "先规划一下" | 用户明确要求先拆解 |

### 手动触发
| 关键词 | 说明 |
|--------|------|
| "切任务模式" / "Plan Mode" | 手动进入 |
| "帮我拆解一下" | 要求拆解 |
| "这个任务比较复杂" | 提示 agent 切模式 |

---

## 📚 文件说明

| 文件 | 说明 |
|------|------|
| [SKILL.md](./SKILL.md) | OpenClaw agent skill 文件（核心） |
| [README.md](./README.md) | 中文总览 |
| [README_EN.md](./README_EN.md) | English overview |
| [examples/](./examples/) | 使用场景示例 |
| [docs/](./docs/) | 详细设计文档 |

---

## 🤝 如何参与

- ⭐ **Star** — 让更多人看到
- 🐛 **Issue** — 报告问题或建议功能
- 🔀 **PR** — 改进文档或逻辑
- 📢 **分享** — 告诉朋友这个工具

详见 [CONTRIBUTING.md](./CONTRIBUTING.md)

---

## 📜 许可证

[MIT](./LICENSE) — 自由使用、修改、分发
