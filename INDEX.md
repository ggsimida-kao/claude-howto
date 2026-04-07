<picture>
  <source media="(prefers-color-scheme: dark)" srcset="resources/logos/claude-howto-logo-dark.svg">
  <img alt="Claude How To" src="resources/logos/claude-howto-logo.svg">
</picture>

# Claude Code 示例 - 完整索引

本文档提供了按功能类型组织的所有示例文件的完整索引。

## 摘要统计

- **总文件数**：100+ 个文件
- **类别**：10 个功能类别
- **Plugins**：3 个完整 plugins
- **Skills**：6 个完整 skills
- **Hooks**：8 个示例 hooks
- **可直接使用**：所有示例

---

## 01. 斜杠命令（10 个文件）

用户触发的常见工作流快捷方式。

| 文件 | 描述 | 使用场景 |
|------|-------------|----------|
| `optimize.md` | 代码优化分析器 | 发现性能问题 |
| `pr.md` | 拉取请求准备 | PR 工作流自动化 |
| `generate-api-docs.md` | API 文档生成器 | 生成 API 文档 |
| `commit.md` | 提交消息助手 | 标准化提交 |
| `setup-ci-cd.md` | CI/CD 管道设置 | DevOps 自动化 |
| `push-all.md` | 推送所有更改 | 快速推送工作流 |
| `unit-test-expand.md` | 扩展单元测试覆盖率 | 测试自动化 |
| `doc-refactor.md` | 文档重构 | 文档改进 |
| `pr-slash-command.png` | 截图示例 | 可视参考 |
| `README.md` | 文档 | 设置和使用指南 |

**安装路径**：`.claude/commands/`

**使用**：`/optimize`、`/pr`、`/generate-api-docs`、`/commit`、`/setup-ci-cd`、`/push-all`、`/unit-test-expand`、`/doc-refactor`

---

## 02. Memory（6 个文件）

持久化上下文和项目标准。

| 文件 | 描述 | 范围 | 位置 |
|------|-------------|-------|----------|
| `project-CLAUDE.md` | 团队项目标准 | 项目级 | `./CLAUDE.md` |
| `directory-api-CLAUDE.md` | API 特定规则 | 目录 | `./src/api/CLAUDE.md` |
| `personal-CLAUDE.md` | 个人偏好 | 用户 | `~/.claude/CLAUDE.md` |
| `memory-saved.png` | 截图：已保存的 memory | - | 可视参考 |
| `memory-ask-claude.png` | 截图：询问 Claude | - | 可视参考 |
| `README.md` | 文档 | - | 参考 |

**安装**：复制到适当位置

**使用**：由 Claude 自动加载

---

## 03. Skills（28 个文件）

带脚本和模板的自动调用能力。

### 代码审查 Skill（5 个文件）
```
code-review/
├── SKILL.md                          # Skill 定义
├── scripts/
│   ├── analyze-metrics.py            # 代码指标分析器
│   └── compare-complexity.py         # 复杂度比较
└── templates/
    ├── review-checklist.md           # 审查清单
    └── finding-template.md           # 发现文档
```

**目的**：综合代码审查，包含安全、性能和质量分析

**自动调用**：审查代码时

---

### 品牌语音 Skill（4 个文件）
```
brand-voice/
├── SKILL.md                          # Skill 定义
├── templates/
│   ├── email-template.txt            # 邮件格式
│   └── social-post-template.txt      # 社交媒体格式
└── tone-examples.md                  # 示例消息
```

**目的**：确保通信中的品牌声音一致性

**自动调用**：创建营销文案时

---

### 文档生成器 Skill（2 个文件）
```
doc-generator/
├── SKILL.md                          # Skill 定义
└── generate-docs.py                  # Python 文档提取器
```

**目的**：从源代码生成综合 API 文档

**自动调用**：创建/更新 API 文档时

---

### 重构 Skill（5 个文件）
```
refactor/
├── SKILL.md                          # Skill 定义
├── scripts/
│   ├── analyze-complexity.py         # 复杂度分析器
│   └── detect-smells.py              # 代码味道检测器
├── references/
│   ├── code-smells.md                # 代码味道目录
│   └── refactoring-catalog.md        # 重构模式
└── templates/
    └── refactoring-plan.md           # 重构计划模板
```

