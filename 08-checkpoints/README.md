<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../resources/logos/claude-howto-logo-dark.svg">
  <img alt="Claude How To" src="../resources/logos/claude-howto-logo.svg">
</picture>

# Checkpoints and Rewind（检查点和回溯）

检查点允许您保存会话状态并回溯到 Claude Code 会话中的先前点。这对于探索不同方法、从错误中恢复或比较替代解决方案非常宝贵。

## 概述

检查点允许您保存会话状态并回溯到先前点，实现安全实验和多种方法的探索。它们是会话状态的快照，包括：
- 所有交换的消息
- 进行的文件修改
- 工具使用历史
- 会话上下文

检查点在探索不同方法、从错误中恢复或比较替代解决方案时非常宝贵。

## 关键概念

| 概念 | 描述 |
|---------|-------------|
| **Checkpoint（检查点）** | 包括消息、文件和上下文的会话状态快照 |
| **Rewind（回溯）** | 返回先前的检查点，丢弃后续更改 |
| **Branch Point（分支点）** | 从该点探索多种方法的检查点 |

## 访问检查点

您可以通过两种主要方式访问和管理检查点：

### 使用键盘快捷键
按两次 `Esc`（`Esc` + `Esc`）打开检查点界面并浏览保存的检查点。

### 使用斜杠命令
使用 `/rewind` 命令（别名：`/checkpoint`）快速访问：

```bash
# Open rewind interface
/rewind

# Or use the alias
/checkpoint
```

## 回溯选项

当您回溯时，会显示五个选项菜单：

1. **Restore code and conversation（恢复代码和对话）** -- 将文件和消息恢复到该检查点
2. **Restore conversation（恢复对话）** -- 仅回溯消息，保持当前代码不变
3. **Restore code（恢复代码）** -- 仅恢复文件更改，保持完整对话历史
4. **Summarize from here（从这里总结）** -- 将此点之后的对话压缩成 AI 生成的摘要。原始消息保留在记录中。您可以选择提供指令以将摘要集中在特定主题上。
5. **Never mind（算了）** -- 取消并返回当前状态

## 自动检查点

Claude Code 会自动为您创建检查点：

- **每个用户提示词** - 每次用户输入时创建新检查点
- **持久化** - 检查点跨会话持久化
- **自动清理** - 检查点在 30 天后自动清理

这意味着您始终可以回溯到对话中任何先前的点，从几分钟前到几天前。

## 使用场景

| 场景 | 工作流 |
|----------|----------|
| **Exploring Approaches（探索方法）** | Save → Try A → Save → Rewind → Try B → Compare |
| **Safe Refactoring（安全重构）** | Save → Refactor → Test → If fail: Rewind |
| **A/B Testing（A/B 测试）** | Save → Design A → Save → Rewind → Design B → Compare |
| **Mistake Recovery（错误恢复）** | Notice issue → Rewind to last good state |

## 使用检查点

### 查看和回溯

按 `Esc` 两次或使用 `/rewind` 打开检查点浏览器。您将看到所有可用检查点的列表以及时间戳。选择任何检查点以回溯到该状态。

### 检查点详情

每个检查点显示：
- 创建时的时间戳
- 修改的文件
- 对话中的消息数量
- 使用的工具

## 实用示例

### 示例 1：探索不同方法

```
User: Let's add a caching layer to the API

Claude: I'll add Redis caching to your API endpoints...
[Makes changes at checkpoint A]

User: Actually, let's try in-memory caching instead

Claude: I'll rewind to explore a different approach...
[User presses Esc+Esc and rewinds to checkpoint A]
[Implements in-memory caching at checkpoint B]

User: Now I can compare both approaches
```

### 示例 2：从错误中恢复

```
User: Refactor the authentication module to use JWT

Claude: I'll refactor the authentication module...
[Makes extensive changes]

User: Wait, that broke the OAuth integration. Let's go back.

Claude: I'll help you rewind to before the refactoring...
[User presses Esc+Esc and selects the checkpoint before the refactor]

User: Let's try a more conservative approach this time
```

### 示例 3：安全实验

```
User: Let's try rewriting this in a functional style
[Creates checkpoint before experiment]

Claude: [Makes experimental changes]

User: The tests are failing. Let's rewind.
[User presses Esc+Esc and rewinds to the checkpoint]

Claude: I've rewound the changes. Let's try a different approach.
```

### 示例 4：分支方法

```
User: I want to compare two database designs
[Takes note of checkpoint - call it "Start"]

Claude: I'll create the first design...
[Implements Schema A]

User: Now let me go back and try the second approach
[User presses Esc+Esc and rewinds to "Start"]

Claude: Now I'll implement Schema B...
[Implements Schema B]

User: Great! Now I have both schemas to choose from
```

## 检查点保留

Claude Code 自动管理您的检查点：

- 每次用户提示词时自动创建检查点
- 旧检查点保留最多 30 天
- 自动清理检查点以防止无限存储增长

## 工作流模式

### 探索分支策略

当探索多种方法时：

