+++
title = "OpenSpec 入门指南：规范驱动的 AI 辅助开发"
date = 2026-05-17T08:20:00+08:00
draft = false
description = "OpenSpec 是一个规范驱动的开发框架，帮助开发者和 AI 编码助手在写代码之前先达成共识。本文将带你从零开始掌握 OpenSpec 的核心概念和工作流程。"
tags = ["OpenSpec", "AI 辅助开发", "规范驱动开发", "Claude Code", "开发工作流"]
categories = ["技术教程", "开发工具"]
toc = true
weight = 2
slug = "openspec-beginners-guide"
+++

# OpenSpec 入门指南：规范驱动的 AI 辅助开发

> 让 AI 辅助开发从「靠谱」到「确定」

## 前言

AI 编码助手（如 Claude Code、Cursor 等）功能强大，但当需求只存在于对话历史中时，AI 的输出往往不可预测。**OpenSpec** 正是为了解决这一问题而生的——它添加了一个轻量级的规范层，让开发者和 AI 在写代码之前先对齐「要做什么」。

---

## 1. 什么是 OpenSpec？

### 1.1 核心定位

OpenSpec 是一个**规范驱动的开发框架（Spec-Driven Development, SDD）**，专门为 AI 编码助手设计。它的核心理念是：

```
→ fluid not rigid        （灵活而非僵化）
→ iterative not waterfall（迭代而非瀑布）
→ easy not complex       （简单而非复杂）
→ built for brownfield   （支持存量项目）
→ scalable               （从小项目到企业级）
```

### 1.2 解决什么问题？

| 传统开发 | 使用 OpenSpec |
|----------|---------------|
| AI 理解模糊，代码来回改 | 先对齐规范，再写代码 |
| 需求变更是「口头约定」 | 需求写入 spec文档，可追溯 |
| AI 实现与预期不符 | 基于 artifacts 验证实现 |
| 多人协作时理解不一致 | 规范即文档，团队共享 |

### 1.3 核心优势

- **对齐后再开发** — 开发者和 AI 在代码编写前对齐需求
- **保持组织性** — 每个变更都有独立的文件夹，包含 proposal、specs、design、tasks
- **工作流畅** — 随时更新任何 artifact，不受严格阶段限制
- **工具无关** — 支持 20+ 款 AI 编码助手

---

## 2. 快速开始

### 2.1 环境要求

- Node.js 20.19.0 或更高版本

### 2.2 安装与初始化

```bash
# 全局安装 OpenSpec
npm install -g @fission-ai/openspec@latest

# 进入你的项目目录并初始化
cd your-project
openspec init
```

