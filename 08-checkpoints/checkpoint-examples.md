# Checkpoint Examples（检查点示例）

在 Claude Code 中有效使用检查点的真实示例。

Note: Checkpoints are created automatically with every user prompt. You do not need to manually save them. To rewind, press `Esc` twice (`Esc+Esc`) or use `/rewind` to open the checkpoint browser.

注意：检查点会在每个用户提示词时自动创建。您不需要手动保存。要回溯，请按两次 `Esc`（`Esc+Esc`）或使用 `/rewind` 打开检查点浏览器。

## Example 1: Database Migration（示例 1：数据库迁移）

### Scenario（场景）
You need to migrate from MySQL to PostgreSQL but want to explore both a direct migration and a gradual dual-write approach.

您需要从 MySQL 迁移到 PostgreSQL，但想探索直接迁移和渐进式双写方法。

### Workflow（工作流）

```
User: Let's implement a direct migration from MySQL to PostgreSQL
      [Checkpoint A created automatically]
      （让我们实现从 MySQL 到 PostgreSQL 的直接迁移）
      （检查点 A 自动创建）

Claude: I'll implement the direct migration...
（我将实现直接迁移...）
[Changes database driver, updates queries, modifies schema]
（更改数据库驱动程序、更新查询、修改模式）

User: Run the tests
      [Checkpoint B created automatically]
      （运行测试）
      （检查点 B 自动创建）

Claude: Running tests...
❌ 15 tests failing - connection pool issues
（15 个测试失败 - 连接池问题）

User: This approach has issues. Let's try the dual-write pattern instead.
[User presses Esc+Esc, selects Checkpoint A, chooses "Restore code and conversation"]
（这种方法有问题。让我们尝试双写模式。）
（用户按 Esc+Esc，选择检查点 A，选择"恢复代码和对话"）

User: Now implement a dual-write pattern where we write to both databases
（现在实现一个写入两个数据库的双写模式）

Claude: I'll implement dual-write migration...
（我将实现双写迁移...）
[Implements dual-write layer, gradual migration strategy]
（实现双写层、渐进式迁移策略）

User: Run the tests
（运行测试）

Claude: Running tests...
✅ All tests passing
（所有测试通过）

User: The dual-write approach is clearly safer. Let's commit this.
（双写方法显然更安全。让我们提交这个。）
```

## Example 2: Performance Optimization（示例 2：性能优化）

### Scenario（场景）
Multiple performance optimization strategies to try.

多种性能优化策略可以尝试。

### Workflow（工作流）

```
User: Let's optimize the API response time. Current: 450ms
      [Checkpoint "Baseline" created automatically]
      （让我们优化 API 响应时间。当前：450ms）
      （"基线"检查点自动创建）

Claude: I'll add database query caching...
（我将添加数据库查询缓存...）
[Implements Redis caching]
（实现 Redis 缓存）

User: Run performance tests
（运行性能测试）

Claude: Results: 280ms average response time (38% improvement)
（结果：平均响应时间 280ms（38% 改善））

User: Let me try a different approach.
[User presses Esc+Esc, selects "Baseline" checkpoint, chooses "Restore code and conversation"]
（让我尝试不同的方法。）
（用户按 Esc+Esc，选择"基线"检查点，选择"恢复代码和对话"）

User: Try database query optimization instead
（尝试数据库查询优化而不是）

Claude: I'll optimize database queries...
（我将优化数据库查询...）
[Adds indexes, optimizes N+1 queries]
（添加索引、优化 N+1 查询）

User: Run performance tests
（运行性能测试）

Claude: Results: 180ms average response time (60% improvement)
（结果：平均响应时间 180ms（60% 改善））

User: Let me also try a third approach.
[User presses Esc+Esc, selects "Baseline" checkpoint, chooses "Restore code and conversation"]
（让我也尝试第三种方法。）
（用户按 Esc+Esc，选择"基线"检查点，选择"恢复代码和对话"）

User: Try response compression and CDN
（尝试响应压缩和 CDN）

Claude: I'll add compression and CDN...
（我将添加压缩和 CDN...）
[Implements gzip, sets up CDN]
（实现 gzip、设置 CDN）

User: Run performance tests
（运行性能测试）

Claude: Results: 320ms average response time (29% improvement)
（结果：平均响应时间 320ms（29% 改善））

User: Query optimization was the best. Let me go back and combine it with caching.
[User presses Esc+Esc, selects the checkpoint after query optimization, chooses "Restore code and conversation"]
（查询优化是最好的。让我回去将它与缓存结合起来。）
（用户按 Esc+Esc，选择查询优化后的检查点，选择"恢复代码和对话"）

User: Now add Redis caching on top of these optimized queries
（在这些优化查询之上添加 Redis 缓存）

Claude: [Adds Redis caching on top of optimized queries]
（在优化查询之上添加 Redis 缓存）

User: Run performance tests
（运行性能测试）

Claude: Results: 95ms average response time (79% improvement) 🎉
（结果：平均响应时间 95ms（79% 改善）🎉）

User: Perfect! This is the winner. Let's commit this.
（完美！这是赢家。让我们提交这个。）
```

