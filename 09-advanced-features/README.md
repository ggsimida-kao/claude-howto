<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../resources/logos/claude-howto-logo-dark.svg">
  <img alt="Claude How To" src="../resources/logos/claude-howto-logo.svg">
</picture>

# Advanced Features（高级功能）

Claude Code 高级功能综合指南，包括规划模式（Planning Mode）、扩展思考（Extended Thinking）、自动模式（Auto Mode）、后台任务（Background Tasks）、权限模式（Permission Modes）、打印模式（Print Mode，非交互式）、会话管理（Session Management）、交互功能（Interactive Features）、渠道（Channels）、语音听写（Voice Dictation）、远程控制（Remote Control）、Web 会话（Web Sessions）、桌面应用（Desktop App）、任务列表（Task List）、提示建议（Prompt Suggestions）、Git 工作树（Git Worktrees）、沙箱（Sandboxing）、托管设置（Managed Settings）和配置（Configuration）。

## Table of Contents（目录）

1. [Overview（概述）](#overview)
2. [Planning Mode（规划模式）](#planning-mode)
3. [Extended Thinking（扩展思考）](#extended-thinking)
4. [Auto Mode（自动模式）](#auto-mode)
5. [Background Tasks（后台任务）](#background-tasks)
6. [Scheduled Tasks（计划任务）](#scheduled-tasks)
7. [Permission Modes（权限模式）](#permission-modes)
8. [Headless Mode（无头模式）](#headless-mode)
9. [Session Management（会话管理）](#session-management)
10. [Interactive Features（交互功能）](#interactive-features)
11. [Voice Dictation（语音听写）](#voice-dictation)
12. [Channels（渠道）](#channels)
13. [Chrome Integration（Chrome 集成）](#chrome-integration)
14. [Remote Control（远程控制）](#remote-control)
15. [Web Sessions（Web 会话）](#web-sessions)
16. [Desktop App（桌面应用）](#desktop-app)
17. [Task List（任务列表）](#task-list)
18. [Prompt Suggestions（提示建议）](#prompt-suggestions)
19. [Git Worktrees（Git 工作树）](#git-worktrees)
20. [Sandboxing（沙箱）](#sandboxing)
21. [Managed Settings (Enterprise)（托管设置（企业版））](#managed-settings-enterprise)
22. [Configuration and Settings（配置和设置）](#configuration-and-settings)
23. [Best Practices（最佳实践）](#best-practices)
24. [Additional Resources（其他资源）](#additional-resources)

---

## Overview（概述）

Claude Code 的高级功能扩展了核心能力，包括规划、推理、自动化和控制机制。这些功能支持复杂开发任务、代码审查、自动化和多会话管理的复杂工作流。

**主要高级功能包括：**
- **Planning Mode（规划模式）**：在编码前创建详细的实施计划
- **Extended Thinking（扩展思考）**：用于复杂问题的深度推理
- **Auto Mode（自动模式）**：后台安全分类器在执行前审查每个操作（研究预览版）
- **Background Tasks（后台任务）**：运行长时间操作而不阻塞对话
- **Permission Modes（权限模式）**：控制 Claude 可以做什么（`default`、`acceptEdits`、`plan`、`auto`、`dontAsk`、`bypassPermissions`）
- **Print Mode（打印模式）**：非交互式运行 Claude Code 用于自动化和 CI/CD（`claude -p`）
- **Session Management（会话管理）**：管理多个工作会话
- **Interactive Features（交互功能）**：键盘快捷键、多行输入和命令历史
- **Voice Dictation（语音听写）**：支持 20 种语言的按键通话语音输入
- **Channels（渠道）**：MCP 服务器将消息推送到运行中的会话（研究预览版）
- **Remote Control（远程控制）**：从 Claude.ai 或 Claude 应用控制 Claude Code
- **Web Sessions（Web 会话）**：在 claude.ai/code 的浏览器中运行 Claude Code
- **Desktop App（桌面应用）**：用于可视化差异审查和多个会话的独立应用
- **Task List（任务列表）**：跨上下文压缩持久化任务跟踪
- **Prompt Suggestions（提示建议）**：基于上下文的智能命令建议
- **Git Worktrees（Git 工作树）**：用于并行工作的隔离工作树分支
- **Sandboxing（沙箱）**：操作系统级文件系统和网络隔离
- **Managed Settings（托管设置）**：通过 plist、Registry 或托管文件进行企业部署
- **Configuration（配置）**：使用 JSON 配置文件自定义行为

---

## Planning Mode（规划模式）

规划模式允许 Claude 在实施复杂任务之前进行思考，创建一个您可以审查和批准的详细计划。

### 什么是规划模式？

规划模式是一种两阶段方法：
1. **规划阶段**：Claude 分析任务并创建详细的实施计划
2. **实施阶段**：批准后，Claude 执行计划

### 何时使用规划模式

✅ 使用规划模式用于：
- 复杂的多文件重构
- 新功能实施
- 架构更改
- 数据库迁移
- 主要 API 重新设计

❌ 不要使用规划模式用于：
- 简单的 bug 修复
- 格式化更改
- 单文件编辑
- 快速查询

### 激活规划模式

**斜杠命令**：
```bash
/plan Implement user authentication system
```

**CLI 标志**：
```bash
claude --permission-mode plan
```

**设为默认**：
```json
{
  "permissions": {
    "defaultMode": "plan"
  }
}
```

**键盘快捷键**：
- `Shift + Tab` - 切换权限模式（包括计划）
- `Alt + M` - 切换权限模式（Windows/Linux）

### 规划模式的好处

- **结构化实施方法**：详细的实施步骤分解
- **审查和批准**：执行前批准或调整计划
- **风险识别**：实施前识别潜在问题
- **清晰的阶段**：有组织的实施阶段和里程碑

### 示例：功能实施

```
User: /plan Add a real-time notification system

Claude: I'll create a plan for implementing real-time notifications.

## Implementation Plan

### Phase 1: Infrastructure Setup
1. Install WebSocket libraries (socket.io)
2. Set up WebSocket server
3. Configure connection management

### Phase 2: Backend Implementation
4. Create notification service
5. Implement notification queue
6. Add database schema for notifications
7. Create API endpoints

### Phase 3: Frontend Integration
8. Set up WebSocket client
9. Create notification UI components
10. Implement notification state management
11. Add notification permissions

### Phase 4: Testing & Deployment
12. Write unit tests
13. Write integration tests
14. Update documentation
15. Deploy to staging

Estimated time: 3-4 hours
Files to modify: 12
New files to create: 8

Ready to proceed? (yes/no/modify plan)

User: yes

Claude: [Begins implementation following the plan]
```

### 计划修改

```
User: Modify the plan - skip the queue for now, we'll add it later

Claude: Updated plan:
[Shows modified plan with queue removed]

User: Looks good, proceed

Claude: [Implements modified plan]
```

### 规划模式配置

规划模式通过 CLI 标志或斜杠命令激活：

```bash
# Activate plan mode via CLI
claude --permission-mode plan

# Or use the /plan slash command inside the REPL
/plan Implement user authentication system
```

**规划的模型别名**：使用 `opusplan` 作为模型别名来使用 Opus 进行规划，Sonnet 执行：

```bash
claude --model opusplan "design and implement the new API"
```

**外部编辑计划**：按 `Ctrl+G` 在外部编辑器中打开当前计划进行详细修改。

---

## Extended Thinking（扩展思考）

扩展思考允许 Claude 在提供解决方案之前花费更多时间推理复杂问题。

### 什么是扩展思考？

扩展思考是一种深思熟虑的、逐步的推理过程，其中 Claude：
- 分解复杂问题
- 考虑多种方法
- 评估权衡
- 推理边缘情况

### 激活扩展思考

**键盘快捷键**：
- `Option + T`（macOS）/ `Alt + T`（Windows/Linux） - 切换扩展思考

**自动激活**：
- 默认对所有模型启用（Opus 4.6、Sonnet 4.6、Haiku 4.5）
- Opus 4.6：自适应推理，支持努力级别：`low`（○）、`medium`（◐）、`high`（●）、`max`（仅 Opus 4.6）
- 其他模型：固定预算最多 31,999 tokens

**配置方法**：
- 切换：`Alt+T` / `Option+T`，或通过 `/config`
- 查看推理：`Ctrl+O`（详细模式）
- 设置努力级别：`/effort` 命令或 `--effort` 标志

**自定义预算**：
```bash
export MAX_THINKING_TOKENS=1024
```

**努力级别**（仅 Opus 4.6）：
```bash
export CLAUDE_CODE_EFFORT_LEVEL=high   # low (○), medium (◐), high (●), or max (Opus 4.6 only)
```

**CLI 标志**：
```bash
claude --effort high "complex architectural review"
```

**斜杠命令**：
```
/effort high
```

> **注意**：提示词中的关键词 "ultrathink" 激活深度推理模式。努力级别 `low`、`medium`、`high` 和 `max`（仅 Opus 4.6）控制 Claude 执行的推理量。

### 扩展思考的好处

- **深度推理**：花更多时间思考复杂问题
- **更好的架构决策**：通过综合评估做出明智选择
- **边缘情况考虑**：思考潜在问题和场景
- **彻底分析**：复杂问题的结构化方法

### 示例：架构决策

```
User: /think Should we use microservices or a monolith for our e-commerce platform?

Claude: Let me think through this architectural decision carefully...

<extended_thinking>
## Context Analysis
- Team size: 5 developers
- Expected traffic: 10k daily users initially
- Need to scale to 100k+ users
- Limited DevOps resources
- 6-month timeline to MVP

## Approach 1: Microservices
Pros:
+ Independent scaling
+ Technology flexibility
+ Team independence
+ Fault isolation

Cons:
- Operational complexity
- Network overhead
- Distributed tracing needed
- Requires DevOps expertise
- Slower initial development

## Approach 2: Monolith
Pros:
+ Simpler deployment
+ Faster initial development
+ Easier debugging
+ Lower operational overhead
+ Single codebase

Cons:
- Scaling challenges later
- All-or-nothing deployments
- Technology lock-in
- Potential for tight coupling

## Decision Factors
1. Team size (5 devs) → Favors monolith
2. DevOps resources (limited) → Favors monolith
3. Timeline (6 months) → Favors monolith
4. Future scale (100k users) → Achievable with monolith + caching
5. Complexity budget → Limited

## Recommendation
Start with a **modular monolith**:
- Single deployment unit
- Clear module boundaries
- Clean interfaces between modules
- Prepare for future extraction to microservices if needed

This gives you:
✓ Fast initial development
✓ Low operational complexity
✓ Option to extract services later
✓ Clear architecture

Migration path: When you reach 50k+ users or specific modules need independent scaling, extract those modules into microservices.
</extended_thinking>

**Recommendation**: Implement a modular monolith with clean module boundaries.
```

### 扩展思考配置

扩展思考通过环境变量、键盘快捷键和 CLI 标志控制：

```bash
# Set thinking token budget
export MAX_THINKING_TOKENS=16000

# Set effort level (Opus 4.6 only): low (○), medium (◐), high (●), or max (Opus 4.6 only)
export CLAUDE_CODE_EFFORT_LEVEL=high
```

在会话中切换使用 `Alt+T` / `Option+T`，使用 `/effort` 设置努力级别，或通过 `/config` 配置。

---

## Auto Mode（自动模式）

Auto Mode 是一个研究预览版权限模式（2026 年 3 月），使用后台安全分类器在执行前审查每个操作。它允许 Claude 自主工作，同时阻止危险操作。

### 要求

- **计划**：团队计划（企业和 API 滚动推出）
- **模型**：Claude Sonnet 4.6 或 Opus 4.6
- **分类器**：在 Claude Sonnet 4.6 上运行（增加额外 token 成本）

### 启用自动模式

```bash
# Unlock auto mode with CLI flag
claude --enable-auto-mode

# Then cycle to it with Shift+Tab in the REPL
```

或者将其设为默认权限模式：

```bash
claude --permission-mode auto
```

通过配置设置：
```json
{
  "permissions": {
    "defaultMode": "auto"
  }
}
```

### 分类器如何工作

后台分类器使用以下决策顺序评估每个操作：

1. **允许/拒绝规则** -- 首先检查显式权限规则
2. **只读/编辑自动批准** -- 文件读取和编辑自动通过
3. **分类器** -- 后台分类器审查操作
4. **回退** -- 连续 3 次或总共 20 次阻止后回退到提示

### 默认阻止的操作

自动模式默认阻止以下操作：

| 阻止的操作 | 示例 |
|----------------|---------|
| 管道安装 | `curl \| bash` |
| 发送敏感数据到外部 | API 密钥、凭证通过网络传输 |
| 生产部署 | 针对生产环境的部署命令 |
| 批量删除 | 大目录上的 `rm -rf` |
| IAM 更改 | 权限和角色修改 |
| 强制推送到 main | `git push --force origin main` |

### 默认允许的操作

| 允许的操作 | 示例 |
|----------------|---------|
| 本地文件操作 | 读取、写入、编辑项目文件 |
| 声明的依赖安装 | `npm install`、`pip install` 从清单 |
| 只读 HTTP | `curl` 用于获取文档 |
| 推送到当前分支 | `git push origin feature-branch` |

### 配置自动模式

**打印默认规则为 JSON**：
```bash
claude auto-mode defaults
```

**通过 `autoMode.environment` 托管设置配置可信基础设施**，用于企业部署。这允许管理员定义可信的 CI/CD 环境、部署目标和基础设施模式。

### 回退行为

当分类器不确定时，自动模式回退到提示用户：
- 连续 **3 次**分类器阻止后
- 会话中总共 **20 次**分类器阻止后

这确保当分类器无法自信地批准操作时，用户始终保持控制。

### 种子自动模式等效权限（无需团队计划）

如果您没有团队计划或想要一个更简单的方法而不使用后台分类器，您可以向 `~/.claude/settings.json` 种子一个保守的安全权限规则基线。该脚本从只读和本地检查规则开始，然后让您在想要时选择加入编辑、测试、本地 git 写入和 GitHub 写入操作。

---

## Background Tasks（后台任务）

后台任务允许长时间运行的操作在不阻塞对话的情况下执行。

### 什么是后台任务？

后台任务异步运行，而您继续工作：
- 长时间测试套件
- 构建进程
- 数据库迁移
- 部署脚本
- 分析工具

**基本用法：**
```bash
User: Run tests in background

Claude: Started task bg-1234

/task list           # Show all tasks
/task status bg-1234 # Check progress
/task show bg-1234   # View output
/task cancel bg-1234 # Cancel task
```

---

## Permission Modes（权限模式）

权限模式控制 Claude 可以采取哪些操作而无需明确批准。

### 可用的权限模式

| 模式 | 行为 |
|---|---|
| `default` | 仅读取文件；其他所有操作都提示 |
| `acceptEdits` | 读取和编辑文件；命令提示 |
| `plan` | 仅读取文件（研究模式，无编辑） |
| `auto` | 所有操作，带后台安全分类器检查（研究预览版） |
| `bypassPermissions` | 所有操作，无权限检查（危险） |
| `dontAsk` | 仅预批准的工具执行；其他所有工具被拒绝 |

使用 `Shift+Tab` 在 CLI 中循环切换模式。通过 `--permission-mode` 标志或 `permissions.defaultMode` 设置设置默认。

---

## Headless Mode（无头模式）

打印模式（`claude -p`）允许 Claude Code 无需交互式输入即可运行，非常适合自动化和 CI/CD。

---

## Session Management（会话管理）

有效地管理多个 Claude Code 会话。

---

## Interactive Features（交互功能）

### 键盘快捷键

Claude Code 支持键盘快捷键以提高效率。

| 快捷键 | 描述 |
|----------|---------|
| `Ctrl+C` | 取消当前输入/生成 |
| `Ctrl+D` | 退出 Claude Code |
| `Ctrl+G` | 在外部编辑器中编辑计划 |
| `Ctrl+L` | 清除终端屏幕 |
| `Ctrl+O` | 切换详细输出（查看推理） |
| `Ctrl+R` | 反向搜索历史 |
| `Ctrl+T` | 切换任务列表视图 |
| `Ctrl+B` | 后台运行任务 |
| `Esc+Esc` | 回溯代码/对话 |
| `Shift+Tab` / `Alt+M` | 切换权限模式 |
| `Option+P` / `Alt+P` | 切换模型 |
| `Option+T` / `Alt+T` | 切换扩展思考 |

---

## Voice Dictation（语音听写）

语音听写为 Claude Code 提供按键通话语音输入，允许您说话而不是打字输入提示。

---

## Channels（渠道）

渠道（研究预览版）允许 MCP 服务器将消息推送到运行中的 Claude Code 会话，实现与外部服务的实时集成。

---

## Chrome Integration（Chrome 集成）

Chrome 集成将 Claude Code 连接到您的 Chrome 或 Microsoft Edge 浏览器，用于实时网络自动化和调试。

---

## Remote Control（远程控制）

远程控制让您从手机、平板电脑或任何浏览器继续本地运行的 Claude Code 会话。

---

## Web Sessions（Web 会话）

Web 会话允许您直接在浏览器中 claude.ai/code 运行 Claude Code，或从 CLI 创建 Web 会话。

---

## Desktop App（桌面应用）

Claude Code 桌面应用提供一个独立应用程序，具有可视化差异审查、并行会话和集成连接器。

---

## Task List（任务列表）

任务列表功能提供跨上下文压缩（当对话历史被修剪以适应上下文窗口时）的持久化任务跟踪。

---

## Prompt Suggestions（提示建议）

提示建议根据您的 git 历史和当前对话上下文显示灰色示例命令。

---

## Git Worktrees（Git 工作树）

Git 工作树允许您在隔离的工作树中启动 Claude Code，实现不同分支上的并行工作，而无需 stash 或切换。

---

## Sandboxing（沙箱）

沙箱为 Claude Code 执行的 Bash 命令提供操作系统级文件系统和网络隔离。

---

## Managed Settings (Enterprise)（托管设置（企业版））

托管设置使企业管理员能够使用平台原生管理工具在整个组织中部署 Claude Code 配置。

---

## Configuration and Settings（配置和设置）

### 配置文件位置

1. **全局配置**：`~/.claude/config.json`
2. **项目配置**：`./.claude/config.json`
3. **用户配置**：`~/.config/claude-code/settings.json`

---

## Best Practices（最佳实践）

### 规划模式
- ✅ 用于复杂的多步骤任务
- ✅ 批准前审查计划
- ✅ 需要时修改计划
- ❌ 不要用于简单任务

### 扩展思考
- ✅ 用于架构决策
- ✅ 用于复杂问题解决
- ✅ 审查推理过程
- ❌ 不要用于简单查询

### 权限
- ✅ 使用 `plan` 进行代码审查（只读）
- ✅ 使用 `default` 进行交互式开发
- ✅ 使用 `acceptEdits` 进行自动化工作流
- ✅ 使用 `auto` 进行带安全防护的自主工作
- ❌ 除非绝对必要，否则不要使用 `bypassPermissions`

### 会话
- ✅ 为不同任务使用单独的会话
- ✅ 保存重要的会话状态
- ✅ 清理旧会话
- ❌ 不要在同一个会话中混合不相关的工作

---

## Additional Resources（其他资源）

- [Official Interactive Mode Documentation](https://code.claude.com/docs/en/interactive-mode)
- [Official Headless Mode Documentation](https://code.claude.com/docs/en/headless)
- [CLI Reference](https://code.claude.com/docs/en/cli-reference)
- [Checkpoints Guide](../08-checkpoints/) - Session management and rewinding
- [Slash Commands](../01-slash-commands/) - Command reference
- [Memory Guide](../02-memory/) - Persistent context
- [Skills Guide](../03-skills/) - Autonomous capabilities
- [Subagents Guide](../04-subagents/) - Delegated task execution
- [MCP Guide](../05-mcp/) - External data access
- [Hooks Guide](../06-hooks/) - Event-driven automation
- [Plugins Guide](../07-plugins/) - Bundled extensions
