---
name: claude-md
description: Create or update CLAUDE.md files following best practices for optimal AI agent onboarding
---

## 用户输入

```text
$ARGUMENTS
```

**你必须**在继续之前考虑用户输入（如果不为空）。用户可以指定：
- `create` - 从头创建新的 CLAUDE.md
- `update` - 改进现有的 CLAUDE.md
- `audit` - 分析并报告当前 CLAUDE.md 质量
- 一个特定路径用于创建/更新

## 核心原则

**LLM 是无状态的**：CLAUDE.md 是每个对话自动包含的唯一文件。它作为 AI 代理进入代码库的主要入职文档。

### 黄金法则

1. **少即是多**：前沿 LLM 可以遵循约 150-200 条指令。Claude Code 的系统提示已经使用约 50 条。
2. **通用适用性**：仅包含与每个会话相关的信息。
3. **不要把 Claude 当作 Linter 使用**：使用确定性工具代替。
4. **永远不要自动生成**：CLAUDE.md 是 AI 工具的最高杠杆点。

## 执行流程

### 1. 项目分析

1. 检查现有的 CLAUDE.md 文件
2. 识别项目结构：技术栈、项目类型、开发工具
3. 审查现有文档

### 2. 内容策略（WHAT、WHY、HOW）

- **WHAT**：技术栈概述、项目组织、关键目录
- **WHY**：项目目的、架构决策、主要组件职责
- **HOW**：工作流程、测试程序、验证方法、关键陷阱

### 3. 渐进式披露策略

对于较大的项目，建议创建 `agent_docs/` 文件夹，并在 CLAUDE.md 中引用。

### 4. 质量约束

- **目标行数**：少于 300 行（最好少于 100 行）
- **无样式规则**
- **无任务特定指令**
- **无代码片段**：使用文件引用代替
- **无冗余信息**

### 5. 必要章节

```markdown
# Project Name
Brief one-line description.

## Tech Stack
- Primary language and version
- Key frameworks/libraries
- Database/storage (if any)

## Development Commands
- Install: `command`
- Test: `command`
- Build: `command`

## Critical Conventions
[Only non-obvious, high-impact conventions]

## Known Issues / Gotchas
[Things that consistently trip up developers]
```

### 6. 应避免的反模式

**不要包括：**
- 代码样式指南
- 关于如何使用 Claude 的文档
- 显而易见模式的冗长解释
- 复制粘贴的代码示例
- 通用最佳实践
- 任务特定指令
- 自动生成的内容

### 7. 验证清单

- [ ] 少于 300 行（最好少于 100 行）
- [ ] 每一行都适用于所有会话
- [ ] 无样式/格式规则
- [ ] 无代码片段
- [ ] 命令经过验证可以工作
- [ ] 对复杂项目使用渐进式披露
- [ ] 记录了关键陷阱
- [ ] 与 README.md 无冗余

## 注意事项

- 在包含之前始终验证命令可以工作
- 如有疑问，保留它——少即是多
- 系统提醒告诉 Claude CLAUDE.md"可能相关也可能不相关"
- Monorepos 最受益于清晰的 WHAT/WHY/HOW 结构