**目的**：带复杂度分析的系统性代码重构

**自动调用**：重构代码时

---

### Claude MD Skill（1 个文件）
```
claude-md/
└── SKILL.md                          # Skill 定义
```

**目的**：管理和优化 CLAUDE.md 文件

---

### 博客草稿 Skill（3 个文件）
```
blog-draft/
├── SKILL.md                          # Skill 定义
└── templates/
    ├── draft-template.md             # 博客草稿模板
    └── outline-template.md           # 博客大纲模板
```

**目的**：以一致结构起草博客文章

**另外**：`README.md` - Skills 概述和使用指南

**安装路径**：`~/.claude/skills/` 或 `.claude/skills/`

---

## 04. Subagents（9 个文件）

具有自定义能力的专业 AI 助手。

| 文件 | 描述 | 工具 | 使用场景 |
|------|-------------|-------|----------|
| `code-reviewer.md` | 代码质量分析 | read、grep、diff、lint_runner | 综合审查 |
| `test-engineer.md` | 测试覆盖率分析 | read、write、bash、grep | 测试自动化 |
| `documentation-writer.md` | 文档创建 | read、write、grep | 文档生成 |
| `secure-reviewer.md` | 安全审查（只读） | read、grep | 安全审计 |
| `implementation-agent.md` | 完整实现 | read、write、bash、grep、edit、glob | 功能开发 |
| `debugger.md` | 调试专家 | read、bash、grep | Bug 调查 |
| `data-scientist.md` | 数据分析专家 | read、write、bash | 数据工作流 |
| `clean-code-reviewer.md` | 清洁代码标准 | read、grep | 代码质量 |
| `README.md` | 文档 | - | 设置和使用指南 |

**安装路径**：`.claude/agents/`

**使用**：由主 agent 自动委托

---

## 05. MCP Protocol（5 个文件）

外部工具和 API 集成。

| 文件 | 描述 | 集成对象 | 使用场景 |
|------|-------------|-----------------|----------|
| `github-mcp.json` | GitHub 集成 | GitHub API | PR/issue 管理 |
| `database-mcp.json` | 数据库查询 | PostgreSQL/MySQL | 实时数据查询 |
| `filesystem-mcp.json` | 文件操作 | 本地文件系统 | 文件管理 |
| `multi-mcp.json` | 多个服务器 | GitHub + DB + Slack | 完整集成 |
| `README.md` | 文档 | - | 设置和使用指南 |

**安装路径**：`.mcp.json`（项目范围）或 `~/.claude.json`（用户范围）

**使用**：`/mcp__github__list_prs` 等

---

## 06. Hooks（9 个文件）

自动执行的事件驱动自动化脚本。

| 文件 | 描述 | 事件 | 使用场景 |
|------|-------------|-------|----------|
| `format-code.sh` | 自动格式化代码 | PreToolUse:Write | 代码格式化 |
| `pre-commit.sh` | 提交前运行测试 | PreToolUse:Bash | 测试自动化 |
| `security-scan.sh` | 安全扫描 | PostToolUse:Write | 安全检查 |
| `log-bash.sh` | 记录 bash 命令 | PostToolUse:Bash | 命令日志 |
| `validate-prompt.sh` | 验证提示词 | PreToolUse | 输入验证 |
| `notify-team.sh` | 发送通知 | Notification | 团队通知 |
| `context-tracker.py` | 跟踪上下文窗口使用 | PostToolUse | 上下文监控 |
| `context-tracker-tiktoken.py` | 基于 token 的上下文跟踪 | PostToolUse | 精确 token 计数 |
| `README.md` | 文档 | - | 设置和使用指南 |

**安装路径**：在 `~/.claude/settings.json` 中配置

**使用**：在设置中配置，自动执行