> **提示：** OpenSpec 也支持 pnpm、yarn、bun 和 nix。详见[官方安装文档](https://github.com/iyangming/OpenSpec/blob/main/docs/installation.md)。

### 2.3 初始化后的目录结构

```
openspec/
├── specs/              # 源代码规范（系统当前行为的描述）
│   └── <domain>/
│       └── spec.md
├── changes/            # 提议的变更
│   └── <change-name>/
│       ├── proposal.md
│       ├── design.md
│       ├── tasks.md
│       └── specs/      # 增量规范
│           └── <domain>/
│               └── spec.md
└── config.yaml         # 项目配置（可选）
```

**两个核心目录：**

- `specs/` — 源代码规范，描述系统当前如何运作，按领域组织（如 `specs/auth/`、`specs/payments/`）
- `changes/` — 提议的修改，每个变更有独立文件夹，完成后会合并到 `specs/`

---

## 3. 核心概念

### 3.1 Artifact（产物）

每个变更文件夹包含四种 artifact，它们相互依赖、层层递进：

| Artifact | 作用 |
|----------|------|
| `proposal.md` | 「为什么」和「做什么」— 捕获意图、范围和方案 |
| `specs/` | 增量规范 — 展示新增/修改/删除的需求 |
| `design.md` | 「怎么做」— 技术方案和架构决策 |
| `tasks.md` | 实现检查清单 — 带复选框的任务列表 |

**产物之间的依赖关系：**

```
proposal ──► specs ──► design ──► tasks ──► implement
   ▲           ▲          ▲                    │
   └───────────┴──────────┴────────────────────┘
            随时更新
```

### 3.2 Delta Specs（增量规范）

增量规范是 OpenSpec 的核心概念。它展示相对于当前规范的变更。

**格式示例：**

```markdown
# Delta for Auth

## ADDED Requirements

### Requirement: 双因素认证
系统必须在登录时要求第二个认证因素。

#### Scenario: 需要 OTP
- GIVEN 已启用双因素认证的用户
- WHEN 用户提交有效凭证
- THEN 展示 OTP 挑战

## MODIFIED Requirements

### Requirement: 会话超时
系统应在 30 分钟不活动后使会话过期。
（之前：60 分钟）

## REMOVED Requirements

### Requirement: 记住我
（因双因素认证而弃用）
```

### 3.3 Schema（模式）

Schema 定义了 artifact 的序列和依赖关系。默认的 `spec-driven` schema 包含：

```
proposal → specs → design → tasks → apply-required
```

你也可以创建自定义 schema 来适应特定工作流。

---

## 4. 工作流程

### 4.1 默认快速路径（core profile）

新安装默认使用 `core` profile，命令最精简：

```
/opsx:propose ──► /opsx:apply ──► /opsx:sync ──► /opsx:archive
```

**完整示例：**

```text
你: /opsx:propose 添加深色模式

AI:  创建了 openspec/changes/add-dark-mode/
     ✓ proposal.md — 为什么做这个变更
     ✓ specs/       — 需求和场景
     ✓ design.md    — 技术方案
     ✓ tasks.md     — 实现检查清单
     准备开始实现！

你: /opsx:apply

AI:  开始实现...
     ✓ 1.1 创建 ThemeContext
     ✓ 1.2 添加 CSS 自定义属性
     ✓ 1.3 实现 localStorage 持久化
     ✓ 2.1 创建 ThemeToggle 组件
     ...
     所有任务完成！

你: /opsx:archive

AI:  归档 add-dark-mode...
     ✓ 规范已合并到 openspec/specs/ui/spec.md
     ✓ 已移动到 openspec/changes/archive/2025-01-24-add-dark-mode/
     完成！
```

### 4.2 扩展工作流（Expanded Workflow）

如果需要更细粒度的控制，可以启用扩展命令：

```bash
openspec config profile  # 选择 workflows
openspec update           # 应用更改
```

扩展工作流命令：

| 命令 | 作用 |
|------|------|
| `/opsx:new` | 开始一个新的变更脚手架 |
| `/opsx:continue` | 创建下一个 artifact（增量） |
| `/opsx:ff` | 一次性创建所有规划 artifact |
| `/opsx:verify` | 验证实现是否匹配规范 |
| `/opsx:bulk-archive` | 批量归档多个变更 |
| `/opsx:onboard` | 引导式教程 |

**扩展路径：**

```
/opsx:new ──► /opsx:ff ──► /opsx:apply ──► /opsx:verify ──► /opsx:archive
```

### 4.3 探索模式

当需求不明确时，先探索再动手：

```text
你: /opsx:explore

AI:  你想探索什么？

你: 我们的 API 限流方案应该怎么做？

AI:  让我研究一下你当前的代码库...
     [分析代码库，考虑模式]

     我发现了三种方案：
     1. 中间件限流（简单，按端点）
     2. Redis 后端（可扩展，共享状态）
     3. Token bucket 按用户（公平，复杂）

     你当前的技术栈支持方案 1 或 2。你的规模是？

你: 用 Redis 吧，可以开始一个变更吗？

AI:  随时可以。运行 /opsx:propose implement-redis-rate-limiting 开始。
```

---

## 5. 命令详解

### 5.1 `/opsx:propose` — 提议变更

创建新变更并生成所有规划 artifact：

```text
/opsx:propose [变更名称或描述]
```

**示例：**

```text
/opsx:propose 添加用户头像上传功能
```

### 5.2 `/opsx:apply` — 应用实现

根据 tasks.md 实现任务：

```text
/opsx:apply [变更名称]
```

可以随时中断和恢复，实现状态保存在 tasks.md 的复选框中。

### 5.3 `/opsx:verify` — 验证实现

验证实现是否匹配 artifacts，检查三个维度：

| 维度 | 检查内容 |
|------|----------|
| **完整性** | 所有任务完成？所有需求有对应代码？ |
| **正确性** | 实现是否符合规范意图？边界情况处理？ |
| **一致性** | 设计决策是否反映在代码中？ |

**示例输出：**

```
COMPLETENESS
✓ tasks.md 中所有 8 个任务已完成
✓ specs 中所有需求都有对应代码
⚠ 场景「系统偏好检测」没有测试覆盖

CORRECTNESS
✓ 实现符合规范意图
✓ 边界情况已处理

COHERENCE
✓ 设计决策反映在代码结构中
⚠ design 提到「CSS 变量」但实现用的是 Tailwind

SUMMARY
Critical: 0 | Warnings: 2 | 可归档: 是
```

### 5.4 `/opsx:archive` — 归档变更

完成变更并移动到归档目录：

```text
/opsx:archive [变更名称]
```

归档时如果规范尚未同步，会提示你同步。

### 5.5 `/opsx:explore` — 探索想法

在正式提出变更前，先调研和分析：

```text
/opsx:explore [主题]
```

不创建任何 artifact，用于澄清需求、对比方案。

---

## 6. 实际案例：添加深色模式

### 6.1 提议变更

```text
你: /opsx:propose add-dark-mode

AI:  创建了 openspec/changes/add-dark-mode/
     ✓ proposal.md — 为什么做这个变更
     ✓ specs/       — 需求和场景
     ✓ design.md    — 技术方案
     ✓ tasks.md     — 实现检查清单
     准备开始实现！
```

### 6.2 生成的 proposal.md

```markdown
# Proposal: 添加深色模式

## Intent
用户请求深色模式选项，以减少夜间使用的眼睛疲劳。

## Scope
- 在设置中添加主题切换
- 支持系统偏好检测
- 在 localStorage 中持久化偏好

## Approach
使用 CSS 自定义属性进行主题管理，React context 进行状态管理。
```

### 6.3 生成的 tasks.md

```markdown
# Tasks

## 1. 主题基础设施
- [ ] 1.1 创建带 light/dark 状态的 ThemeContext
- [ ] 1.2 添加颜色 CSS 自定义属性
- [ ] 1.3 实现 localStorage 持久化

## 2. UI 组件
- [ ] 2.1 创建 ThemeToggle 组件
- [ ] 2.2 在设置页面添加切换
- [ ] 2.3 更新 Header 以包含快速切换

## 3. 样式
- [ ] 3.1 定义深色主题调色板
- [ ] 3.2 更新组件以使用 CSS 变量
```

### 6.4 实现与归档

```text
你: /opsx:apply

AI:  开始实现...
     ✓ 1.1 创建了 ThemeContext
     ✓ 1.2 添加了 CSS 自定义属性
     ✓ 2.1 创建了 ThemeToggle 组件
     ...
     所有任务完成！

你: /opsx:verify

AI:  验证通过，可以归档了。

你: /opsx:archive

AI:  ✓ 规范已合并到 openspec/specs/ui/spec.md
     ✓ 已移动到归档目录
     完成！
```

---

## 7. 与其他工具的对比

| 工具 | OpenSpec 的优势 |
|------|-----------------|
| **Spec Kit (GitHub)** | 更轻量，迭代更自由 |
| **Kiro (AWS)** | 支持多种 AI 工具和模型 |
| **无规范开发** | 带来可预测性，而非繁文缛节 |

---

## 8. 最佳实践

### 8.1 保持变更专注

一个逻辑单元的变更对应一个 change。如果要「添加功能 X 同时重构 Y」，考虑拆成两个独立变更。

### 8.2 需求不明确时先探索

使用 `/opsx:explore` 调研问题空间，再提出变更。

### 8.3 归档前验证

使用 `/opsx:verify` 检查实现与规范的一致性。

### 8.4 清晰的命名

```
✓ 好命名：add-dark-mode, fix-login-redirect, optimize-query
✗ 避免：feature-1, update, changes, wip
```

---

## 9. 更新 OpenSpec

```bash
# 升级包
npm install -g @fission-ai/openspec@latest

# 在项目内刷新 AI 指令
openspec update
```

---

## 10. 总结

OpenSpec 将规范驱动开发的理念带入了 AI 辅助开发时代。通过在实现前对齐需求，它解决了 AI 编码助手「强大但不可预测」的问题。

**核心要点：**

- ✅ 先对齐规范，再写代码
- ✅ 每个变更有完整的 artifacts（proposal、specs、design、tasks）
- ✅ 增量规范让存量项目也能轻松接入
- ✅ 支持 20+ 款 AI 编码助手
- ✅ 工作流程灵活，可迭代

**下一步行动：**

1. 在你的项目中运行 `openspec init`
2. 尝试 `/opsx:propose` 提出一个小变更
3. 使用 `/opsx:apply` 实现它
4. 用 `/opsx:archive` 完成闭环

---

## 参考资料

- OpenSpec GitHub: [github.com/Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec)
- 官方文档: [docs.openspec.ai](https://docs.openspec.ai)
- Discord 社区: [discord.gg/YctCnvvshC](https://discord.gg/YctCnvvshC)

---

**作者**: iyangming  
**发布时间**: 2026-05-17  
**标签**: #OpenSpec #AI辅助开发 #规范驱动开发 #Claude Code

> 如果你觉得这篇文章有帮助，欢迎分享给更多对 AI 编码助手感兴趣的朋友！