# Polyglot Engineering 多语言工程插件

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-purple.svg)](https://claude.ai)

一个全面的 Claude Code 插件，支持 TypeScript、Python 和 Java 项目，实现"复合工程"理念——让每一次工程工作都使后续工作变得更容易。

## 功能特性

- **多语言代码审查**：针对 TypeScript、Python、Java 的专业审查器
- **架构分析**：设计模式、SOLID 原则、系统设计审查
- **安全扫描**：基于 OWASP 的漏洞检测
- **性能优化**：识别瓶颈和优化机会
- **文档生成**：架构文档、API 参考、UML 图、README、用户手册
- **计划驱动开发**：遵循 BMAD 方法论的结构化开发

## 快速开始

### 安装

#### 方式一：添加 Marketplace（推荐）

```bash
# 在 Claude Code 中添加此仓库作为 marketplace
/plugin marketplace add kingoliang/polyglot-engineering-claude-plugin

# 安装插件
/plugin install polyglot-engineering@kingoliang
```

#### 方式二：交互式安装

```bash
# 打开插件浏览器
/plugin

# 选择 "Browse Plugins"，找到 polyglot-engineering
```

#### 方式三：团队配置

在项目的 `.claude/settings.json` 中添加：

```json
{
  "marketplaces": ["kingoliang/polyglot-engineering-claude-plugin"],
  "plugins": ["polyglot-engineering@kingoliang"]
}
```

团队成员信任仓库后，插件会自动安装。

### 验证安装

```bash
# 查看可用命令
/help

# 查看已安装插件
/plugin
```

### 使用示例

```bash
# 规划新功能
/polyglot:plan 添加 JWT 用户认证功能

# 执行计划
/polyglot:work

# 审查代码变更
/polyglot:review staged

# 生成文档
/polyglot:docs all

# 处理审查问题
/polyglot:triage
```

## 命令说明

| 命令 | 说明 |
|------|------|
| `/polyglot:plan` | 将功能描述转换为详细的实施计划 |
| `/polyglot:work` | 使用 git worktree 隔离环境系统执行计划 |
| `/polyglot:review` | 多代理代码审查，支持语言特定分析 |
| `/polyglot:docs` | 从代码生成全面的文档 |
| `/polyglot:triage` | 交互式处理审查发现的问题 |

## 代理列表

### 代码审查代理

| 代理 | 用途 |
|------|------|
| `typescript-reviewer` | TypeScript/JavaScript 最佳实践、React 模式 |
| `python-reviewer` | Python 模式、Django/FastAPI/Flask 审查 |
| `java-reviewer` | Java 模式、Spring Boot、Jakarta EE 审查 |
| `architecture-strategist` | 设计模式、系统架构 |
| `security-sentinel` | OWASP 漏洞、安全最佳实践 |
| `performance-oracle` | 性能瓶颈、优化建议 |
| `code-simplicity-reviewer` | 清洁代码、SOLID、可维护性 |

### 研究代理

| 代理 | 用途 |
|------|------|
| `codebase-researcher` | 分析和映射现有代码库 |
| `framework-researcher` | 研究框架和库 |

### 文档代理

| 代理 | 用途 |
|------|------|
| `architecture-doc-generator` | 系统架构文档 |
| `api-doc-generator` | API 参考（OpenAPI/REST/GraphQL） |
| `uml-generator` | Mermaid 格式的 UML 图 |
| `readme-generator` | 项目 README 文件 |
| `manual-generator` | 用户手册和指南 |

### 工作流代理

| 代理 | 用途 |
|------|------|
| `plan-executor` | 执行实施计划 |
| `review-coordinator` | 协调多代理审查 |

## 文档生成

生成各种类型的文档：

```bash
# 生成所有文档
/polyglot:docs all

# 架构文档
/polyglot:docs architecture

# API 参考
/polyglot:docs api

# UML 图
/polyglot:docs uml

# README
/polyglot:docs readme

# 用户手册
/polyglot:docs manual
```

### 输出结构

```
docs/
├── architecture/
│   ├── overview.md
│   ├── components.md
│   └── decisions/
├── api/
│   ├── reference.md
│   └── openapi.yaml
├── diagrams/
│   ├── class-diagram.md
│   └── sequence-*.md
└── user-guide/
    ├── getting-started.md
    └── user-manual.md
```

## 项目结构

```
polyglot-engineering/
├── .claude-plugin/
│   ├── plugin.json          # 插件配置
│   └── marketplace.json     # Marketplace 配置
├── agents/
│   ├── review/              # 代码审查代理
│   ├── research/            # 研究代理
│   ├── docs/                # 文档代理
│   └── workflow/            # 工作流代理
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
├── templates/               # 文档模板
│   ├── architecture/
│   ├── api/
│   ├── readme/
│   ├── manual/
│   └── prd/
├── docs/                    # 使用文档
│   └── USER_GUIDE.md
├── CLAUDE.md               # 插件说明
├── CHANGELOG.md            # 版本历史
└── README.md               # 本文件
```

## 支持的语言

### TypeScript/JavaScript
- React, Vue, Angular
- Next.js, Nuxt.js
- Express, Fastify, NestJS
- Jest, Vitest, Playwright

### Python
- Django, FastAPI, Flask
- SQLAlchemy, Pydantic
- pytest, asyncio

### Java
- Spring Boot, Spring Security
- Jakarta EE, JPA
- Maven, Gradle
- JUnit 5, Mockito

## 设计理念

本插件遵循 **复合工程 (Compounding Engineering)** 理念：

> "每一次工程工作都应该使后续工作变得更容易，而不是更困难。"

通过以下方式实现：
1. **规划**：基于研究的详细实施计划
2. **执行**：系统化、质量验证的实现
3. **审查**：多代理、全面的代码审查
4. **文档**：自动生成、始终保持最新的文档

## 贡献指南

欢迎贡献！提交 PR 前请阅读贡献指南。

1. Fork 本仓库
2. 创建功能分支
3. 提交更改
4. 更新 CHANGELOG.md
5. 提交 Pull Request

## 许可证

MIT 许可证 - 详见 [LICENSE](LICENSE)

## 致谢

- 灵感来源：[compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin)
- 文档结构参考：[BMAD Method](https://github.com/bmad-code-org/BMAD-METHOD)

---

使用 [Claude Code](https://claude.ai) 构建