**Hook 类型**（4 种类型，25 个事件）：
- 工具 Hooks：PreToolUse、PostToolUse、PostToolUseFailure、PermissionRequest
- 会话 Hooks：SessionStart、SessionEnd、Stop、StopFailure、SubagentStart、SubagentStop
- 任务 Hooks：UserPromptSubmit、TaskCompleted、TaskCreated、TeammateIdle
- 生命周期 Hooks：ConfigChange、CwdChanged、FileChanged、PreCompact、PostCompact、WorktreeCreate、WorktreeRemove、Notification、InstructionsLoaded、Elicitation、ElicitationResult

---

## 07. Plugins（3 个完整 plugins，40 个文件）

捆绑的功能集合。

### PR 审查 Plugin（10 个文件）
```
pr-review/
├── .claude-plugin/
│   └── plugin.json                   # Plugin 清单
├── commands/
│   ├── review-pr.md                  # 综合审查
│   ├── check-security.md             # 安全检查
│   └── check-tests.md                # 测试覆盖率检查
├── agents/
│   ├── security-reviewer.md          # 安全专家
│   ├── test-checker.md               # 测试专家
│   └── performance-analyzer.md       # 性能专家
├── mcp/
│   └── github-config.json            # GitHub 集成
├── hooks/
│   └── pre-review.js                 # 预审查验证
└── README.md                         # Plugin 文档
```

**功能**：安全分析、测试覆盖率、性能影响

**命令**：`/review-pr`、`/check-security`、`/check-tests`

**安装**：`/plugin install pr-review`

---

### DevOps 自动化 Plugin（15 个文件）
```
devops-automation/
├── .claude-plugin/
│   └── plugin.json                   # Plugin 清单
├── commands/
│   ├── deploy.md                     # 部署
│   ├── rollback.md                   # 回滚
│   ├── status.md                    # 系统状态
│   └── incident.md                  # 事件响应
├── agents/
│   ├── deployment-specialist.md      # 部署专家
│   ├── incident-commander.md         # 事件协调员
│   └── alert-analyzer.md             # 告警分析器
├── mcp/
│   └── kubernetes-config.json        # Kubernetes 集成
├── hooks/
│   ├── pre-deploy.js                 # 预部署检查
│   └── post-deploy.js                # 部署后任务
├── scripts/
│   ├── deploy.sh                     # 部署自动化
│   ├── rollback.sh                   # 回滚自动化
│   └── health-check.sh               # 健康检查
└── README.md                         # Plugin 文档
```

**功能**：Kubernetes 部署、回滚、监控、事件响应

**命令**：`/deploy`、`/rollback`、`/status`、`/incident`

**安装**：`/plugin install devops-automation`

---

### 文档 Plugin（14 个文件）
```
documentation/
├── .claude-plugin/
│   └── plugin.json                   # Plugin 清单
├── commands/
│   ├── generate-api-docs.md          # API 文档生成
│   ├── generate-readme.md           # README 创建
│   ├── sync-docs.md                  # 文档同步
│   └── validate-docs.md              # 文档验证
├── agents/
│   ├── api-documenter.md             # API 文档专家
│   ├── code-commentator.md           # 代码注释专家
│   └── example-generator.md          # 示例创建器
├── mcp/
│   └── github-docs-config.json       # GitHub 集成
├── templates/
│   ├── api-endpoint.md               # API 端点模板
│   ├── function-docs.md              # 函数文档模板
│   └── adr-template.md               # ADR 模板
└── README.md                         # Plugin 文档
```

**功能**：API 文档、README 生成、文档同步、验证

**命令**：`/generate-api-docs`、`/generate-readme`、`/sync-docs`、`/validate-docs`

**安装**：`/plugin install documentation`

**另外**：`README.md` - Plugins 概述和使用指南

---

## 08. Checkpoints 和 Rewind（2 个文件）

保存会话状态并探索替代方法。

| 文件 | 描述 | 内容 |
|------|-------------|---------|
| `README.md` | 文档 | 综合 checkpoint 指南 |
| `checkpoint-examples.md` | 真实示例 | 数据库迁移、性能优化、UI 迭代、调试 |

**核心概念**：
- **Checkpoint**：会话状态的快照
- **Rewind**：返回之前的 checkpoint
- **Branch Point**：从同一 checkpoint 探索多种方法

