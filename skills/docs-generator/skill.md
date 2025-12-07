# 文档生成器技能

从代码分析生成各类文档的综合技能。

## 能力

- 生成架构文档
- 创建 API 参考文档
- 生成 UML 图（Mermaid 格式）
- 编写 README 文件
- 创建用户手册
- 生成变更日志条目

## 用法

此技能由 `/polyglot:docs` 命令和文档代理调用。

## 流程

### 1. 代码分析

```bash
# 分析项目结构
find src -type f \( -name "*.ts" -o -name "*.py" -o -name "*.java" \)

# 提取导出和公共 API
grep -r "export" src/
```

### 2. 模式识别

- 识别架构模式
- 映射组件关系
- 记录数据流

### 3. 模板应用

根据文档类型应用相应模板：
- `architecture-template.md` 用于架构文档
- `api-template.md` 用于 API 参考
- `readme-template.md` 用于 README 文件
- `manual-template.md` 用于用户手册

### 4. 内容生成

生成内容章节：
1. 概述和目的
2. 技术细节
3. 使用示例
4. 配置选项

### 5. 质量检查

- 验证完整性
- 检查失效链接
- 验证代码示例
- 确保一致性

## 输出位置

| 文档类型 | 默认位置 |
|----------|----------|
| 架构 | `docs/architecture/` |
| API | `docs/api/` |
| UML | `docs/diagrams/` |
| README | 项目根目录 |
| 手册 | `docs/user-guide/` |

## 集成点

- 与 `codebase-researcher` 代理协作
- 使用 `templates/` 目录中的模板
- 输出到标准文档位置
