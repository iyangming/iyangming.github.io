+++
title = "Claude Skills 入门与进阶指南"
date = 2026-05-17T09:00:00+08:00
draft = false
description = "Claude Skills 是 Anthropic 推出的技能系统，让 Claude 能够动态加载指令和工具来完成特定任务。本文从入门到进阶，全面介绍 Skills 的概念、用法和创建方法。"
tags = ["Claude", "AI 助手", "Skills", "Claude Code", "Agent Skills"]
categories = ["技术教程", "AI 工具"]
toc = true
weight = 3
slug = "claude-skills-guide"
+++

# Claude Skills 入门与进阶指南

> 解锁 Claude 的专业化能力

## 前言

Claude 是一款强大的 AI 助手，但当遇到专业领域任务时，默认能力可能不够精准。**Skills（技能）** 系统让你可以给 Claude 加载特定的指令集，让它在特定任务上表现出专家级水平。

本文基于 [Anthropic Skills 仓库](https://github.com/anthropics/skills) 的开源实现，带你从零掌握 Skills 的概念、用法和创建方法。

---

## 1. 什么是 Skills？

### 1.1 核心概念

Skills 是包含指令、脚本和资源的文件夹，Claude 会动态加载它们来提升在特定任务上的表现。Skills 教会 Claude 如何以可重复的方式完成特定任务，例如：

- 按照公司品牌指南创建文档
- 使用组织特定的工作流程分析数据
- 自动化个人任务

### 1.2 Skills vs 普通提示

| 对比项 | 普通对话 | 使用 Skills |
|--------|----------|-------------|
| 每次任务 | 重复说明要求 | 自动加载专业指令 |
| 知识一致性 | 依赖每次描述 | 规范化、专业化 |
| 触发方式 | 手动描述 | 自动识别场景 |
| 可复用性 | 低 | 高，开箱即用 |

### 1.3 工作原理

Skills 使用**渐进式披露**（Progressive Disclosure）三层加载：

```
┌────────────────────────────────────────────┐
│ Layer 1: Metadata（name + description）     │
│         ~100 words，常驻上下文              │
├────────────────────────────────────────────┤
│ Layer 2: SKILL.md body                      │
│         <500 行，技能触发时加载             │
├────────────────────────────────────────────┤
│ Layer 3: Bundled Resources（脚本/资源）     │
│         按需加载，脚本可直接执行            │
└────────────────────────────────────────────┘
```

---

## 2. 快速开始

### 2.1 在 Claude Code 中使用

Claude Code 支持插件市场，可以直接安装官方 Skills：

```bash
# 添加插件市场
/plugin marketplace add anthropics/skills

# 安装示例技能集
/plugin install document-skills@anthropic-agent-skills
/plugin install example-skills@anthropic-agent-skills
```

安装后，只需提及技能名称即可使用：

```
使用 PDF skill 从 path/to/file.pdf 提取表单字段
```

### 2.2 在 Claude.ai 中使用

Claude.ai 的付费用户可以直接使用所有官方 Skills，也可以上传自定义技能。详见 [官方文档](https://support.claude.com/en/articles/12512180-using-skills-in-claude)。

### 2.3 在 Claude API 中使用

通过 Claude API 可以使用预置 Skills，也可以上传自定义 Skills。参见 [Skills API 快速入门](https://docs.claude.com/en/api/skills-guide)。

---

## 3. 官方 Skills 示例

### 3.1 文档处理技能

| 技能 | 用途 |
|------|------|
| `docx` | 创建、读取、编辑 Word 文档（.docx） |
| `pdf` | 处理 PDF 文件 |
| `pptx` | 创建 PowerPoint 演示文稿 |
| `xlsx` | 处理 Excel 电子表格 |
| `doc-coauthoring` | 文档协作编辑 |

**使用示例：**

```
创建一份专业的 Word 文档，包含目录、页眉页脚和公司 logo
```

### 3.2 开发技能

| 技能 | 用途 |
|------|------|
| `claude-api` | 构建、调试、优化 Claude API 应用 |
| `mcp-builder` | 构建 MCP（Model Context Protocol）服务器 |
| `frontend-design` | 前端设计与实现 |
| `webapp-testing` | Web 应用测试 |
| `skill-creator` | 创建和优化自定义 Skills |

### 3.3 创意技能

| 技能 | 用途 |
|------|------|
| `algorithmic-art` | 算法艺术生成 |
| `canvas-design` | Canvas 设计 |
| `web-artifacts-builder` | Web 工件构建 |
| `theme-factory` | 主题工厂 |

### 3.4 企业技能

| 技能 | 用途 |
|------|------|
| `brand-guidelines` | 品牌指南应用 |
| `internal-comms` | 内部沟通 |
| `slack-gif-creator` | Slack 表情包创建 |

---

## 4. 技能结构解析

### 4.1 目录结构

一个技能文件夹结构如下：

```
skill-name/
├── SKILL.md              # 必需：技能定义文件
├── scripts/              # 可选：可执行脚本
│   ├── office/
│   │   ├── unpack.py
│   │   └── validate.py
│   └── ...
├── references/           # 可选：参考资料
│   └── documentation.md
└── assets/               # 可选：资源文件
    ├── templates/
    └── icons/
```

### 4.2 SKILL.md 结构

```markdown
---
name: my-skill-name
description: 技能的清晰描述，说明何时使用和做什么
---

# My Skill Name

[你的指令内容，Claude 激活此技能时会遵循这些指令]

## Examples
- 示例用法 1
- 示例用法 2

## Guidelines
- 指南 1
- 指南 2
```

**必需的前置matter字段：**

| 字段 | 说明 |
|------|------|
| `name` | 技能唯一标识符（小写，连字符分隔） |
| `description` | 完整描述：技能做什么以及何时使用 |

---

## 5. 创建自定义技能

### 5.1 技能创建流程

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  1. 捕获意图  │───►│  2. 访谈调研  │───►│  3. 编写 SKILL.md│
└──────────────┘    └──────────────┘    └──────────────┘
                                             │
                                             ▼
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  6. 扩展测试  │◄──│  5. 迭代改进  │◄──│  4. 编写测试用例│
└──────────────┘    └──────────────┘    └──────────────┘
```

### 5.2 捕获意图

在开始创建技能前，明确以下问题：

1. **这个技能要使能 Claude 做什么？**
2. **何时触发？（什么用户短语/上下文）**
3. **期望的输出格式是什么？**
4. **是否需要设置测试用例来验证技能效果？**

### 5.3 编写 description 的技巧

description 是技能的主要触发机制，需要包含：
- 技能做什么
- **何时使用**（具体场景）

> **提示：** Claude 有"欠触发"倾向——即在有用时不使用技能。为了解决这个问题，description 要稍微"强势"一些。例如：
>
> ❌ 弱："How to build a simple fast dashboard."
>
> ✅ 强："How to build a simple fast dashboard. **Make sure to use this skill whenever the user mentions dashboards, data visualization, internal metrics, or wants to display any kind of company data.**"

### 5.4 代码示例

**docx 技能示例：**

```javascript
const { Document, Packer, Paragraph, TextRun } = require('docx');

const doc = new Document({
  sections: [{
    properties: {
      page: {
        size: { width: 12240, height: 15840 },  // US Letter
        margin: { top: 1440, right: 1440, bottom: 1440, left: 1440 }
      }
    },
    children: [
      new Paragraph({
        children: [
          new TextRun({ text: "Hello World", bold: true })
        ]
      })
    ]
  }]
});

Packer.toBuffer(doc).then(buffer => fs.writeFileSync("output.docx", buffer));
```

---

## 6. 技能触发机制

### 6.1 自动触发

当用户提到相关关键词时，技能会自动激活。例如：

- 提到 "Word document"、".docx" → 触发 `docx` 技能
- 提到 "PDF"、提取表单字段 → 触发 `pdf` 技能
- 代码导入 `anthropic` SDK → 触发 `claude-api` 技能

### 6.2 手动触发

在 Claude Code 中可以直接调用：

```
使用 PDF skill 提取 path/to/file.pdf 的所有文本
```

### 6.3 避免欠触发

Skills 的 description 应该：
- 明确列出触发场景
- 包含同义词和相关术语
- 描述典型使用情境

---

## 7. Claude Code 插件市场

### 7.1 注册插件市场

```bash
/plugin marketplace add anthropics/skills
```

### 7.2 浏览和安装

1. 选择 `Browse and install plugins`
2. 选择 `anthropic-agent-skills`
3. 选择技能集（如 `document-skills` 或 `example-skills`）
4. 选择 `Install now`

### 7.3 直接安装

```bash
/plugin install document-skills@anthropic-agent-skills
/plugin install example-skills@anthropic-agent-skills
```

---

## 8. 进阶：技能优化与测试

### 8.1 使用 skill-creator 技能

Anthropic 提供了 `skill-creator` 技能来帮助创建和优化技能：

1. **创建草稿** — 基于访谈编写初始 SKILL.md
2. **编写测试用例** — 创建验证技能效果的测试 prompt
3. **运行评估** — 使用 Claude 执行测试
4. **定性评估** — 人工检查输出质量
5. **定量评估** — 运行带方差的基准测试
6. **迭代改进** — 根据反馈重写技能
7. **扩展测试集** — 更大规模验证

### 8.2 定量评估

对于有客观可验证输出的技能（如文件转换、数据提取、代码生成），可以：

1. 准备多样化的测试用例
2. 运行多次并分析方差
3. 优化 description 以提高触发准确性

### 8.3 Description 优化

使用专门的工具优化技能的 description，减少欠触发和误触发。

---

## 9. 实际应用案例

### 9.1 企业品牌文档自动化

创建 `brand-docs` 技能，确保所有对外文档符合品牌规范：

```markdown
---
name: brand-docs
description: 创建符合公司品牌规范的文档。当用户请求创建报告、备忘录、信函或任何正式文档时使用。触发场景包括：提及"创建文档"、"生成报告"、"公司信函"、"品牌材料"。确保所有输出遵循公司 VI 手册，包括字体、颜色、logo 放置和格式标准。
---

# Brand Document Creation

## Brand Guidelines
[插入公司品牌规范内容]

## Document Templates
[文档模板说明]

## Quality Checklist
- [ ] 字体符合品牌标准
- [ ] 颜色使用品牌色板
- [ ] Logo 正确放置
- [ ] 格式符合公司标准
```

### 9.2 代码审查技能

创建 `code-review` 技能，标准化代码审查流程：

```markdown
---
name: code-review
description: 执行代码审查。当用户要求"审查代码"、"review"、"检查bug"或"分析代码质量"时触发。使用此技能可以系统性地检查代码的：可读性、性能、安全性、测试覆盖率、最佳实践遵循情况。
---

# Code Review

## Review Checklist
1. **可读性** — 命名清晰、函数简洁、注释充分
2. **性能** — 无明显性能问题、无 N+1 查询
3. **安全性** — 无注入风险、无敏感信息泄露
4. **测试** — 测试覆盖率充分、测试质量高
5. **最佳实践** — 符合语言/框架惯例

## Output Format
[审查结果的结构化输出格式]
```

---

## 10. 最佳实践

### 10.1 技能设计原则

| 原则 | 说明 |
|------|------|
| **专注单一职责** | 每个技能做一件事做好 |
| **清晰的触发描述** | 让 Claude 知道何时使用 |
| **渐进式复杂度** | 基础指令简单，细节按需加载 |
| **包含示例** | 具体示例胜过抽象描述 |

### 10.2 description 编写

- ✅ 使用具体的触发场景描述
- ✅ 包含同义词和相关术语
- ✅ 描述典型输入/输出
- ❌ 避免模糊的"这技能很有用"
- ❌ 避免过于宽泛的触发词

### 10.3 SKILL.md 组织

- 保持 < 500 行
- 大文件添加目录
- 参考文件清晰引用
- 关键决策有明确说明

---

## 11. 参考资源

### 官方资源

- [Anthropic Skills 仓库](https://github.com/anthropics/skills)
- [What are skills?](https://support.claude.com/en/articles/12512176-what-are-skills)
- [Using skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude)
- [How to create custom skills](https://support.claude.com/en/articles/12512198-creating-custom-skills)
- [Agent Skills 规范](https://agentskills.io/specification)
- [Equipping agents for the real world](https://anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)

### 相关工具

- [Claude Code](/docs/claude-code)
- [MCP (Model Context Protocol)](https://modelcontextprotocol.io)
- [Anthropic API](https://docs.anthropic.com)

---

## 12. 总结

Skills 系统让 Claude 拥有了专业化的能力，通过动态加载指令和工具，它可以像专家一样处理特定领域的任务。

**核心要点：**

- ✅ Skills 是包含指令、脚本和资源的可复用单元
- ✅ 三层加载机制平衡了上下文和功能
- ✅ 清晰的 description 是正确触发的关键
- ✅ 渐进式披露让大型技能也能高效工作
- ✅ 支持多种触发方式：自动、手动、API

**下一步行动：**

1. 在 Claude Code 中尝试安装一个技能集
2. 使用已安装的技能完成一个实际任务
3. 尝试创建你的第一个自定义技能

---

**作者**: iyangming
**发布时间**: 2026-05-17
**标签**: #Claude #Skills #AI助手 #Claude Code #Agent Skills

> 如果你觉得这篇文章有帮助，欢迎分享给更多对 AI 辅助开发感兴趣的朋友！