**使用**：
```
# Checkpoints 在每个用户提示词时自动创建
# 要 rewind，按 Esc 两次或使用：
/rewind
# 然后选择：恢复代码和对话、仅恢复对话、仅恢复代码、从这里总结、或算了
```

**使用场景**：
- 尝试不同实现
- 从错误中恢复
- 安全实验
- 比较解决方案
- A/B 测试

---

## 09. 高级功能（3 个文件）

用于复杂工作流的高级能力。

| 文件 | 描述 | 功能 |
|------|-------------|----------|
| `README.md` | 完整指南 | 所有高级功能文档 |
| `config-examples.json` | 配置示例 | 10+ 特定场景配置 |
| `planning-mode-examples.md` | Planning 示例 | REST API、数据库迁移、重构 |
| 计划任务 | 使用 `/loop` 和 cron 工具的重复任务 | 自动化重复工作流 |
| Chrome 集成 | 通过无头 Chromium 的浏览器自动化 | 网页测试和抓取 |
| 远程控制（扩展） | 连接方法、安全性、对比表 | 远程会话管理 |
| 键盘自定义 | 自定义键绑定、组合键支持、上下文 | 个性化快捷方式 |
| 桌面应用（扩展） | 连接器、launch.json、企业功能 | 桌面集成 |

**涵盖的高级功能**：

### Planning Mode
- 创建详细实现计划
- 时间估算和风险评估
- 系统性任务分解

### Extended Thinking
- 复杂问题的深度推理
- 架构决策分析
- 权衡评估

### 后台任务
- 不阻塞的长时间运行操作
- 并行开发工作流
- 任务管理和监控

### 权限模式
- **default**：风险操作前请求批准
- **acceptEdits**：自动接受文件编辑，其他则询问
- **plan**：只读分析，不修改
- **auto**：自动批准安全操作，风险操作则提示
- **dontAsk**：接受除风险操作外的所有操作
- **bypassPermissions**：接受所有（需要 `--dangerously-skip-permissions`）

### Headless Mode（`claude -p`）
- CI/CD 集成
- 自动化任务执行
- 批处理

### 会话管理
- 多个工作会话
- 会话切换和保存
- 会话持久化

### 交互功能
- 键盘快捷键
- 命令历史
- Tab 补全
- 多行输入

### 配置
- 全面的设置管理
- 环境特定配置
- 按项目自定义

### 计划任务
- 使用 `/loop` 命令的重复任务
- Cron 工具：CronCreate、CronList、CronDelete
- 自动化重复工作流

### Chrome 集成
- 通过无头 Chromium 的浏览器自动化
- 网页测试和抓取能力
- 页面交互和数据提取

### 远程控制（扩展）
- 连接方法和协议
- 安全考虑和最佳实践
- 远程访问选项对比表

### 键盘自定义
- 自定义键绑定配置
- 多键快捷方式的组合键支持
- 上下文感知键绑定激活

### 桌面应用（扩展）
- 用于 IDE 集成的连接器
- launch.json 配置
- 企业功能和使用

---

## 10. CLI 使用（1 个文件）

命令行接口使用模式和参考。

| 文件 | 描述 | 内容 |
|------|-------------|----------|
| `README.md` | CLI 文档 | 标志、选项和使用模式 |

**关键 CLI 功能**：
- `claude` - 启动交互式会话
- `claude -p "prompt"` - 无头/非交互模式
- `claude web` - 启动网页会话
- `claude --model` - 选择模型（Sonnet 4.6、Opus 4.6）
- `claude --permission-mode` - 设置权限模式
- `claude --remote` - 通过 WebSocket 启用远程控制

---

## 文档文件（13 个文件）

| 文件 | 位置 | 描述 |
|------|----------|-------------|
| `README.md` | `/` | 主示例概述 |
| `INDEX.md` | `/` | 本完整索引 |
| `QUICK_REFERENCE.md` | `/` | 快速参考卡 |
| `README.md` | `/01-slash-commands/` | 斜杠命令指南 |
| `README.md` | `/02-memory/` | Memory 指南 |
| `README.md` | `/03-skills/` | Skills 指南 |
| `README.md` | `/04-subagents/` | Subagents 指南 |
| `README.md` | `/05-mcp/` | MCP 指南 |
| `README.md` | `/06-hooks/` | Hooks 指南 |
| `README.md` | `/07-plugins/` | Plugins 指南 |
| `README.md` | `/08-checkpoints/` | Checkpoints 指南 |
| `README.md` | `/09-advanced-features/` | 高级功能指南 |
| `README.md` | `/10-cli/` | CLI 指南 |

