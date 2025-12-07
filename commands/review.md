# /polyglot:review 命令

执行全面的多代理代码审查，包含语言特定和横切关注点分析。

## 用法

```
/polyglot:review [目标]
```

### 目标类型
- `staged` - 审查暂存的变更
- `branch` - 审查当前分支 vs main
- `pr #123` - 审查指定 PR
- `files path/to/file.ts` - 审查指定文件
- `commit abc123` - 审查指定提交

## 流程

### 阶段1：分析

1. **变更检测**
   ```bash
   # 确定审查内容
   git diff --name-only [target]
   ```

2. **语言分类**
   - 识别文件类型
   - 按语言分组
   - 标注混合语言变更

3. **变更范围评估**
   - 新文件 vs 修改
   - 添加/删除的行数
   - 受影响的组件

### 阶段2：代理调用

根据变更调用相应代理：

| 变更文件 | 调用的代理 |
|----------|-----------|
| *.ts, *.tsx | typescript-reviewer |
| *.py | python-reviewer |
| *.java | java-reviewer |
| API 路由 | architecture-strategist, security-sentinel |
| 数据库 | performance-oracle, security-sentinel |
| 认证代码 | security-sentinel |
| 所有变更 | code-simplicity-reviewer |

### 阶段3：执行审查

每个代理审查并报告：
1. 安全问题
2. 性能关注
3. 代码质量问题
4. 最佳实践违反
5. 改进建议

### 阶段4：综合

`review-coordinator` 代理：
1. 收集所有发现
2. 去除重复
3. 分配优先级
4. 创建统一报告

## 输出格式

```markdown
# 代码审查报告

**目标**：[审查的内容]
**分支**：[分支名称]
**审查代理**：[使用的代理列表]
**日期**：[审查日期]

---

## 摘要

| 严重程度 | 数量 |
|----------|------|
| 严重 | 0 |
| 高 | 2 |
| 中 | 5 |
| 低 | 3 |

**结论**：[通过 / 需要修改 / 阻塞]

---

## 严重问题
*必须在合并前修复*

无

---

## 高优先级问题
*应该修复*

### [H1] 缺少错误处理
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

## 中优先级问题
*考虑修复*

### [M1] N+1 查询模式
...

---

## 低优先级问题
*可选改进*

### [L1] 考虑使用 Record 类型
...

---

## 正面观察

- 新认证逻辑测试覆盖良好
- 服务层关注点分离清晰
- TypeScript 泛型使用正确

---

## 审查的文件

| 文件 | 问题数 | 状态 |
|------|--------|------|
| src/api/users.ts | 2 | 需要修改 |
| src/services/auth.ts | 0 | 通过 |
| tests/auth.test.ts | 1 | 小问题 |

---

## 行动项目

1. [ ] 修复 `users.ts:45` 的错误处理
2. [ ] 解决 `users.ts:78` 的 N+1 查询
3. [ ] 考虑 Record 类型建议
```

## 审查深度

### 快速审查
- 仅语法和类型问题
- 适用于小变更

```
/polyglot:review staged --quick
```

### 标准审查（默认）
- 所有语言特定检查
- 敏感区域安全检查
- 数据操作性能检查

```
/polyglot:review branch
```

### 深度审查
- 所有代理参与
- 架构审查
- 全面安全扫描

```
/polyglot:review pr #123 --deep
```

## 与 Triage 集成

审查后使用：
```
/polyglot:triage
```

交互式处理发现的问题，支持自动修复建议。

## 最佳实践

1. **尽早审查**：在大提交前审查
2. **频繁审查**：小审查更有效
3. **处理严重问题**：永不带严重问题合并
4. **从发现中学习**：使用模式预防未来问题