## Example 3: UI/UX Iteration（示例 3：UI/UX 迭代）

### Scenario（场景）
Trying different layouts for a dashboard.

尝试仪表板的不同布局。

### Workflow（工作流）

```
User: Let's redesign the dashboard with a sidebar layout
      [Checkpoint "Start" created automatically]
      （让我们用侧边栏布局重新设计仪表板）
      （"开始"检查点自动创建）

Claude: [Implements sidebar layout]
（实现侧边栏布局）

User: Show me a screenshot
（给我看截图）

Claude: [Shows screenshot]
（显示截图）

User: The sidebar feels cramped. Let's try a top navigation instead.
[User presses Esc+Esc, selects "Start" checkpoint, chooses "Restore code and conversation"]
（侧边栏感觉狭窄。让我们尝试顶部导航。）
（用户按 Esc+Esc，选择"开始"检查点，选择"恢复代码和对话"）

User: Try a top navigation layout
（尝试顶部导航布局）

Claude: [Implements top navigation]
（实现顶部导航）

User: Show me a screenshot
（给我看截图）

Claude: [Shows screenshot]
（显示截图）

User: Better, but let's try a card-based grid layout
[User presses Esc+Esc, selects "Start" checkpoint, chooses "Restore code and conversation"]
（更好，但让我们尝试基于卡片的网格布局）
（用户按 Esc+Esc，选择"开始"检查点，选择"恢复代码和对话"）

User: Try a card-based grid layout
（尝试基于卡片的网格布局）

Claude: [Implements card grid]
（实现卡片网格）

User: Show me a screenshot
（给我看截图）

Claude: [Shows screenshot]
（显示截图）

User: This is great! But can we combine the top nav with the card grid?
[User presses Esc+Esc, selects the checkpoint after the card grid, chooses "Restore code and conversation"]
（这很棒！但我们可以把顶部导航和卡片网格结合起来吗？）
（用户按 Esc+Esc，选择卡片网格后的检查点，选择"恢复代码和对话"）

User: Add top navigation to the card grid layout
（将顶部导航添加到卡片网格布局）

Claude: [Adds top navigation to card grid]
（将顶部导航添加到卡片网格）

User: Perfect! This is the final design.
（完美！这是最终设计。）
```

## Example 4: Debugging Session（示例 4：调试会话）

### Scenario（场景）
Hunting down a tricky bug with multiple hypotheses.

用多种假设追踪一个棘手的 bug。

### Workflow（工作流）