---

## 完整文件树

```
claude-howto/
├── README.md                                    # 主概述
├── INDEX.md                                     # 本文件
├── QUICK_REFERENCE.md                           # 快速参考卡
├── claude_concepts_guide.md                     # 原指南
│
├── 01-slash-commands/                           # 斜杠命令
│   ├── optimize.md
│   ├── pr.md
│   ├── generate-api-docs.md
│   ├── commit.md
│   ├── setup-ci-cd.md
│   ├── push-all.md
│   ├── unit-test-expand.md
│   ├── doc-refactor.md
│   ├── pr-slash-command.png
│   └── README.md
│
├── 02-memory/                                   # Memory
│   ├── project-CLAUDE.md
│   ├── directory-api-CLAUDE.md
│   ├── personal-CLAUDE.md
│   ├── memory-saved.png
│   ├── memory-ask-claude.png
│   └── README.md
│
├── 03-skills/                                   # Skills
│   ├── code-review/
│   │   ├── SKILL.md
│   │   ├── scripts/
│   │   │   ├── analyze-metrics.py
│   │   │   └── compare-complexity.py
│   │   └── templates/
│   │       ├── review-checklist.md
│   │       └── finding-template.md
│   ├── brand-voice/
│   │   ├── SKILL.md
│   │   ├── templates/
│   │   │   ├── email-template.txt
│   │   │   └── social-post-template.txt
│   │   └── tone-examples.md
│   ├── doc-generator/
│   │   ├── SKILL.md
│   │   └── generate-docs.py
│   ├── refactor/
│   │   ├── SKILL.md
│   │   ├── scripts/
│   │   │   ├── analyze-complexity.py
│   │   │   └── detect-smells.py
│   │   ├── references/
│   │   │   ├── code-smells.md
│   │   │   └── refactoring-catalog.md
│   │   └── templates/
│   │       └── refactoring-plan.md
│   ├── claude-md/
│   │   └── SKILL.md
│   ├── blog-draft/
│   │   ├── SKILL.md
│   │   └── templates/
│   │       ├── draft-template.md
│   │       └── outline-template.md
│   └── README.md
│
├── 04-subagents/                                # Subagents
│   ├── code-reviewer.md
│   ├── test-engineer.md
│   ├── documentation-writer.md
│   ├── secure-reviewer.md
│   ├── implementation-agent.md
│   ├── debugger.md
│   ├── data-scientist.md
│   ├── clean-code-reviewer.md
│   └── README.md
│
├── 05-mcp/                                      # MCP Protocol
│   ├── github-mcp.json
│   ├── database-mcp.json
│   ├── filesystem-mcp.json
│   ├── multi-mcp.json
│   └── README.md
│
├── 06-hooks/                                    # Hooks
│   ├── format-code.sh
│   ├── pre-commit.sh
│   ├── security-scan.sh
│   ├── log-bash.sh
│   ├── validate-prompt.sh
│   ├── notify-team.sh
│   ├── context-tracker.py
│   ├── context-tracker-tiktoken.py
│   └── README.md
│
├── 07-plugins/                                  # Plugins
│   ├── pr-review/
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── commands/
│   │   │   ├── review-pr.md
│   │   │   ├── check-security.md
│   │   │   └── check-tests.md
│   │   ├── agents/
│   │   │   ├── security-reviewer.md
│   │   │   ├── test-checker.md
│   │   │   └── performance-analyzer.md
│   │   ├── mcp/
│   │   │   └── github-config.json
│   │   ├── hooks/
│   │   │   └── pre-review.js
│   │   └── README.md
│   ├── devops-automation/
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── commands/
│   │   │   ├── deploy.md
│   │   │   ├── rollback.md
│   │   │   ├── status.md
│   │   │   └── incident.md
│   │   ├── agents/
│   │   │   ├── deployment-specialist.md
│   │   │   ├── incident-commander.md
│   │   │   └── alert-analyzer.md
│   │   ├── mcp/
│   │   │   └── kubernetes-config.json
│   │   ├── hooks/
│   │   │   ├── pre-deploy.js
│   │   │   └── post-deploy.js
│   │   ├── scripts/
│   │   │   ├── deploy.sh
│   │   │   ├── rollback.sh
│   │   │   └── health-check.sh
│   │   └── README.md
│   ├── documentation/
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── commands/
│   │   │   ├── generate-api-docs.md
│   │   │   ├── generate-readme.md
│   │   │   ├── sync-docs.md
│   │   │   └── validate-docs.md
│   │   ├── agents/
│   │   │   ├── api-documenter.md
│   │   │   ├── code-commentator.md
│   │   │   └── example-generator.md
│   │   ├── mcp/
│   │   │   └── github-docs-config.json
│   │   ├── templates/
│   │   │   ├── api-endpoint.md
│   │   │   ├── function-docs.md
│   │   │   └── adr-template.md
│   │   └── README.md
│   └── README.md
│
├── 08-checkpoints/                              # Checkpoints
│   ├── checkpoint-examples.md
│   └── README.md
│
├── 09-advanced-features/                        # 高级功能
│   ├── config-examples.json
│   ├── planning-mode-examples.md
│   └── README.md
│
└── 10-cli/                                      # CLI 使用
    └── README.md
```

