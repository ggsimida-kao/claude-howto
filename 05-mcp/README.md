<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../resources/logos/claude-howto-logo-dark.svg">
  <img alt="Claude How To" src="../resources/logos/claude-howto-logo.svg">
</picture>

# MCP (Model Context Protocol)

本文件夹包含 Claude Code 与 MCP 服务器配置和使用的综合文档和示例。

## 概述

MCP（Model Context Protocol）是一种标准化方式，允许 Claude 访问外部工具、API 和实时数据源。与 Memory 不同，MCP 提供对变化数据的实时访问。

关键特性：
- 实时访问外部服务
- 实时数据同步
- 可扩展架构
- 安全认证
- 基于工具的交互

## MCP 架构

MCP 通过标准化协议连接 Claude 与外部服务：

```
Claude -->|Request| MCP Server -->|Query| External Service
         <--|Response| <--|Data| <--
```

## MCP 安装方法

Claude Code 支持多种传输协议：

### HTTP 传输（推荐）

```bash
# Basic HTTP connection
claude mcp add --transport http notion https://mcp.notion.com/mcp

# HTTP with authentication header
claude mcp add --transport http secure-api https://api.example.com/mcp \
  --header "Authorization: Bearer your-token"
```

### Stdio 传输（本地）

```bash
# Local Node.js server
claude mcp add --transport stdio myserver -- npx @myorg/mcp-server

# With environment variables
claude mcp add --transport stdio myserver --env KEY=value -- npx server
```

### OAuth 2.0 认证

```bash
# Connect to an OAuth-enabled MCP server
claude mcp add --transport http my-service https://my-service.example.com/mcp

# Pre-configure OAuth credentials
claude mcp add --transport http my-service https://my-service.example.com/mcp \
  --client-id "your-client-id" \
  --client-secret "your-client-secret"
```

## MCP 工具搜索

当 MCP 工具描述超过上下文窗口的 10% 时，Claude Code 自动启用工具搜索以高效选择正确的工具。

## MCP 配置管理

```bash
# Add HTTP-based server
claude mcp add --transport http github https://api.github.com/mcp

# List all MCP servers
claude mcp list

# Remove an MCP server
claude mcp remove github
```

## MCP 配置位置

| 作用域 | 位置 | 描述 |
|----------|----------|---------|
| **Local** | `~/.claude.json` | 仅当前用户、当前项目 |
| **Project** | `.mcp.json` | Git 仓库，可与团队共享 |
| **User** | `~/.claude.json` | 所有项目可用 |

### 项目作用域配置

```json
{
  "mcpServers": {
    "github": {
      "type": "http",
      "url": "https://api.github.com/mcp"
    }
  }
}
```

## MCP 与 Memory：决策矩阵

| 需求 | 选择 |
|------|------|
| 需要外部数据？否 | 使用 Memory |
| 外部数据？经常变化 | 使用 MCP |
| 外部数据？很少变化 | 使用 Memory |

## Claude 作为 MCP 服务器

Claude Code 本身可以作为其他应用程序的 MCP 服务器：

```bash
# Start Claude Code as an MCP server
claude mcp serve
```

## 安全最佳实践

### 做

- 使用环境变量存储所有凭证
- 定期轮换令牌和 API 密钥
- 尽可能使用只读令牌
- 将 MCP 服务器访问范围限制为最小必需
- 监控 MCP 服务器使用和访问日志
- 使用 OAuth 进行外部服务（可用时）
- 测试 MCP 连接后再投入生产

### 不做

- 不要在配置文件中硬编码凭证
- 不要将令牌或密钥提交到 git
- 不要授予不必要的权限
- 不要忽略认证错误

## 环境变量

```bash
# ~/.bashrc or ~/.zshrc
export GITHUB_TOKEN="ghp_xxxxxxxxxxxxx"
export DATABASE_URL="postgresql://user:pass@localhost/mydb"
```

然后在 MCP 配置中引用：

```json
{
  "env": {
    "GITHUB_TOKEN": "${GITHUB_TOKEN}"
  }
}
```

## 故障排除

### MCP 服务器未找到
```bash
# Verify MCP server is installed
npm list -g @modelcontextprotocol/server-github
```

### 认证失败
```bash
# Verify environment variable is set
echo $GITHUB_TOKEN
```

### 连接超时
- 检查网络连接
- 验证 API 端点可访问
- 检查 API 速率限制

## 相关概念

### Memory vs MCP
- **Memory**：存储持久、不变的数据（偏好、上下文、历史）
- **MCP**：访问实时、变化的数据（API、数据库、实时服务）

### 何时使用
- **使用 Memory**：用户偏好、对话历史、学习到的上下文
- **使用 MCP**：当前 GitHub 问题、实时数据库查询、实时数据

## 其他资源

- [官方 MCP 文档](https://code.claude.com/docs/en/mcp)
- [MCP 协议规范](https://modelcontextprotocol.io/specification)
- [MCP GitHub 仓库](https://github.com/modelcontextprotocol/servers)
- [Claude Code CLI 参考](https://code.claude.com/docs/en/cli-reference)