```
User: There's a memory leak in the application
      [Checkpoint "Before debugging" created automatically]
      （应用程序中存在内存泄漏）
      （"调试前"检查点自动创建）

Claude: Let me investigate...
（让我调查...）
[Analyzes code]
（分析代码）

User: I think it's in the event listeners. Let's fix those.
（我认为问题在事件监听器中。让我们修复那些。）

Claude: [Fixes event listener cleanup]
（修复事件监听器清理）

User: Run memory profiler
（运行内存分析器）

Claude: Still leaking memory - event listeners weren't the issue
（仍在泄漏内存 - 事件监听器不是问题）

User: Let me go back and try a different hypothesis.
[User presses Esc+Esc, selects "Before debugging" checkpoint, chooses "Restore code and conversation"]
（让我回去尝试不同的假设。）
（用户按 Esc+Esc，选择"调试前"检查点，选择"恢复代码和对话"）

User: Maybe it's the database connections?
（也许是数据库连接？）

Claude: [Implements connection pooling fixes]
（实现连接池修复）

User: Run memory profiler
（运行内存分析器）

Claude: Still leaking - not the connections either
（仍在泄漏 - 也不是连接）

User: Let me go back and try another angle.
[User presses Esc+Esc, selects "Before debugging" checkpoint, chooses "Restore code and conversation"]
（让我回去尝试另一个角度。）
（用户按 Esc+Esc，选择"调试前"检查点，选择"恢复代码和对话"）

User: Let's check for circular references
（让我们检查循环引用）

Claude: [Finds and fixes circular references in cache]
（找到并修复缓存中的循环引用）

User: Run memory profiler
（运行内存分析器）

Claude: ✅ Memory leak fixed! The circular references in the caching layer were the culprit.
（✅ 内存泄漏修复了！缓存层中的循环引用是罪魁祸首。）

User: Excellent! Let's commit this fix.
（太棒了！让我们提交这个修复。）
```

## Example 5: API Design Evolution（示例 5：API 设计演进）

### Scenario（场景）
Designing a REST API with multiple iterations.

设计具有多次迭代的 REST API。

### Workflow（工作流）

```
User: Create a REST API for our blog platform
      [Checkpoint "Before API design" created automatically]
      （为我们博客平台创建 REST API）
      （"API 设计前"检查点自动创建）

Claude: [Creates basic CRUD API]
（创建基本 CRUD API）

User: This is too simple. Let's add pagination and filtering
（这太简单了。让我们添加分页和过滤）

Claude: [Adds pagination and filtering]
（添加分页和过滤）

User: We need better resource relationships
（我们需要更好的资源关系）

Claude: [Implements HATEOAS links]
（实现 HATEOAS 链接）

User: Actually, let's try GraphQL instead of REST
[User presses Esc+Esc, selects "Before API design" checkpoint, chooses "Restore code and conversation"]
（实际上，让我们尝试 GraphQL 而不是 REST）
（用户按 Esc+Esc，选择"API 设计前"检查点，选择"恢复代码和对话"）

User: Implement a GraphQL API for our blog platform instead
（改为我们的博客平台实现 GraphQL API）

Claude: [Implements GraphQL API]
（实现 GraphQL API）

User: I think REST is better for our use case.
[User presses Esc+Esc, selects the checkpoint after HATEOAS, chooses "Restore code and conversation"]
（我认为 REST 更适合我们的用例）
（用户按 Esc+Esc，选择 HATEOAS 后的检查点，选择"恢复代码和对话"）

User: Let's finalize the REST approach.
（让我们最终确定 REST 方法。）
```

## Example 6: Configuration Management（示例 6：配置管理）

### Scenario（场景）
Testing different configuration approaches.

测试不同的配置方法。

### Workflow（工作流）

```
User: Move configuration to environment variables
      [Checkpoint "Original config" created automatically]
      （将配置移到环境变量）
      （"原始配置"检查点自动创建）

Claude: [Implements env var configuration]
（实现环境变量配置）

User: Test in development
（在开发中测试）

Claude: Works locally but deployment issues in production
（本地工作正常但生产环境部署有问题）

User: Let me try a different approach.
[User presses Esc+Esc, selects "Original config" checkpoint, chooses "Restore code and conversation"]
（让我尝试不同的方法。）
（用户按 Esc+Esc，选择"原始配置"检查点，选择"恢复代码和对话"）

User: Try a config file approach with validation
（尝试带验证的配置文件方法）

Claude: [Implements YAML config with JSON schema validation]
（实现带 JSON schema 验证的 YAML 配置）

User: Test in development
（在开发中测试）

Claude: ✅ Works well, good validation errors
（✅ 工作良好，验证错误信息也很好）

User: Can we also support env vars for sensitive values?
（我们也可以支持敏感值的环境变量吗？）

Claude: [Adds env var override for secrets]
（为 secrets 添加环境变量覆盖）

User: Test deployment
（测试部署）

Claude: ✅ All environments working correctly
（✅ 所有环境都正常工作）

User: Perfect! This is production-ready.
（完美！这可以投入生产了。）
```