---

## 按使用场景快速入门

### 代码质量和审查
```bash
# 安装斜杠命令
cp 01-slash-commands/optimize.md .claude/commands/

# 安装 subagent
cp 04-subagents/code-reviewer.md .claude/agents/

# 安装 skill
cp -r 03-skills/code-review ~/.claude/skills/

# 或安装完整 plugin
/plugin install pr-review
```

### DevOps 和部署
```bash
# 安装 plugin（包含一切）
/plugin install devops-automation
```

### 文档
```bash
# 安装斜杠命令
cp 01-slash-commands/generate-api-docs.md .claude/commands/

# 安装 subagent
cp 04-subagents/documentation-writer.md .claude/agents/

# 安装 skill
cp -r 03-skills/doc-generator ~/.claude/skills/

# 或安装完整 plugin
/plugin install documentation
```

### 团队标准
```bash
# 设置项目 memory
cp 02-memory/project-CLAUDE.md ./CLAUDE.md

# 编辑以匹配你团队的标准
```

### 外部集成
```bash
# 设置环境变量
export GITHUB_TOKEN="your_token"
export DATABASE_URL="postgresql://..."

# 安装 MCP 配置（项目范围）
cp 05-mcp/multi-mcp.json .mcp.json
```

### 自动化和验证
```bash
# 安装 hooks
mkdir -p ~/.claude/hooks
cp 06-hooks/*.sh ~/.claude/hooks/
chmod +x ~/.claude/hooks/*.sh

# 在设置中配置 hooks（~/.claude/settings.json）
# 参见 06-hooks/README.md
```

### 安全实验
```bash
# Checkpoints 在每个用户提示词时自动创建
# 要 rewind：按 Esc+Esc 或使用 /rewind
# 然后从 rewind 菜单中选择要恢复的内容

# 参见 08-checkpoints/README.md 获取示例
```

### 高级工作流
```bash
# 配置高级功能
# 参见 09-advanced-features/config-examples.json

# 使用 planning 模式
/plan Implement feature X

# 使用权限模式
claude --permission-mode plan          # 用于代码审查（只读）
claude --permission-mode acceptEdits   # 自动接受编辑
claude --permission-mode auto          # 自动批准安全操作

# 使用无头模式运行 CI/CD
claude -p "Run tests and report results"

# 运行后台任务
Run tests in background

# 参见 09-advanced-features/README.md 获取完整指南
```

---

## 功能覆盖矩阵

