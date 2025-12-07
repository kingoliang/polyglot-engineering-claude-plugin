# Polyglot Engineering 多语言工程插件

## 概述

本插件为 TypeScript、Python 和 Java 项目实现了全面的工程工作流。提供代码审查、规划和文档生成功能，遵循复合工程理念。

## 插件结构

```
polyglot-engineering/
├── .claude-plugin/
│   ├── plugin.json          # 插件配置
│   └── marketplace.json     # Marketplace 配置
├── agents/
│   ├── review/              # 代码审查代理
│   │   ├── typescript-reviewer.md
│   │   ├── python-reviewer.md
│   │   ├── java-reviewer.md
│   │   ├── architecture-strategist.md
│   │   ├── security-sentinel.md
│   │   ├── performance-oracle.md
│   │   └── code-simplicity-reviewer.md
│   ├── research/            # 研究代理
│   │   ├── codebase-researcher.md
│   │   └── framework-researcher.md
│   ├── docs/                # 文档代理
│   │   ├── architecture-doc-generator.md
│   │   ├── api-doc-generator.md
│   │   ├── uml-generator.md
│   │   ├── readme-generator.md
│   │   └── manual-generator.md
│   └── workflow/            # 工作流代理
│       ├── plan-executor.md
│       └── review-coordinator.md
├── commands/                # 插件命令
│   ├── plan.md
│   ├── work.md
│   ├── review.md
│   ├── docs.md
│   └── triage.md
├── skills/                  # 可复用技能
│   ├── docs-generator/
│   ├── code-analysis/
│   └── uml-generator/
└── templates/               # 文档模板
    ├── architecture/
    ├── api/
    ├── readme/
    ├── manual/
    └── prd/
```

## 核心命令

### `/polyglot:plan`
将功能描述转换为详细的实施计划，包含研究和验收标准。

### `/polyglot:work`
使用隔离的 git worktree 系统执行计划。

### `/polyglot:review`
执行多代理代码审查，包含语言特定和横切关注点分析。

### `/polyglot:docs`
生成全面的文档（架构、API、UML、README、手册）。

### `/polyglot:triage`
展示审查发现以供批准和优先级排序。

## 版本控制

修改此插件时：
1. 更新 `.claude-plugin/plugin.json` 中的版本号
2. 在 `CHANGELOG.md` 中记录更改
3. 确保 README.md 反映当前状态

### 版本类型
- **主版本 (MAJOR)**：破坏性变更、重大重组
- **次版本 (MINOR)**：新代理、命令或技能
- **补丁版本 (PATCH)**：Bug 修复、文档更新、小幅改进

## 支持的语言

- **TypeScript/JavaScript**：全面支持 React、Node.js、Next.js、Express
- **Python**：Django、FastAPI、Flask、异步模式、类型提示
- **Java**：Spring Boot、Jakarta EE、Maven/Gradle、设计模式
