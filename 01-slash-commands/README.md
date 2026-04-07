<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../resources/logos/claude-howto-logo-dark.svg">
  <img alt="Claude How To" src="../resources/logos/claude-howto-logo.svg">
</picture>

# 斜杠命令（Slash Commands）

## 概述

斜杠命令是在交互式会话中控制 Claude 行为的快捷方式，分为多种类型：

- **内置命令（Built-in commands）**：由 Claude Code 提供（`/help`、`/clear`、`/model`）
- **技能（Skills）**：用户自定义命令，以 `SKILL.md` 文件形式创建（`/optimize`、`/pr`）
- **插件命令（Plugin commands）**：来自已安装插件的命令（`/frontend-design:frontend-design`）
- **MCP 提示词（MCP prompts）**：来自 MCP 服务器的命令（`/mcp__github__list_prs`）

> **注意**：自定义斜杠命令已合并到技能中。`.claude/commands/` 中的文件仍然可用，但技能（`.claude/skills/`）现在是推荐方式。两者都会创建 `/命令名` 快捷方式。完整的参考说明请参阅[技能指南](../03-skills/)。

## 内置命令参考

内置命令是常用操作的快捷方式。Claude Code 提供 **55+ 个内置命令**和 **5 个捆绑技能**。在 Claude Code 中输入 `/` 可查看完整列表，或输入 `/` 后跟任意字母进行筛选。

| 命令 | 用途 |
|---------|---------|
| `/add-dir <路径>` | 添加工作目录 |
| `/agents` | 管理智能体配置 |
| `/branch [名称]` | 将对话分支到新会话（别名：`/fork`）。注：`/fork` 在 v2.1.77 中更名为 `/branch` |
| `/btw <问题>` | 附带提问，不添加到历史记录 |
| `/chrome` | 配置 Chrome 浏览器集成 |
| `/clear` | 清除对话（别名：`/reset`、`/new`） |
| `/color [颜色\|default]` | 设置提示栏颜色 |
| `/compact [指令]` | 压缩对话，可附带聚焦指令 |
| `/config` | 打开设置（别名：`/settings`） |
| `/context` | 将上下文使用情况可视化为彩色网格 |
| `/copy [N]` | 将助手回复复制到剪贴板；`w` 写入文件 |
| `/cost` | 显示令牌使用统计 |
| `/desktop` | 在桌面应用继续（别名：`/app`） |
| `/diff` | 交互式差异查看器，查看未提交的更改 |
| `/doctor` | 诊断安装健康状况 |
| `/effort [low\|medium\|high\|max\|auto]` | 设置努力程度。`max` 需要 Opus 4.6 |
| `/exit` | 退出 REPL（别名：`/quit`） |
| `/export [文件名]` | 将当前对话导出为文件或剪贴板 |
| `/extra-usage` | 为速率限制配置额外用量 |
| `/fast [on\|off]` | 切换快速模式 |
| `/feedback` | 提交反馈（别名：`/bug`） |
| `/help` | 显示帮助 |
| `/hooks` | 查看钩子配置 |
| `/ide` | 管理 IDE 集成 |
| `/init` | 初始化 `CLAUDE.md`。设置 `CLAUDE_CODE_NEW_INIT=true` 可启用交互式流程 |
| `/insights` | 生成会话分析报告 |
| `/install-github-app` | 设置 GitHub Actions 应用 |
| `/install-slack-app` | 安装 Slack 应用 |
| `/keybindings` | 打开键绑定配置 |
| `/login` | 切换 Anthropic 账户 |
| `/logout` | 登出 Anthropic 账户 |
| `/mcp` | 管理 MCP 服务器和 OAuth |
| `/memory` | 编辑 `CLAUDE.md`，切换自动记忆 |
| `/mobile` | 移动应用的二维码（别名：`/ios`、`/android`） |
| `/model [模型]` | 选择模型，左右箭头选择努力程度 |
| `/passes` | 分享免费周 Claude Code |
| `/permissions` | 查看/更新权限（别名：`/allowed-tools`） |
| `/plan [描述]` | 进入计划模式 |
| `/plugin` | 管理插件 |
| `/pr-comments [PR]` | 获取 GitHub PR 评论 |
| `/privacy-settings` | 隐私设置（仅 Pro/Max） |
| `/release-notes` | 查看更新日志 |
| `/reload-plugins` | 重新加载活动插件 |
| `/remote-control` | 从 claude.ai 远程控制（别名：`/rc`） |
| `/remote-env` | 配置默认远程环境 |
| `/rename [名称]` | 重命名会话 |
| `/resume [会话]` | 恢复对话（别名：`/continue`） |
| `/review` | **已弃用** — 请安装 `code-review` 插件替代 |
| `/rewind` | 回退对话和/或代码（别名：`/checkpoint`） |
| `/sandbox` | 切换沙盒模式 |
| `/schedule [描述]` | 创建/管理计划任务 |
| `/security-review` | 分析分支的安全漏洞 |
| `/skills` | 列出可用技能 |
| `/stats` | 可视化每日用量、会话、连续记录 |
| `/status` | 显示版本、模型、账户信息 |
| `/statusline` | 配置状态栏 |
| `/tasks` | 列出/管理后台任务 |
| `/terminal-setup` | 配置终端键绑定 |
| `/theme` | 更改颜色主题 |
| `/vim` | 切换 Vim/普通模式 |
| `/voice` | 切换按键说话语音输入 |