| 类别 | 命令 | Agents | MCP | Hooks | 脚本 | 模板 | 文档 | 图片 | 总计 |
|----------|----------|--------|-----|-------|---------|-----------|------|--------|-------|
| **01 斜杠命令** | 8 | - | - | - | - | - | 1 | 1 | **10** |
| **02 Memory** | - | - | - | - | - | 3 | 1 | 2 | **6** |
| **03 Skills** | - | - | - | - | 5 | 9 | 1 | - | **28** |
| **04 Subagents** | - | 8 | - | - | - | - | 1 | - | **9** |
| **05 MCP** | - | - | 4 | - | - | - | 1 | - | **5** |
| **06 Hooks** | - | - | - | 8 | - | - | 1 | - | **9** |
| **07 Plugins** | 11 | 9 | 3 | 3 | 3 | 3 | 4 | - | **40** |
| **08 Checkpoints** | - | - | - | - | - | - | 1 | 1 | **2** |
| **09 高级** | - | - | - | - | - | - | 1 | 2 | **3** |
| **10 CLI** | - | - | - | - | - | - | 1 | - | **1** |

---

## 学习路径

### 初学者（第 1 周）
1. 阅读 `README.md`
2. 安装 1-2 个斜杠命令
3. 创建项目 memory 文件
4. 尝试基本命令

### 中级（第 2-3 周）
1. 设置 GitHub MCP
2. 安装一个 subagent
3. 尝试委托任务
4. 安装一个 skill

### 高级（第 4 周+）
1. 安装完整 plugin
2. 创建自定义斜杠命令
3. 创建自定义 subagent
4. 创建自定义 skill
5. 构建你自己的 plugin

### 专家（第 5 周+）
1. 设置 hooks 实现自动化
2. 使用 checkpoints 进行实验
3. 配置 planning 模式
4. 有效使用权限模式
5. 为 CI/CD 设置无头模式
6. 精通会话管理

---

## 按关键词搜索

### 性能
- `01-slash-commands/optimize.md` - 性能分析
- `04-subagents/code-reviewer.md` - 性能审查
- `03-skills/code-review/` - 性能指标
- `07-plugins/pr-review/agents/performance-analyzer.md` - 性能专家

### 安全
- `04-subagents/secure-reviewer.md` - 安全审查
- `03-skills/code-review/` - 安全分析
- `07-plugins/pr-review/` - 安全检查

### 测试
- `04-subagents/test-engineer.md` - 测试工程师
- `07-plugins/pr-review/commands/check-tests.md` - 测试覆盖率

### 文档
- `01-slash-commands/generate-api-docs.md` - API 文档命令
- `04-subagents/documentation-writer.md` - 文档编写器 agent
- `03-skills/doc-generator/` - 文档生成器 skill
- `07-plugins/documentation/` - 完整文档 plugin

### 部署
- `07-plugins/devops-automation/` - 完整 DevOps 解决方案

### 自动化
- `06-hooks/` - 事件驱动自动化
- `06-hooks/pre-commit.sh` - 预提交自动化
- `06-hooks/format-code.sh` - 自动格式化
- `09-advanced-features/` - 用于 CI/CD 的无头模式

### 验证
- `06-hooks/security-scan.sh` - 安全验证
- `06-hooks/validate-prompt.sh` - 提示词验证

### 实验
- `08-checkpoints/` - 带 rewind 的安全实验
- `08-checkpoints/checkpoint-examples.md` - 真实示例

### Planning
- `09-advanced-features/planning-mode-examples.md` - Planning 模式示例
- `09-advanced-features/README.md` - 扩展思考

### 配置
- `09-advanced-features/config-examples.json` - 配置示例

---

## 注意事项

- 所有示例可直接使用
- 修改以适应你的特定需求
- 示例遵循 Claude Code 最佳实践
- 每个类别都有自己的 README，包含详细说明
- 脚本包含适当的错误处理
- 模板可自定义

---

## 贡献

想添加更多示例？请按以下结构：
1. 创建适当的子目录
2. 包含带使用说明的 README.md
3. 遵循命名约定
4. 彻底测试
5. 更新本索引

---

**最后更新**：2026 年 3 月
**总示例数**：100+ 个文件
**类别**：10 个功能
**Hooks**：8 个自动化脚本
**配置示例**：10+ 个场景
**可直接使用**：所有示例
