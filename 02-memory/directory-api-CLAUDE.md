# API 模块标准

此文件覆盖 /src/api/ 下所有内容的根 CLAUDE.md。

## API 特定标准

### 请求验证
- 使用 Zod 进行模式验证
- 始终验证输入
- 返回 400 和验证错误
- 包含字段级错误详情

### 认证
- 所有端点需要 JWT 令牌
- 令牌在 Authorization 头中
- 令牌 24 小时后过期
- 实现刷新令牌机制

### 响应格式

所有响应必须遵循此结构：

```json
{
  "success": true,
  "data": { /* actual data */ },
  "timestamp": "2025-11-06T10:30:00Z",
  "version": "1.0"
}
```

错误响应：
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "User message",
    "details": { /* field errors */ }
  },
  "timestamp": "2025-11-06T10:30:00Z"
}
```

### 分页
- 使用基于游标的分页（不是偏移量）
- 包含 `hasMore` 布尔值
- 最大页面大小限制为 100
- 默认页面大小：20

### 速率限制
- 已认证用户每小时 1000 次请求
- 公共端点每小时 100 次请求
- 超限时返回 429
- 包含 retry-after 头

### 缓存
- 使用 Redis 进行会话缓存
- 默认缓存时长：5 分钟
- 写操作时使缓存失效
- 使用资源类型标记缓存键