```
1. Start with initial implementation → Checkpoint A
2. Try Approach 1 → Checkpoint B
3. Rewind to Checkpoint A
4. Try Approach 2 → Checkpoint C
5. Compare results from B and C
6. Choose best approach and continue
```

### 安全重构模式

在进行重大更改时：

```
1. Current state → Checkpoint (auto)
2. Start refactoring
3. Run tests
4. If tests pass → Continue working
5. If tests fail → Rewind and try different approach
```

## 最佳实践

由于检查点是自动创建的，您可以专注于工作，而不必担心手动保存状态。但请记住以下做法：

### 有效使用检查点

✅ **宜：**
- 回溯前查看可用检查点
- 当想探索不同方向时使用回溯
- 保留检查点以比较不同方法
- 了解每个回溯选项的作用（恢复代码和对话、恢复对话、恢复代码或总结）

❌ **忌：**
- 仅依赖检查点进行代码保存
- 期望检查点跟踪外部文件系统更改
- 使用检查点代替 git 提交

## 配置

您可以在设置中切换自动检查点：

```json
{
  "autoCheckpoint": true
}
```

- `autoCheckpoint`：启用或禁用每次用户提示词时自动创建检查点（默认：`true`）

## 限制

检查点有以下限制：

- **Bash 命令更改不跟踪** - 文件系统上的操作如 `rm`、`mv`、`cp` 不会在检查点中捕获
- **外部更改不跟踪** - 在 Claude Code 外部进行的更改（在您的编辑器、终端等中）不会捕获
- **不是版本控制的替代品** - 使用 git 进行代码库的永久、可审计更改

## 故障排除

### 缺少检查点

**问题**：找不到预期的检查点

**解决方案**：
- 检查检查点是否被清除
- 验证设置中 `autoCheckpoint` 是否启用
- 检查磁盘空间

### 回溯失败

**问题**：无法回溯到检查点

**解决方案**：
- 确保没有冲突的未提交更改
- 检查检查点是否损坏
- 尝试回溯到不同的检查点

## 与 Git 集成

检查点补充（但不替换）git：

| 功能 | Git | 检查点 |
|---------|-----|-------------|
| Scope（范围） | File system（文件系统） | Conversation + files（对话 + 文件） |
| Persistence（持久性） | Permanent（永久） | Session-based（基于会话） |
| Granularity（粒度） | Commits（提交） | Any point（任意点） |
| Speed（速度） | Slower（较慢） | Instant（即时） |
| Sharing（共享） | Yes（是） | Limited（有限） |

一起使用：
1. 使用检查点进行快速实验
2. 使用 git 提交进行最终确定的更改
3. 在 git 操作前创建检查点
4. 将成功的检查点状态提交到 git

## 快速入门指南

### 基本工作流

1. **正常工作** - Claude Code 自动创建检查点
2. **想回去？** - 按 `Esc` 两次或使用 `/rewind`
3. **选择检查点** - 从列表中选择要回溯的检查点
4. **选择要恢复的内容** - 选择恢复代码和对话、恢复对话、恢复代码、从这里总结或取消
5. **继续工作** - 您已回到该点

### 键盘快捷键

- **`Esc` + `Esc`** - 打开检查点浏览器
- **`/rewind`** - 访问检查点的替代方式
- **`/checkpoint`** - `/rewind` 的别名

## 了解何时回溯：上下文监控

检查点让您可以回去——但您怎么知道什么时候应该回去？随着对话增长，Claude 的上下文窗口会填满，模型质量会悄然下降。您可能在不知不觉中从半盲模型发送代码。

**[cc-context-stats](https://github.com/luongnv89/cc-context-stats)** 通过向 Claude Code 状态栏添加实时**上下文区域**来解决这个问题。它跟踪您在上下文窗口中的位置——从**Plan**（绿色，安全进行规划和编码）到**Code**（黄色，避免开始新计划）再到**Dump**（橙色，完成并回溯）。当您看到区域转换时，就知道是时候创建检查点并重新开始了，而不是用降级的输出继续。

## 相关概念

- **[Advanced Features](../09-advanced-features/)** - Planning mode and other advanced capabilities
- **[Memory Management](../02-memory/)** - Managing conversation history and context
- **[Slash Commands](../01-slash-commands/)** - User-invoked shortcuts
- **[Hooks](../06-hooks/)** - Event-driven automation
- **[Plugins](../07-plugins/)** - Bundled extension packages

## 其他资源

- [Official Checkpointing Documentation](https://code.claude.com/docs/en/checkpointing)
- [Advanced Features Guide](../09-advanced-features/) - Extended thinking and other capabilities

## 摘要

检查点是 Claude Code 中的一项自动功能，让您可以安全地探索不同方法而不丢失工作。每次用户提示词都会自动创建新检查点，因此您可以回溯到会话中任何先前的点。

主要好处：
- 无顾虑地尝试多种方法进行实验
- 快速从错误中恢复
- 并排比较不同的解决方案
- 与版本控制系统安全集成

记住：检查点不是 git 的替代品。使用检查点进行快速实验，使用 git 进行永久代码更改。
