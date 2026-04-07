<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../resources/logos/claude-howto-logo-dark.svg">
  <img alt="Claude How To" src="../resources/logos/claude-howto-logo.svg">
</picture>

# Agent Skills 指南

Agent Skills 是可复用的、基于文件系统的能力扩展，可以将 Claude 的功能转化为专业领域专家。它们将特定领域的专业知识、工作流程和最佳实践打包成可发现的组件，当相关任务出现时 Claude 会自动使用。

## 概述

**Agent Skills** 是模块化的能力增强单元，可以将通用型 Agent 转化为专业专家。与提示词（针对一次性任务的对话级指令）不同，Skills 按需加载，无需在多个对话中重复提供相同的指导。

### 关键优势

- **专业化**：为特定领域任务定制能力
- **减少重复**：创建一次，自动在多个对话中使用
- **组合能力**：组合 Skills 构建复杂工作流程
- **扩展工作流程**：跨多个项目和团队复用 Skills
- **保证质量**：将最佳实践直接嵌入工作流程

Skills 遵循 [Agent Skills](https://agentskills.io) 开放标准，可在多种 AI 工具间通用。Claude Code 在标准基础上增加了额外功能，如调用控制、子代理执行和动态上下文注入。

> **注意**：自定义斜杠命令已合并到 Skills 中。`.claude/commands/` 文件仍然有效并支持相同的前置matter字段。推荐在新开发中使用 Skills。当同一路径存在两者时（如 `.claude/commands/review.md` 和 `.claude/skills/review/SKILL.md`），Skill 优先。

## Skills 工作原理：渐进式披露

Skills 利用**渐进式披露**架构——Claude 根据需要分阶段加载信息，而不是预先消耗上下文。这实现了高效的上下文管理，同时保持无限的可扩展性。

### 三级加载

| 级别 | 加载时机 | Token 消耗 | 内容 |
|-------|------------|------------|-------|
| **Level 1: Metadata** | 始终（启动时） | 每个 Skill 约 100 tokens | YAML 前置matter中的 `name` 和 `description` |
| **Level 2: Instructions** | Skill 被触发时 | 5k tokens 以内 | SKILL.md 正文，包含工作流程和指导 |
| **Level 3+: Resources** | 按需 | 实际无限制 | 通过 bash 执行的脚本、模板、文档，不加载内容到上下文 |

这意味着你可以安装许多 Skills 而不会产生上下文惩罚——Claude 只知道每个 Skill 的存在和何时使用它，直到真正被触发。

## Skill 类型与位置

| 类型 | 位置 | 作用域 | 共享 | 适用于 |
|------|----------|-------|--------|----------|
| **Enterprise** | 托管设置 | 所有组织用户 | 是 | 组织级标准 |
| **Personal** | `~/.claude/skills/<skill-name>/SKILL.md` | 个人 | 否 | 个人工作流程 |
| **Project** | `.claude/skills/<skill-name>/SKILL.md` | 团队 | 是（通过 git） | 团队标准 |
| **Plugin** | `<plugin>/skills/<skill-name>/SKILL.md` | 启用插件处 | 取决于插件 | 与插件捆绑 |

当多个级别存在同名 Skill 时，优先级高的位置优先：**enterprise > personal > project**。Plugin Skills 使用 `plugin-name:skill-name` 命名空间，不会冲突。

### 自动发现

**嵌套目录**：当你在子目录中处理文件时，Claude Code 会自动从嵌套的 `.claude/skills/` 目录发现 Skills。

**`--add-dir` 目录**：通过 `--add-dir` 添加的目录中的 Skills 会自动加载并具有实时变更检测。

**描述预算**：Skill 描述（Level 1 元数据）上限为上下文窗口的 **2%**（回退：**16,000 字符**）。

## 创建自定义 Skills

### 基本目录结构

```
my-skill/
├── SKILL.md           # 主指令（必需）
├── template.md        # Claude 填充的模板
├── examples/
│   └── sample.md      # 显示预期格式的示例输出
└── scripts/
    └── validate.sh    # Claude 可执行的脚本
```

### SKILL.md 格式

```yaml
---
name: your-skill-name
description: Brief description of what this Skill does and when to use it
---

# Your Skill Name

## Instructions
Provide clear, step-by-step guidance for Claude.

## Examples
Show concrete examples of using this Skill.
```

### 必需字段

- **name**：仅使用小写字母、数字和连字符（最多 64 个字符）。不能包含 "anthropic" 或 "claude"。
- **description**：Skill 做什么以及何时使用（最多 1024 个字符）。

### 可选前置matter字段

| 字段 | 描述 |
|-------|-------|
| `name` | 仅小写字母、数字、连字符（最多 64 字符） |
| `description` | Skill 做什么以及何时使用（最多 1024 字符） |
| `argument-hint` | `/` 自动补全菜单中显示的提示 |
| `disable-model-invocation` | `true` = 仅用户可通过 `/name` 调用 |
| `user-invocable` | `false` = 从 `/` 菜单隐藏 |
| `allowed-tools` | Skill 可使用而无需权限提示的工具列表 |
| `model` | Skill 激活时的模型覆盖 |
| `effort` | Skill 激活时的工作量级别覆盖：`low`、`medium`、`high` 或 `max` |
| `context` | `fork` 在隔离子代理上下文中运行 Skill |
| `agent` | `context: fork` 时的子代理类型 |
| `shell` | `!`command`` 替换和脚本使用的 shell：`bash` 或 `powershell` |
| `hooks` | 作用域限定到此 Skill 生命周期的钩子 |

## Skills 与其他功能

| 功能 | 调用方式 | 适用于 |
|---------|------------|---------|
| **Skills** | 自动或 `/name` | 可复用专业知识、工作流程 |
| **斜杠命令** | 用户发起 `/name` | 快速快捷方式（已合并到 Skills） |
| **子代理** | 自动委托 | 隔离任务执行 |
| **Memory (CLAUDE.md)** | 始终加载 | 持久项目上下文 |
| **MCP** | 实时 | 外部数据/服务访问 |
| **钩子** | 事件驱动 | 自动副作用 |

## 捆绑 Skills

Claude Code 附带多个内置 Skills，无需安装即可始终使用：

| Skill | 描述 |
|-------|-------|
| `/simplify` | 审查更改的文件以实现复用、质量和效率；生成 3 个并行审查代理 |
| `/batch <instruction>` | 使用 git worktrees 跨代码库编排大规模并行更改 |
| `/debug [description]` | 通过读取调试日志排除当前会话故障 |
| `/loop [interval] <prompt>` | 重复运行提示 |
| `/claude-api` | 加载 Claude API/SDK 参考 |

## 其他资源

- [官方 Skills 文档](https://code.claude.com/docs/en/skills)
- [Agent Skills 架构博客](https://claude.com/blog/equipping-agents-for-the-real-world-with-agent-skills)
- [Skills 仓库](https://github.com/luongnv89/skills)
- [斜杠命令指南](../01-slash-commands/)
- [子代理指南](../04-subagents/)
- [Memory 指南](../02-memory/)
- [MCP（Model Context Protocol）](../05-mcp/)
- [钩子指南](../06-hooks/)