## Example 7: Test Strategy（示例 7：测试策略）

### Scenario（场景）
Implementing comprehensive testing.

实施全面测试。

### Workflow（工作流）

```
User: Add unit tests for the auth module
      [Checkpoint created automatically]
      （为 auth 模块添加单元测试）
      （自动创建检查点）

Claude: [Adds Jest unit tests]
（添加 Jest 单元测试）

User: Run tests
（运行测试）

Claude: 45 tests passing, 78% coverage
（45 个测试通过，78% 覆盖率）

User: Add integration tests too
（也添加集成测试）

Claude: [Adds integration tests]
（添加集成测试）

User: Run tests
（运行测试）

Claude: 89 tests passing, 92% coverage, but tests are slow (3 minutes)
（89 个测试通过，92% 覆盖率，但测试很慢（3 分钟））

User: The tests are too slow. Let's optimize.
（测试太慢了。让我们优化。）

Claude: [Optimizes test setup, adds parallel execution]
（优化测试设置，添加并行执行）

User: Run tests
（运行测试）

Claude: 89 tests passing, 92% coverage, 35 seconds ✅
（89 个测试通过，92% 覆盖率，35 秒 ✅）

User: Great! Now add E2E tests for critical paths
（太棒了！现在为关键路径添加 E2E 测试）

Claude: [Adds Playwright E2E tests]
（添加 Playwright E2E 测试）

User: Run all tests
（运行所有测试）

Claude: 112 tests passing, 94% coverage, 2 minutes
（112 个测试通过，94% 覆盖率，2 分钟）

User: Perfect balance of coverage and speed!
（完美的覆盖率和速度平衡！）
```

## Example 8: Using Summarize from Checkpoint（示例 8：使用从检查点总结）

### Scenario（场景）
After a long debugging session, you want to condense the conversation while preserving context.

在长时间的调试会话之后，您想在保留上下文的同时压缩对话。

### Workflow（工作流）

```
User: [After 20+ messages of debugging and exploration]
（[经过 20 多条调试和探索消息后]）

[User presses Esc+Esc, selects an early checkpoint, chooses "Summarize from here"]
（用户按 Esc+Esc，选择早期检查点，选择"从这里总结"）
[Optionally provides instructions: "Focus on what we tried and what worked"]
（可选提供指令："专注于我们尝试了什么，什么有效"）

Claude: [Generates a summary of the conversation from that point forward]
（[生成从该点开始的对话摘要]）
[Original messages are preserved in the transcript]
（[原始消息保留在记录中]）
[The summary replaces the visible conversation, reducing context window usage]
（[摘要替换可见对话，减少上下文窗口使用]）

User: Now let's continue with the approach that worked.
（现在让我们继续使用有效的方法。）
```

## Key Takeaways（关键要点）

1. **Checkpoints are automatic（检查点是自动的）**: Every user prompt creates a checkpoint -- no manual saving needed（每个用户提示词都会创建检查点 -- 无需手动保存）
2. **Use Esc+Esc or /rewind（使用 Esc+Esc 或 /rewind）**: These are the two ways to access the checkpoint browser（这是访问检查点浏览器的两种方式）
3. **Choose the right restore option（选择正确的恢复选项）**: Restore code, conversation, both, or summarize depending on your needs（根据需要恢复代码、对话、两者或总结）
4. **Don't fear experimentation（不要害怕实验）**: Checkpoints make it safe to try radical changes（检查点使尝试激进更改变得安全）
5. **Combine with git（与 git 结合使用）**: Use checkpoints for exploration, git for finalized work（使用检查点进行探索，使用 git 进行最终确定的工作）
6. **Summarize long sessions（总结长会话）**: Use "Summarize from here" to keep conversations manageable（使用"从这里总结"保持对话可管理）
