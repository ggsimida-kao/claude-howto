<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../resources/logos/claude-howto-logo-dark.svg">
  <img alt="Claude How To" src="../resources/logos/claude-howto-logo.svg">
</picture>

# Subagents - 完整参考指南

Subagents 是 Claude Code 可以将任务委托给的专业化 AI 助手。每个子代理都有特定目的，使用独立于主对话的上下文窗口，并可以配置特定工具和自定义系统提示。

## 目录

1. [概述](#概述)
2. [关键优势](#关键优势)
3. [文件位置](#文件位置)
4. [配置](#配置)
5. [内置子代理](#内置子代理)
6. [管理子代理](#管理子代理)
7. [使用子代理](#使用子代理)
8. [可恢复代理](#可恢复代理)
9. [链式子代理](#链式子代理)
10. [子代理的持久内存](#子代理的持久内存)
11. [后台子代理](#后台子代理)
12. [工作树隔离](#工作树隔离)
13. [限制可生成的子代理](#限制可生成的子代理)
14. [`claude agents` CLI 命令](#claude-agents-cli-命令)
15. [Agent Teams（实验性）](#agent-teams实验性)
16. [插件子代理安全](#插件子代理安全)
17. [架构](#架构)
18. [上下文管理](#上下文管理)
19. [何时使用子代理](#何时使用子代理)
20. [最佳实践](#最佳实践)
21. [示例子代理](#示例子代理)
22. [安装说明](#安装说明)
23. [相关概念](#相关概念)

---

## 概述

Subagents 通过以下方式实现委托任务执行：
- 创建具有独立上下文窗口的**隔离 AI 助手**
- 提供用于专业知识的**自定义系统提示**
- 强制执行**工具访问控制**以限制能力
- 防止复杂任务造成的**上下文污染**
- 实现多个专业任务的**并行执行**

每个子代理独立操作，只接收其任务所需的特定上下文，然后将结果返回主代理进行综合。

**快速开始**：使用 `/agents` 命令交互式创建、查看、编辑和管理子代理。

---

## 关键优势

| 优势 | 描述 |
|--------|---------|
| **上下文保留** | 在独立上下文中操作，防止主对话污染 |
| **专业知识** | 针对特定领域微调，成功率更高 |
| **可复用性** | 跨不同项目使用并与团队共享 |
| **灵活权限** | 不同子代理类型有不同的工具访问级别 |
| **可扩展性** | 多个代理同时处理不同方面 |

---

## 文件位置

| 优先级 | 类型 | 位置 | 作用域 |
|----------|------|----------|-------|
| 1（最高） | **CLI 定义** | 通过 `--agents` 标志（JSON） | 仅会话 |
| 2 | **项目子代理** | `.claude/agents/` | 当前项目 |
| 3 | **用户子代理** | `~/.claude/agents/` | 所有项目 |
| 4（最低） | **插件代理** | 插件 `agents/` 目录 | 通过插件 |

---

## 配置

### 文件格式

Subagents 通过 YAML 前置matter定义，后跟 markdown 中的系统提示：

```yaml
---
name: your-sub-agent-name
description: Description of when this subagent should be invoked
tools: tool1, tool2, tool3  # Optional
disallowedTools: tool4  # Optional
model: sonnet  # Optional
skills: skill1, skill2  # Optional
memory: user  # Optional
background: false  # Optional
effort: high  # Optional
isolation: worktree  # Optional
---

Your subagent's system prompt goes here.
```

### 配置字段

| 字段 | 必需 | 描述 |
|-------|----------|---------|
| `name` | 是 | 唯一标识符 |
| `description` | 是 | 用途的自然语言描述 |
| `tools` | 否 | 特定工具列表 |
| `disallowedTools` | 否 | 明确禁止的工具 |
| `model` | 否 | 使用的模型 |
| `skills` | 否 | 预加载到上下文的 Skills |
| `memory` | 否 | 持久内存目录作用域 |
| `background` | 否 | 设为 `true` 作为后台任务运行 |
| `effort` | 否 | 推理努力级别 |
| `isolation` | 否 | 设为 `worktree` 获取独立 git worktree |

---

## 内置子代理

| 代理 | 模型 | 用途 |
|-------|-------|---------|
| **general-purpose** | 继承 | 复杂多步骤任务 |
| **Plan** | 继承 | 计划模式研究 |
| **Explore** | Haiku | 只读代码库探索 |
| **Bash** | 继承 | 终端命令 |
| **Claude Code Guide** | Haiku | 回答 Claude Code 功能问题 |

### Explore 代理

| 属性 | 值 |
|----------|-------|
| **模型** | Haiku（快速、低延迟） |
| **模式** | 严格只读 |
| **工具** | Glob、Grep、Read、Bash（只读命令） |
| **用途** | 快速代码库搜索和分析 |

---

## 使用子代理

### 自动委托

Claude 根据以下内容主动委托任务：
- 任务描述
- 子代理配置中的 `description` 字段
- 当前上下文和可用工具

### 明确调用

```
> Use the test-runner subagent to fix failing tests
> Have the code-reviewer subagent look at my recent changes
```

### @-提及调用

```
> @"code-reviewer (agent)" review the auth module
```

---

## 可恢复代理

Subagents 可以从完全保留上下文的先前对话继续：

```bash
# Initial invocation
> Use the code-analyzer agent to start reviewing the authentication module
# Returns agentId: "abc123"

# Resume the agent later
> Resume agent abc123 and now analyze the authorization logic as well
```

---

## 链式子代理

按顺序执行多个子代理：

```bash
> First use the code-analyzer subagent to find performance issues,
  then use the optimizer subagent to fix them
```

---

## 子代理的持久内存

`memory` 字段为子代理提供跨会话持久的目录。

### 内存作用域

| 作用域 | 目录 | 用例 |
|-------|-----------|---------|
| `user` | `~/.claude/agent-memory/<name>/` | 跨所有项目的个人笔记 |
| `project` | `.claude/agent-memory/<name>/` | 与团队共享的项目知识 |
| `local` | `.claude/agent-memory-local/<name>/` | 不提交到版本控制的本地知识 |

---

## 后台子代理

Subagents 可以在后台运行，释放主对话处理其他任务。

### 键盘快捷键

| 快捷键 | 操作 |
|----------|--------|
| `Ctrl+B` | 将当前运行的子代理任务放到后台 |
| `Ctrl+F` | 终止所有后台代理（按两次确认） |

---

## 工作树隔离

`isolation: worktree` 设置为子代理提供自己的 git worktree，允许它独立进行更改而不影响主工作树。

---

## Agent Teams（实验性）

Agent Teams 协调多个 Claude Code 实例共同处理复杂任务。与子代理不同，团队成员独立工作，通过共享邮箱系统直接通信。

### 子代理 vs Agent Teams

| 方面 | 子代理 | Agent Teams |
|--------|-----------|-------------|
| **委托模型** | 父代理委托子任务，等待结果 | 团队负责人分配工作，团队成员独立执行 |
| **上下文** | 每个子任务全新上下文，结果提炼回来 | 每个团队成员维护自己的持久上下文 |
| **协调** | 顺序或并行，由父代理管理 | 通过共享任务列表和自动依赖管理 |
| **通信** | 仅返回值 | 通过邮箱进行代理间消息传递 |
| **最佳用途** | 专注、定义明确的子任务 | 需要并行工作的大型多文件项目 |

### 启用 Agent Teams

```bash
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1
```

---

## 架构

### 子代理生命周期

```
User -> Main Agent -> CodeReviewer Subagent
                   -> Tester Subagent
                   -> Docs Subagent
Main Agent -> Synthesizes results -> User
```

### 上下文管理

- 每个子代理获得一个**全新的上下文窗口**，没有主对话历史
- 只有**相关上下文**传递给子代理执行其特定任务
- 结果被**提炼**回主代理
- 这防止了长项目中的**上下文 token 耗尽**

---

## 何时使用子代理

| 场景 | 使用子代理 | 为什么 |
|----------|--------------|---------|
| 复杂功能，很多步骤 | 是 | 分离关注点，防止上下文污染 |
| 快速代码审查 | 否 | 不必要的开销 |
| 并行任务执行 | 是 | 每个子代理有自己的上下文 |
| 需要专业知识 | 是 | 自定义系统提示 |
| 长时分析 | 是 | 防止主上下文耗尽 |
| 单个任务 | 否 | 不必要地增加延迟 |

---

## 最佳实践

### 设计原则

**做：**
- 从 Claude 生成的代理开始
- 设计专注的子代理
- 写详细提示
- 限制工具访问
- 版本控制项目子代理

**不做：**
- 创建重叠的同角色子代理
- 给子代理不必要的工具访问
- 对简单的单步任务使用子代理
- 在一个子代理中混合关注点

---

## 示例子代理

### 1. Code Reviewer（code-reviewer.md）

**用途**：全面的代码质量和可维护性分析

**工具**：Read、Grep、Glob、Bash

**专业**：安全漏洞检测、性能优化识别、可维护性评估、测试覆盖率分析

### 2. Test Engineer（test-engineer.md）

**用途**：测试策略、覆盖率分析和自动化测试

**工具**：Read、Write、Bash、Grep

**专业**：单元测试创建、集成测试设计、边缘情况识别

### 3. Documentation Writer（documentation-writer.md）

**用途**：技术文档、API 文档和用户指南

**工具**：Read、Write、Grep

**专业**：API 端点文档、用户指南创建、架构文档

### 4. Secure Reviewer（secure-reviewer.md）

**用途**：专注安全的代码审查，最小权限

**工具**：Read、Grep

**专业**：安全漏洞检测、认证/授权问题、数据暴露风险

### 5. Implementation Agent（implementation-agent.md）

**用途**：功能开发的完整实现能力

**工具**：Read、Write、Edit、Bash、Grep、Glob

**专业**：功能实现、代码生成、构建和测试执行

### 6. Debugger（debugger.md）

**用途**：错误、测试失败和意外行为的调试专家

**工具**：Read、Edit、Bash、Grep、Glob

**专业**：根本原因分析、错误调查、测试失败解决

### 7. Data Scientist（data-scientist.md）

**用途**：SQL 查询和数据洞察的数据分析专家

**工具**：Bash、Read、Write

**专业**：SQL 查询优化、BigQuery 操作、数据分析和统计洞察

---

## 安装说明

### 方法 1：使用 /agents 命令（推荐）

```bash
/agents
```

### 方法 2：复制到项目

```bash
mkdir -p .claude/agents
cp /path/to/04-subagents/*.md .claude/agents/
rm .claude/agents/README.md
```

### 方法 3：复制到用户目录

```bash
mkdir -p ~/.claude/agents
cp /path/to/04-subagents/*.md ~/.claude/agents/
```

---

## 相关概念

| 功能 | 用户调用 | 自动调用 | 持久 | 外部访问 | 隔离上下文 |
|---------|--------------|--------------|-----------|------------------|------------------|
| **斜杠命令** | 是 | 否 | 否 | 否 | 否 |
| **子代理** | 是 | 是 | 否 | 否 | 是 |
| **Memory** | 自动 | 自动 | 是 | 否 | 否 |
| **MCP** | 自动 | 是 | 否 | 是 | 否 |
| **Skills** | 是 | 是 | 否 | 否 | 否 |

---

*最后更新：2026 年 3 月*
