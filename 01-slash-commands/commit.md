---
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*), Bash(git diff:*)
argument-hint: [消息]
description: 创建带上下文的 git 提交
---

## 上下文

- 当前 git 状态：!`git status`
- 当前 git diff：!`git diff HEAD`
- 当前分支：!`git branch --show-current`
- 最近的提交：!`git log --oneline -10`

## 你的任务

根据以上更改，创建一个 git 提交。

如果通过参数提供了消息，则使用：$ARGUMENTS

否则，分析更改并按照 conventional commits 格式创建适当的提交消息：
- `feat:` 用于新功能
- `fix:` 用于错误修复
- `docs:` 用于文档更改
- `refactor:` 用于代码重构
- `test:` 用于添加测试
- `chore:` 用于维护任务
