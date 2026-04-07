<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../../resources/logos/claude-howto-logo-dark.svg">
  <img alt="Claude How To" src="../../resources/logos/claude-howto-logo.svg">
</picture>

# Documentation Plugin（文档插件）

为您的项目提供全面的文档生成和维护。

## Features（功能特性）

✅ API documentation generation（API 文档生成）
✅ README creation and updates（README 创建和更新）
✅ Documentation synchronization（文档同步）
✅ Code comment improvements（代码注释改进）
✅ Example generation（示例生成）

## Installation（安装）

```bash
/plugin install documentation
```

## What's Included（包含内容）

### Slash Commands（斜杠命令）
- `/generate-api-docs` - Generate API documentation（生成 API 文档）
- `/generate-readme` - Create or update README（创建或更新 README）
- `/sync-docs` - Sync docs with code changes（同步文档与代码更改）
- `/validate-docs` - Validate documentation（验证文档）

### Subagents（子代理）
- `api-documenter` - API documentation specialist（API 文档专家）
- `code-commentator` - Code comment improvements（代码注释改进）
- `example-generator` - Code example creation（代码示例创建）

### Templates（模板）
- `api-endpoint.md` - API endpoint documentation template（API 端点文档模板）
- `function-docs.md` - Function documentation template（函数文档模板）
- `adr-template.md` - Architecture Decision Record template（架构决策记录模板）

### MCP Servers（MCP 服务器）
- GitHub integration for documentation syncing（用于文档同步的 GitHub 集成）

## Usage（使用方法）

### Generate API Documentation（生成 API 文档）
```
/generate-api-docs
```

### Create README（创建 README）
```
/generate-readme
```

### Sync Documentation（同步文档）
```
/sync-docs
```

### Validate Documentation（验证文档）
```
/validate-docs
```

## Requirements（要求）

- Claude Code 1.0+
- GitHub access (optional)（GitHub 访问（可选））

## Example Workflow（工作流示例）

```
User: /generate-api-docs

Claude:
1. Scans all API endpoints in /src/api/
   扫描 /src/api/ 中的所有 API 端点
2. Delegates to api-documenter subagent
   委托给 api-documenter 子代理
3. Extracts function signatures and JSDoc
   提取函数签名和 JSDoc
4. Organizes by module/endpoint
   按模块/端点组织
5. Uses api-endpoint.md template
   使用 api-endpoint.md 模板
6. Generates comprehensive markdown docs
   生成全面的 Markdown 文档
7. Includes curl, JavaScript, and Python examples
   包含 curl、JavaScript 和 Python 示例

Result:
✅ API documentation generated
📄 Files created:
   - docs/api/users.md
   - docs/api/auth.md
   - docs/api/products.md
📊 Coverage: 23/23 endpoints documented
```

## Templates Usage（模板使用）

### API Endpoint Template（API 端点模板）
Use for documenting REST API endpoints with full examples.
用于使用完整示例记录 REST API 端点。

### Function Documentation Template（函数文档模板）
Use for documenting individual functions/methods.
用于记录单独的函数/方法。

### ADR Template（架构决策记录模板）
Use for documenting architectural decisions.
用于记录架构决策。

## Configuration（配置）

Set up GitHub token for documentation syncing:
设置 GitHub 令牌以进行文档同步：
```bash
export GITHUB_TOKEN="your_github_token"
```

## Best Practices（最佳实践）

- Keep documentation close to code（将文档保持在代码附近）
- Update docs with code changes（随代码更改更新文档）
- Include practical examples（包含实用示例）
- Validate regularly（定期验证）
- Use templates for consistency（使用模板保持一致性）