### 捆绑技能

这些技能随 Claude Code 一起提供，以斜杠命令方式调用：

| 技能 | 用途 |
|-------|---------|
| `/batch <指令>` | 使用工作树编排大规模并行更改 |
| `/claude-api` | 为项目语言加载 Claude API 参考 |
| `/debug [描述]` | 启用调试日志 |
| `/loop [间隔] <提示词>` | 按间隔重复运行提示词 |
| `/simplify [聚焦]` | 审查已更改文件的代码质量 |

### 已弃用的命令

| 命令 | 状态 |
|---------|--------|
| `/review` | 已弃用 — 由 `code-review` 插件替代 |
| `/output-style` | 自 v2.1.73 起已弃用 |
| `/fork` | 已更名为 `/branch`（别名仍可用，v2.1.77） |

### 最近更新

- `/fork` 更名为 `/branch`，保留 `/fork` 作为别名（v2.1.77）
- `/output-style` 已弃用（v2.1.73）
- `/review` 已弃用，改用 `code-review` 插件
- 新增 `/effort` 命令，`max` 级别需要 Opus 4.6
- 新增 `/voice` 命令，用于按键说话语音输入
- 新增 `/schedule` 命令，用于创建/管理计划任务
- 新增 `/color` 命令，用于提示栏自定义
- `/model` 选择器现在显示人类可读的标签（如"Sonnet 4.6"）而非原始模型 ID
- `/resume` 支持 `/continue` 别名
- MCP 提示词可以作为 `/mcp__<服务器>__<提示词>` 命令使用（参见 [MCP 提示词作为命令](#mcp-提示词作为命令)）

## 自定义命令（现为技能）

自定义斜杠命令已**合并到技能中**。两种方式都会创建可通过 `/命令名` 调用的命令：

| 方式 | 位置 | 状态 |
|----------|----------|--------|
| **技能（推荐）** | `.claude/skills/<名称>/SKILL.md` | 当前标准 |
| **旧版命令** | `.claude/commands/<名称>.md` | 仍然可用 |

如果技能和命令同名，**技能优先**。例如，当 `.claude/commands/review.md` 和 `.claude/skills/review/SKILL.md` 同时存在时，使用技能版本。

### 迁移路径

现有的 `.claude/commands/` 文件无需更改即可继续工作。迁移到技能的方法：

**之前（命令）：**
```
.claude/commands/optimize.md
```

**之后（技能）：**
```
.claude/skills/optimize/SKILL.md
```

### 为什么使用技能？

技能相比旧版命令提供额外功能：

- **目录结构**：打包脚本、模板和参考文件
- **自动调用**：Claude 可以在相关时自动触发技能
- **调用控制**：选择用户、Claude 或两者都可以调用
- **子智能体执行**：使用 `context: fork` 在隔离的上下文中运行技能
- **渐进式披露**：仅在需要时加载额外文件

### 将自定义命令创建为技能

创建带有 `SKILL.md` 文件的目录：

```bash
mkdir -p .claude/skills/my-command
```

**文件：** `.claude/skills/my-command/SKILL.md`

```yaml
---
name: my-command
description: 此命令的作用及使用场景
---

# My Command

调用此命令时 Claude 遵循的指令。

1. 第一步
2. 第二步
3. 第三步
```

### Frontmatter 参考

| 字段 | 用途 | 默认值 |
|-------|---------|---------|
| `name` | 命令名称（成为 `/名称`） | 目录名称 |
| `description` | 简短描述（帮助 Claude 了解何时使用） | 第一段 |
| `argument-hint` | 自动补全的预期参数 | 无 |
| `allowed-tools` | 命令可使用但无需授权的工具 | 继承 |
| `model` | 使用的特定模型 | 继承 |
| `disable-model-invocation` | 若为 `true`，仅用户可调用（Claude 不可自动调用） | `false` |
| `user-invocable` | 若为 `false`，在 `/` 菜单中隐藏 | `true` |
| `context` | 设置为 `fork` 以在隔离的子智能体中运行 | 无 |
| `agent` | 使用 `context: fork` 时的智能体类型 | `general-purpose` |
| `hooks` | 技能范围的钩子（PreToolUse、PostToolUse、Stop） | 无 |

### 参数

命令可以接收参数：

**所有参数使用 `$ARGUMENTS`：**

```yaml
---
name: fix-issue
description: 按编号修复 GitHub issue
---

按编号修复 issue #$ARGUMENTS，遵循我们的编码标准
```

用法：`/fix-issue 123` → `$ARGUMENTS` 变为 "123"

**单个参数使用 `$0`、`$1` 等：**

```yaml
---
name: review-pr
description: 审查 PR，附带优先级
---

审查 PR #$0，优先级 $1
```

用法：`/review-pr 456 high` → `$0`="456", `$1`="high"

### 使用 Shell 命令的动态上下文

使用 `!`command`` 在提示词之前执行 bash 命令：

```yaml
---
name: commit
description: 创建带上下文的 git 提交
allowed-tools: Bash(git *)
---

## Context

- 当前 git 状态：!`git status`
- 当前 git diff：!`git diff HEAD`
- 当前分支：!`git branch --show-current`
- 最近的提交：!`git log --oneline -5`

## 你的任务

根据以上更改，创建一个 git 提交。
```

### 文件引用

使用 `@` 包含文件内容：

```markdown
审查 @src/utils/helpers.js 中的实现
比较 @src/old-version.js 和 @src/new-version.js
```

## 插件命令

插件可以提供自定义命令：

```
/plugin-name:command-name
```

或者当没有命名冲突时直接使用 `/command-name`。

**示例：**
```bash
/frontend-design:frontend-design
/commit-commands:commit
```

## MCP 提示词作为命令

MCP 服务器可以将提示词作为斜杠命令暴露：

```
/mcp__<服务器名>__<提示词名> [参数]
```

**示例：**
```bash
/mcp__github__list_prs
/mcp__github__pr_review 456
/mcp__jira__create_issue "Bug 标题" high
```

### MCP 权限语法

在权限中控制 MCP 服务器访问：

- `mcp__github` — 访问整个 GitHub MCP 服务器
- `mcp__github__*` — 通配符访问所有工具
- `mcp__github__get_issue` — 特定工具访问

## 命令架构

```mermaid
graph TD
    A["用户输入: /command-name"] --> B{"命令类型?"}
    B -->|内置| C["执行内置命令"]
    B -->|技能| D["加载 SKILL.md"]
    B -->|插件| E["加载插件命令"]
    B -->|MCP| F["执行 MCP 提示词"]

    D --> G["解析 Frontmatter"]
    G --> H["替换变量"]
    H --> I["执行 Shell 命令"]
    I --> J["发送给 Claude"]
    J --> K["返回结果"]
```

## 命令生命周期

```mermaid
sequenceDiagram
    participant User
    participant Claude as Claude Code
    participant FS as File System
    participant CLI as Shell/Bash

    User->>Claude: 输入 /optimize
    Claude->>FS: 搜索 .claude/skills/ 和 .claude/commands/
    FS-->>Claude: 返回 optimize/SKILL.md
    Claude->>Claude: 解析 frontmatter
    Claude->>CLI: 执行 !`command` 替换
    CLI-->>Claude: 命令输出
    Claude->>Claude: 替换 $ARGUMENTS
    Claude->>User: 处理提示词
    Claude->>User: 返回结果
```

## 本文件夹中的可用命令

这些示例命令可以安装为技能或旧版命令。

### 1. `/optimize` - 代码优化

分析代码的性能问题、内存泄漏和优化机会。

**用法：**
```
/optimize
[粘贴你的代码]
```

### 2. `/pr` - Pull Request 准备

引导完成 PR 准备清单，包括 linting、测试和提交格式。

**用法：**
```
/pr
```

**截图：**
![/pr](pr-slash-command.png)

### 3. `/generate-api-docs` - API 文档生成器

从源代码生成全面的 API 文档。

**用法：**
```
/generate-api-docs
```

### 4. `/commit` - 带上下文的 Git 提交

根据仓库的动态上下文创建 git 提交。

**用法：**
```
/commit [可选消息]
```

### 5. `/push-all` - 暂存、提交并推送

暂存所有更改，创建提交，并推送至远程，带安全检查。

**用法：**
```
/push-all
```

**安全检查：**
- 密钥：`.env*`、`*.key`、`*.pem`、`credentials.json`
- API 密钥：检测真实密钥与占位符
- 大文件：`>10MB` 且无 Git LFS
- 构建产物：`node_modules/`、`dist/`、`__pycache__/`

### 6. `/doc-refactor` - 文档重构

重构项目文档，提高清晰度和可访问性。

**用法：**
```
/doc-refactor
```

### 7. `/setup-ci-cd` - CI/CD 流水线设置

实现预提交钩子和 GitHub Actions 质量保证。

**用法：**
```
/setup-ci-cd
```

### 8. `/unit-test-expand` - 测试覆盖率扩展

通过针对未测试的分支和边缘情况来增加测试覆盖率。

**用法：**
```
/unit-test-expand
```

## 安装

### 作为技能（推荐）

复制到技能目录：

```bash
# 创建技能目录
mkdir -p .claude/skills

# 对于每个命令文件，创建技能目录
for cmd in optimize pr commit; do
  mkdir -p .claude/skills/$cmd
  cp 01-slash-commands/$cmd.md .claude/skills/$cmd/SKILL.md
done
```

### 作为旧版命令

复制到命令目录：

```bash
# 项目范围（团队）
mkdir -p .claude/commands
cp 01-slash-commands/*.md .claude/commands/

# 个人使用
mkdir -p ~/.claude/commands
cp 01-slash-commands/*.md ~/.claude/commands/
```

## 创建你自己的命令

### 技能模板（推荐）

创建 `.claude/skills/my-command/SKILL.md`：

```yaml
---
name: my-command
description: 此命令的作用。使用场景：[触发条件]。
argument-hint: [可选参数]
allowed-tools: Bash(npm *), Read, Grep
---

# 命令标题

## 上下文

- 当前分支：!`git branch --show-current`
- 相关文件：@package.json

## 指令

1. 第一步
2. 第二步（带参数：$ARGUMENTS）
3. 第三步

## 输出格式

- 如何格式化响应
- 需要包含什么
```

### 仅用户可调用的命令（无自动调用）

对于有副作用的命令，Claude 不应自动触发：

```yaml
---
name: deploy
description: 部署到生产环境
disable-model-invocation: true
allowed-tools: Bash(npm *), Bash(git *)
---

将应用程序部署到生产环境：

1. 运行测试
2. 构建应用程序
3. 推送到部署目标
4. 验证部署
```

## 最佳实践

| 宜 | 忌 |
|------|---------|
| 使用清晰、面向动作的名称 | 为一次性任务创建命令 |
| 包含 `description` 说明触发条件 | 在命令中构建复杂逻辑 |
| 保持命令专注于单一任务 | 硬编码敏感信息 |
| 对副作用使用 `disable-model-invocation` | 跳过 description 字段 |
| 使用 `!` 前缀获取动态上下文 | 假设 Claude 知道当前状态 |
| 在技能目录中组织相关文件 | 将所有内容放在一个文件中 |

## 故障排除

### 命令未找到

**解决方案：**
- 检查文件是否在 `.claude/skills/<名称>/SKILL.md` 或 `.claude/commands/<名称>.md`
- 验证 frontmatter 中的 `name` 字段与预期命令名称匹配
- 重启 Claude Code 会话
- 运行 `/help` 查看可用命令

### 命令执行不符合预期

**解决方案：**
- 添加更具体的指令
- 在技能文件中包含示例
- 如果使用 bash 命令，检查 `allowed-tools`
- 先用简单输入测试

### 技能与命令冲突

如果两者同名，**技能优先**。删除其中一个或重命名。

## 相关指南

- **[技能（Skills）](../03-skills/)** — 技能完整参考（自动调用的能力）
- **[记忆（Memory）](../02-memory/)** — 通过 CLAUDE.md 持久化上下文
- **[子智能体（Subagents）](../04-subagents/)** — 委托 AI 智能体
- **[插件（Plugins）](../07-plugins/)** — 捆绑的命令集合
- **[钩子（Hooks）](../06-hooks/)** — 事件驱动自动化

## 其他资源

- [官方交互模式文档](https://code.claude.com/docs/en/interactive-mode) — 内置命令参考
- [官方技能文档](https://code.claude.com/docs/en/skills) — 完整技能参考
- [CLI 参考](https://code.claude.com/docs/en/cli-reference) — 命令行选项

---

*属于 [Claude How To](../) 指南系列*
