# task-plan-mode — 任务规划模式 🎯

<p align="center">
  <a href="https://github.com/Arthur0112ux/task-plan-mode/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"></a>
  <a href="https://github.com/Arthur0112ux/task-plan-mode/stargazers"><img src="https://img.shields.io/github/stars/Arthur0112ux/task-plan-mode?style=flat" alt="GitHub Stars"></a>
  <a href="https://clawhub.ai/skills/task-plan-mode"><img src="https://img.shields.io/badge/clawhub-available-brightgreen" alt="ClawHub"></a>
  <a href="https://github.com/Arthur0112ux/task-plan-mode/releases"><img src="https://img.shields.io/github/v/release/Arthur0112ux/task-plan-mode" alt="Version"></a>
</p>

> **让你的 AI Agent 拥有分步式任务拆解+执行能力，v2.0 新增前置评估流程**
>
> 复杂任务不再是"一轮对话就产出"。AI 先做前置评估 → 明确分几个阶段 → 每个阶段逐步执行 → 阶段间汇报进度。

[中文](./README.md) · [English](./README_EN.md) · [SKILL 说明](./SKILL.md) · [使用示例](./examples/)

**一键安装：**
```bash
npx clawhub@latest install task-plan-mode
```

---

## 📖 这是什么？

**task-plan-mode** 是一个 AI agent 任务规划模式技能。当用户提出复杂任务时，agent：

1. **前置评估（v2.0 新增）** — 先评估任务复杂度，输出阶段划分方案
2. **分步执行** — 需求确认 → 逐步执行 → 阶段汇报
3. **状态追踪** — 每步标注当前阶段和进度

### 解决了什么问题？

| 痛点 | 解决方式 |
|------|---------|
| AI 一轮对话就产出 → 质量不够 | 拆成多轮，每轮只做一件事 |
| 用户需求模糊 → 方向跑偏 | 先确认需求，再动手执行 |
| 做了一半发现缺信息 | 阶段汇报机制，每步可调整 |
| 多 Agent 协作时互相踩 | 单线程执行，阶段清楚 |

### v2.0 更新内容

- **新增 Phase 0：前置评估** — AI 收到任务后先输出阶段划分方案，用户确认后才进入执行
- **新增阶段汇报模板** — 每阶段完成后格式化汇报
- **新增进度标注** — 每次回复末尾标注当前 Phase
- **新增多种任务类型的默认阶段划分**

---

## 🚀 使用方式

### 自动触发

当用户提出以下类型任务时，agent 自动进入 Plan Mode：

- "帮我做一个 X"（网站、小程序、工具）
- "写一份关于 X 的报告/文章"
- "分析一下 X 行业/市场/趋势"
- 任何需要 3 步以上的复杂任务

### 手动触发

```
"规划模式"
"Plan Mode"
"帮我拆解一下这个任务"
"先规划一下"
```

---

## ⚙️ 工作流程

### 完整流程示例

```
用户 → "帮我做一份新能源行业分析报告"

AI (Phase 0)：
📋 任务评估
我计划分 4 个阶段：
Phase 1：需求确认
Phase 2：数据搜集
Phase 3：分析撰写
Phase 4：排版交付
请确认是否按此方案？

用户 → "可以"

AI (Phase 1)：
第一步：读者是谁？公司内部还是公众号读者？
...
（信息足够 → 自动进入 Phase 2）
...
...
AI (Phase Final)：
✅ 全部完成，交付报告：[文件名]
```

---

## 📦 文件结构

```
task-plan-mode/
├── SKILL.md            ← 完整技能文档（核心）
├── README.md           ← 本文件
├── README_EN.md        ← 英文版
├── docs/               ← 设计文档
│   ├── design-principles.md
│   └── triggers.md
├── examples/           ← 使用示例
│   └── *.md
└── LICENSE
```

---

## 🤝 贡献与更新

每次优化后同步到两个位置：
1. **GitHub 仓库** — 版本管理
2. **AI 共享技能库** — 本机 agent 读取

---

## 📄 许可

MIT License — 自由使用、修改、分发。
