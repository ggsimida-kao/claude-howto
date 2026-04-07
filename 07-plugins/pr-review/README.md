<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../../resources/logos/claude-howto-logo-dark.svg">
  <img alt="Claude How To" src="../../resources/logos/claude-howto-logo.svg">
</picture>

# PR Review Plugin（PR 审核插件）

带有安全、测试和文档检查的完整 PR 审核工作流。

## Features（功能特性）

✅ Security analysis（安全分析）
✅ Test coverage checking（测试覆盖率检查）
✅ Documentation verification（文档验证）
✅ Code quality assessment（代码质量评估）
✅ Performance impact analysis（性能影响分析）

## Installation（安装）

```bash
/plugin install pr-review
```

## What's Included（包含内容）

### Slash Commands（斜杠命令）
- `/review-pr` - Comprehensive PR review（全面的 PR 审核）
- `/check-security` - Security-focused review（专注于安全的审核）
- `/check-tests` - Test coverage analysis（测试覆盖率分析）

### Subagents（子代理）
- `security-reviewer` - Security vulnerability detection（安全漏洞检测）
- `test-checker` - Test coverage analysis（测试覆盖率分析）
- `performance-analyzer` - Performance impact evaluation（性能影响评估）

### MCP Servers（MCP 服务器）
- GitHub integration for PR data（用于 PR 数据的 GitHub 集成）

### Hooks（钩子）
- `pre-review.js` - Pre-review validation（审核前验证）

## Usage（使用方法）

### Basic PR Review（基本 PR 审核）
```
/review-pr
```

### Security Check Only（仅安全检查）
```
/check-security
```

### Test Coverage Check（测试覆盖率检查）
```
/check-tests
```

## Requirements（要求）

- Claude Code 1.0+
- GitHub access（GitHub 访问）
- Git repository（Git 仓库）

## Configuration（配置）

Set up your GitHub token:
设置您的 GitHub 令牌：
```bash
export GITHUB_TOKEN="your_github_token"
```

## Example Workflow（工作流示例）

```
User: /review-pr

Claude:
1. Runs pre-review hook (validates git repo)
   运行审核前钩子（验证 git 仓库）
2. Fetches PR data via GitHub MCP
   通过 GitHub MCP 获取 PR 数据
3. Delegates security review to security-reviewer subagent
   将安全审核委托给 security-reviewer 子代理
4. Delegates testing to test-checker subagent
   将测试委托给 test-checker 子代理
5. Delegates performance to performance-analyzer subagent
   将性能委托给 performance-analyzer 子代理
6. Synthesizes all findings
   综合所有发现
7. Provides comprehensive review report
   提供全面的审核报告

Result:
✅ Security: No critical issues found
⚠️  Testing: Coverage is 65%, recommend 80%+
✅ Performance: No significant impact
📝 Recommendations: Add tests for edge cases
```
