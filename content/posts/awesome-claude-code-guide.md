+++
title = "Awesome Claude Code 指南：海量资源一网打尽"
date = 2026-05-17T09:10:00+08:00
draft = false
description = "Awesome Claude Code 是一个精心策划的 Claude Code 资源清单，包含高质量的 Skills、Hooks、Slash Commands、Agent 编排器、开发工具等。本文带你全面了解这个宝库。"
tags = ["Claude Code", "Claude", "AI 辅助开发", "Skills", "Slash Commands", "开发工具"]
categories = ["技术教程", "AI 工具"]
toc = true
weight = 4
slug = "awesome-claude-code-guide"
+++

# Awesome Claude Code 指南：海量资源一网打尽

> 来自 44K+ Stars 的 Claude Code 资源宝库

## 前言

[Awesome Claude Code](https://github.com/hesreallyhim/awesome-claude-code) 是一个精心策划的 Claude Code 资源集合，包含高质量的 Skills、Agents、Hooks、Status Lines、Orchestrators、开发工具，以及 Claude Code 团队持续推出的新功能。

这个仓库获得了 **44K+ Stars**，证明了它在开发者社区的受欢迎程度。本文将带你全面了解这个资源宝库。

---

## 1. 仓库概览

| 指标 | 数值 |
|------|------|
| Stars | 44,000+ |
| Forks | 3,700+ |
| 资源数量 | 500+ |
| 分类 | Skills、Agents、Hooks、Slash Commands 等 |

---

## 2. 资源分类

### 2.1 Agent Skills（智能体技能）

Agent Skills 是 Claude Code 的核心扩展，让 Claude 在特定任务上表现出专家级水平。

**热门 Skills：**

| Skill | 作者 | 说明 |
|--------|------|------|
| AgentSys | avifenesh | 工作流自动化系统，包含插件、agents 和 skills |
| Book Factory | Robert Guss | 完整的书籍创作流水线 Skills |
| Claude Code MCP Enhanced | - | 增强的 MCP 服务器集成 |

### 2.2 Slash Commands（斜杠命令）

通过斜杠命令快速执行特定任务。

| 命令 | 功能 |
|------|------|
| `/act` | 行动命令执行 |
| `/add-to-changelog` | 添加到变更日志 |
| `/commit` | 智能提交 |
| `/create-pr` | 创建 Pull Request |
| `/pr-review` | PR 代码审查 |
| `/optimize` | 代码优化建议 |
| `/testing_plan_integration` | 测试计划集成 |

### 2.3 Hooks（钩子）

Hooks 允许在关键事件触发自定义行为。

| Hook 类型 | 用途 |
|-----------|------|
| pre-tool-use | 工具执行前拦截 |
| post-tool-use | 工具执行后处理 |
| on都与 | 各种事件触发点 |

### 2.4 Claude.md Files（配置）

自定义 Claude 的行为和工作方式。

| 配置 | 说明 |
|------|------|
| Basic-Memory | 基础记忆系统 |
| Comm | 通信增强 |
| Cursor-Tools | Cursor 工具集成 |
| Perplexity-MCP | Perplexity MCP 服务器 |

### 2.5 工作流与指南

| 资源 | 说明 |
|------|------|
| Design-Review-Workflow | 设计审查工作流 |
| Blogging-Platform-Instructions | 博客平台指南 |
| Claude-Code-GitHub-Actions | GitHub Actions 集成 |

---

## 3. 快速上手

### 3.1 安装 Skills

通过 Claude Code 插件市场安装：

```bash
/plugin marketplace add hesreallyhim/awesome-claude-code
/plugin install <skill-name>@awesome-claude-code
```

### 3.2 使用 Slash Commands

在 Claude Code 中直接输入斜杠命令：

```
/commit "fix: 修复登录 bug"
/create-pr "feat: 添加深色模式"
/pr-review
```

### 3.3 集成 MCP 服务器

```bash
claude mcp add <server-name> <server-command>
```

---

## 4. 热门资源推荐

### 4.1 开发工具类

| 资源 | Stars | 说明 |
|------|-------|------|
| AWS-MCP-Server | 高 | AWS 服务集成 |
| LangGraphJS | 高 | JavaScript LangGraph 集成 |
| SPy | 中 | Python 脚本集成 |

### 4.2 工作流类

| 资源 | 说明 |
|------|------|
| create-prp | 创建 PR 说明文档 |
| create-jtbd | Jobs-to-be-Done 模板 |
| update-branch-name | 自动更新分支名 |

### 4.3 企业级应用

| 资源 | 说明 |
|------|------|
| Comm | 企业通信集成 |
| Design-Review-Workflow | 设计审查流程 |

---

## 5. 资源查找技巧

### 5.1 CSV 资源表

仓库提供了完整的 `THE_RESOURCES_TABLE.csv` 文件，包含所有资源的详细信息：

```
ID, Display Name, Category, Sub-Category, Primary Link, Author...
```

可以通过筛选 CSV 快速找到需要的资源。

### 5.2 分类浏览

```
resources/
├── claude.md-files/          # Claude 配置
├── official-documentation/   # 官方文档
├── slash-commands/           # 斜杠命令
└── workflows-knowledge-guides/# 工作流和指南
```

---

## 6. 贡献指南

欢迎提交新的资源！提交前请确保：

1. **质量优先** — 只提交高质量、原创的资源
2. **分类正确** — 将资源放到正确的分类目录
3. **更新 CSV** — 在 `THE_RESOURCES_TABLE.csv` 中添加条目
4. **遵循规范** — 参考现有资源的格式

### 提交步骤

```bash
# 1. Fork 仓库
# 2. 添加资源到对应目录
# 3. 更新 CSV
# 4. 提交 PR
```

---

## 7. 与其他资源对比

| 资源库 | Awesome Claude Code | 其他 |
|--------|---------------------|------|
| 资源数量 | 500+ | 较少 |
| 分类 | 5+ 大类 | 单一 |
| 更新频率 | 活跃 | 一般 |
| Stars | 44K+ | - |

---

## 8. 参考链接

- **GitHub**: [github.com/hesreallyhim/awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code)
- **官方文档**: [docs.anthropic.com](https://docs.anthropic.com)
- **Claude Code**: [claude.ai/code](https://claude.ai/code)

---

## 总结

Awesome Claude Code 是 Claude Code 开发者不可或缺的资源宝库。无论是寻找特定的 Skill、Slash Command，还是学习最佳实践，这个仓库都能提供丰富的资源。

**核心要点：**

- ✅ 44K+ Stars，业界认可度高
- ✅ 500+ 资源，覆盖开发全流程
- ✅ 分类清晰，易于查找
- ✅ 活跃维护，持续更新

**下一步：**

1. 访问 [Awesome Claude Code](https://github.com/hesreallyhim/awesome-claude-code) 探索资源
2. 安装几个感兴趣的 Skills
3. 尝试使用 Slash Commands 提升效率

---

**作者**: iyangming
**发布时间**: 2026-05-17
**标签**: #Claude Code #AI辅助开发 #Skills #Slash Commands

> 如果你觉得这篇文章有帮助，欢迎分享给更多对 Claude Code 感兴趣的朋友！