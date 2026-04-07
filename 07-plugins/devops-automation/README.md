<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../../resources/logos/claude-howto-logo-dark.svg">
  <img alt="Claude How To" src="../../resources/logos/claude-howto-logo.svg">
</picture>

# DevOps Automation Plugin（DevOps 自动化插件）

面向部署、监控和事件响应的完整 DevOps 自动化。

## Features（功能特性）

✅ Automated deployments（自动化部署）
✅ Rollback procedures（回滚程序）
✅ System health monitoring（系统健康监控）
✅ Incident response workflows（事件响应工作流）
✅ Kubernetes integration（Kubernetes 集成）

## Installation（安装）

```bash
/plugin install devops-automation
```

## What's Included（包含内容）

### Slash Commands（斜杠命令）
- `/deploy` - Deploy to production or staging（部署到生产或预发环境）
- `/rollback` - Rollback to previous version（回滚到先前版本）
- `/status` - Check system health（检查系统健康状态）
- `/incident` - Handle production incidents（处理生产环境事件）

### Subagents（子代理）
- `deployment-specialist` - Deployment operations（部署操作）
- `incident-commander` - Incident coordination（事件协调）
- `alert-analyzer` - System health analysis（系统健康分析）

### MCP Servers（MCP 服务器）
- Kubernetes integration（Kubernetes 集成）

### Scripts（脚本）
- `deploy.sh` - Deployment automation（部署自动化）
- `rollback.sh` - Rollback automation（回滚自动化）
- `health-check.sh` - Health check utilities（健康检查工具）

### Hooks（钩子）
- `pre-deploy.js` - Pre-deployment validation（部署前验证）
- `post-deploy.js` - Post-deployment tasks（部署后任务）

## Usage（使用方法）

### Deploy to Staging（部署到预发环境）
```
/deploy staging
```

### Deploy to Production（部署到生产环境）
```
/deploy production
```

### Rollback（回滚）
```
/rollback production
```

### Check Status（检查状态）
```
/status
```

### Handle Incident（处理事件）
```
/incident
```

## Requirements（要求）

- Claude Code 1.0+
- Kubernetes CLI (kubectl)
- Cluster access configured（已配置集群访问）

## Configuration（配置）

Set up your Kubernetes config:
配置您的 Kubernetes：

```bash
export KUBECONFIG=~/.kube/config
```

## Example Workflow（工作流示例）

```
User: /deploy production

Claude:
1. Runs pre-deploy hook (validates kubectl, cluster connection)
   运行部署前钩子（验证 kubectl、集群连接）
2. Delegates to deployment-specialist subagent
   委托给部署专家子代理
3. Runs deploy.sh script
   运行部署脚本
4. Monitors deployment progress via Kubernetes MCP
   通过 Kubernetes MCP 监控部署进度
5. Runs post-deploy hook (waits for pods, smoke tests)
   运行部署后钩子（等待 Pods、冒烟测试）
6. Provides deployment summary
   提供部署摘要

Result:
✅ Deployment complete
📦 Version: v2.1.0
🚀 Pods: 3/3 ready
⏱️  Time: 2m 34s
```
