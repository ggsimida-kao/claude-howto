---
name: Setup CI/CD Pipeline
description: 实现预提交钩子和 GitHub Actions 以确保质量
tags: ci-cd, devops, automation
---

# 设置 CI/CD 流水线

根据项目类型实施全面的 DevOps 质量门控：

1. **分析项目**：检测语言、框架、构建系统和现有工具
2. **配置预提交钩子**，使用特定语言的工具：
   - 格式化：Prettier/Black/gofmt/rustfmt 等
   - Linting：ESLint/Ruff/golangci-lint/Clippy 等
   - 安全：Bandit/gosec/cargo-audit/npm audit 等
   - 类型检查：TypeScript/mypy/flow（如适用）
   - 测试：运行相关测试套件
3. **创建 GitHub Actions 工作流程**（.github/workflows/）：
   - 在 push/PR 时镜像预提交检查
   - 多版本/平台矩阵（如适用）
   - 构建和测试验证
   - 部署步骤（如需要）
4. **验证流水线**：本地测试，创建测试 PR，确认所有检查通过

使用免费/开源工具。尊重现有配置。保持执行快速。
