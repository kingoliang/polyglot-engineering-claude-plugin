# /polyglot:docs 命令

从现有代码生成全面的文档，包括架构文档、API 文档、UML 图、README 和用户手册。

## 用法

```
/polyglot:docs [类型] [选项]
```

### 文档类型

| 类型 | 命令 | 描述 |
|------|------|------|
| 全部 | `/polyglot:docs all` | 生成所有文档 |
| 架构 | `/polyglot:docs architecture` | 系统架构文档 |
| API | `/polyglot:docs api` | API 参考文档 |
| UML | `/polyglot:docs uml` | UML 图 |
| README | `/polyglot:docs readme` | 项目 README |
| 手册 | `/polyglot:docs manual` | 用户手册 |

## 流程

### 阶段1：分析（计划驱动方法）

遵循复合工程计划理念：

1. **代码库研究**
   - 调用 `codebase-researcher` 理解项目
   - 映射项目结构和模式
   - 识别关键组件

2. **文档审计**
   - 检查现有文档
   - 识别缺口
   - 标注过时内容

3. **文档计划**
   - 确定需要生成的内容
   - 按依赖排序
   - 估算范围

### 阶段2：生成

调用相应的文档代理：

1. **架构文档**
   - `architecture-doc-generator` 代理
   - 产出：系统概述、组件文档、ADR

2. **API 文档**
   - `api-doc-generator` 代理
   - 产出：端点文档、Schema、示例

3. **UML 图**
   - `uml-generator` 代理
   - 产出：类图、序列图、组件图

4. **README**
   - `readme-generator` 代理
   - 产出：带徽章、使用说明的项目 README

5. **用户手册**
   - `manual-generator` 代理
   - 产出：入门指南、完整手册、故障排除

### 阶段3：输出

在标准位置生成文件：

```
project/
├── README.md                    # 项目 README
├── docs/
│   ├── architecture/
│   │   ├── overview.md          # 系统概述
│   │   ├── components.md        # 组件文档
│   │   ├── data-flow.md         # 数据流文档
│   │   └── decisions/           # 架构决策记录
│   │       └── ADR-001-*.md
│   ├── api/
│   │   ├── reference.md         # API 参考
│   │   ├── openapi.yaml         # OpenAPI 规范（REST）
│   │   └── examples/            # API 示例
│   ├── diagrams/
│   │   ├── class-diagram.md     # 类图
│   │   ├── sequence-*.md        # 序列图
│   │   └── component.md         # 组件图
│   └── user-guide/
│       ├── getting-started.md   # 入门指南
│       ├── user-manual.md       # 完整用户手册
│       └── troubleshooting.md   # 故障排除指南
└── CHANGELOG.md                 # 变更日志
```

## 命令选项

### 范围选项
```
--scope=full        # 生成完整文档
--scope=minimal     # 仅生成必要文档
--scope=update      # 仅更新现有文档
```

### 格式选项
```
--format=markdown   # Markdown（默认）
--format=html       # HTML 输出
--format=pdf        # PDF 输出（需要 pandoc）
```

### 目标选项
```
--target=developers   # 面向开发者的文档
--target=users        # 面向最终用户的文档
--target=all          # 两者兼顾
```

## 使用示例

### 生成所有文档
```
/polyglot:docs all
```

### 仅生成架构文档
```
/polyglot:docs architecture
```

### 生成带 OpenAPI 的 API 文档
```
/polyglot:docs api --format=openapi
```

### 为特定包生成 UML
```
/polyglot:docs uml --path=src/services
```

### 仅更新 README
```
/polyglot:docs readme --scope=update
```

### 生成用户手册
```
/polyglot:docs manual --target=users
```

## 输出格式

```markdown
# 文档生成报告

**项目**：[项目名称]
**日期**：[生成日期]

## 生成的文档

| 文档 | 路径 | 状态 |
|------|------|------|
| README | README.md | 创建 |
| 架构概述 | docs/architecture/overview.md | 创建 |
| API 参考 | docs/api/reference.md | 创建 |
| 类图 | docs/diagrams/class-diagram.md | 创建 |
| 入门指南 | docs/user-guide/getting-started.md | 创建 |

## 摘要

- **文档总数**：10
- **新建**：8
- **更新**：2

## 后续步骤

1. 审查生成的文档
2. 添加项目特定细节
3. 更新占位符内容
4. 提交文档变更

## 备注

- [观察或建议]
```

## 与 BMAD 方法集成

遵循 BMAD 的文档原则：

### 文档分片
大型项目自动分片：
- `overview.md` - 高级摘要
- `details/` - 详细组件文档
- `reference/` - 技术参考

### 上下文工程
为 AI 代理包含上下文：
- 清晰的文件用途
- 交叉引用
- 实现备注

### 活文档
设计为：
- 易于更新
- 版本控制
- 链接到代码

## 最佳实践

1. **尽早生成**：随代码编写创建文档
2. **审查生成内容**：AI 生成的文档需要审查
3. **保持更新**：重大变更后重新运行
4. **自定义内容**：添加项目特定内容
5. **链接到代码**：引用实际文件路径
