# /polyglot:triage 命令

交互式展示审查发现的问题，支持自动修复功能。

## 用法

```
/polyglot:triage [审查引用]
```

## 流程

### 阶段1：加载发现

1. 加载最近的审查或指定的审查
2. 按严重程度和文件分组
3. 准备可用的自动修复建议

### 阶段2：交互式处理

展示每个发现及选项：

```markdown
## 发现 1/10：[H1] 缺少错误处理

**严重程度**：高
**文件**：`src/api/users.ts:45`
**代理**：typescript-reviewer

**问题**：异步函数缺少 try-catch

**当前代码**：
```typescript
async function getUser(id: string) {
  const user = await db.users.find(id);
  return user;
}
```

**建议修复**：
```typescript
async function getUser(id: string) {
  try {
    const user = await db.users.find(id);
    if (!user) throw new NotFoundError('用户不存在');
    return user;
  } catch (error) {
    logger.error('获取用户失败', { id, error });
    throw error;
  }
}
```

---

**操作**：
[1] 应用修复 - 自动应用建议的修复
[2] 跳过 - 暂时跳过此发现
[3] 忽略 - 标记为不修复并说明原因
[4] 自定义 - 提供自定义修复
[5] 查看上下文 - 查看更多周围代码
```

### 阶段3：处理跟踪

跟踪所有决策：

| 发现 | 决策 | 已应用 |
|------|------|--------|
| H1 | 应用修复 | 是 |
| H2 | 跳过 | - |
| M1 | 忽略: 有意设计 | - |

### 阶段4：摘要

```markdown
# Triage 摘要

## 已应用的修复
- [H1] `users.ts` 中的错误处理
- [M2] `auth.ts` 中添加类型注解

## 已跳过（稍后处理）
- [H2] `query.ts` 中的性能优化

## 已忽略
- [M1] 为兼容性有意使用此模式

## 剩余问题
| 严重程度 | 数量 |
|----------|------|
| 高 | 1 |
| 中 | 2 |

## 后续步骤
- 处理跳过的高优先级问题
- 考虑中优先级问题
- 修复后重新审查：`/polyglot:review staged`
```

## 自动修复能力

### 支持的自动修复

| 问题类型 | 自动修复 |
|----------|---------|
| 缺少类型 | 是 |
| 缺少错误处理 | 模板 |
| 未使用的导入 | 是 |
| 格式问题 | 是 |
| 简单重构 | 是 |
| 安全问题 | 视情况 |
| 架构问题 | 否（需要设计） |

### 修复模板

当无法精确自动修复时，提供模板：

```typescript
// 模板：错误处理
try {
  // 你的代码
} catch (error) {
  // 处理错误
  throw error;
}
```

## 批量操作

### 应用所有安全修复
```
/polyglot:triage --apply-safe
```
应用所有低风险修复（格式、导入、简单类型）。

### 跳过所有低优先级
```
/polyglot:triage --skip-low
```
聚焦于高和中优先级问题。

### 仅处理严重问题
```
/polyglot:triage --critical-only
```
仅显示严重和高严重程度问题。

## 决策指南

### 何时应用
- 明确的改进
- 无行为变更
- 模式被充分理解
- 有测试覆盖

### 何时跳过
- 需要更多上下文
- 不确定需求
- 需要与团队讨论
- 将在相关任务中处理

### 何时忽略
- 有意的模式
- 误报
- 不适用于此代码库
- 已在其他地方处理

## 集成

### Triage 之后
```bash
# 运行测试验证修复
npm test

# 重新审查
/polyglot:review staged

# 全部通过后提交
git add -A
git commit -m "fix: 处理代码审查发现"
```

### 与 Work 命令配合
```bash
# 执行工作期间
/polyglot:work step-3

# 快速审查步骤
/polyglot:review staged --quick

# 处理任何问题
/polyglot:triage
```

## 输出格式

```markdown
# Triage 完成

**会话**：来自 [日期] 的审查
**发现总数**：10

## 处理摘要
| 操作 | 数量 |
|------|------|
| 已应用 | 5 |
| 已跳过 | 3 |
| 已忽略 | 2 |

## 验证
- [ ] 所有测试通过
- [ ] 无新 lint 错误
- [ ] 构建成功

## 使用的命令
```bash
git add src/api/users.ts src/services/auth.ts
git commit -m "fix: 应用代码审查修复

- 添加 getUser 错误处理
- 添加缺失的类型注解
- 移除未使用的导入
"
```
```
