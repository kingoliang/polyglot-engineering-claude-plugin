# 更新日志

本项目的所有重要更改都将记录在此文件中。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)，
版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [1.0.0] - 2024-12-07

### 新增

#### 核心基础设施
- 初始插件配置 (`.claude-plugin/plugin.json`)
- 插件文档 (`CLAUDE.md`)
- Marketplace 配置 (`.claude-plugin/marketplace.json`)

#### 代码审查代理
- `typescript-reviewer`：TypeScript/JavaScript 代码审查，支持 React 模式
- `python-reviewer`：Python 代码审查，支持 Django/FastAPI/Flask
- `java-reviewer`：Java 代码审查，支持 Spring Boot/Jakarta EE 模式
- `architecture-strategist`：架构和设计模式审查
- `security-sentinel`：基于 OWASP 的安全漏洞扫描
- `performance-oracle`：性能瓶颈识别
- `code-simplicity-reviewer`：清洁代码和 SOLID 原则审查

#### 研究代理
- `codebase-researcher`：分析和映射现有代码库
- `framework-researcher`：研究框架和最佳实践

#### 文档代理
- `architecture-doc-generator`：生成架构文档
- `api-doc-generator`：生成 API 参考（OpenAPI/REST/GraphQL）
- `uml-generator`：生成 Mermaid 格式的 UML 图
- `readme-generator`：生成项目 README 文件
- `manual-generator`：生成用户手册和指南

#### 工作流代理
- `plan-executor`：带质量门控的系统化计划执行
- `review-coordinator`：多代理审查协调

#### 命令
- `/polyglot:plan`：将功能描述转换为实施计划
- `/polyglot:work`：使用 git worktree 隔离执行计划
- `/polyglot:review`：多代理代码审查
- `/polyglot:docs`：文档生成
- `/polyglot:triage`：交互式审查问题处理

#### 技能
- `docs-generator`：文档生成技能
- `code-analysis`：代码结构和模式分析
- `uml-generator`：Mermaid 格式 UML 图生成

#### 模板
- 架构文档模板
- API 参考模板
- README 模板
- PRD（产品需求文档）模板
- 用户手册模板

### 支持的语言
- TypeScript/JavaScript（React、Node.js、Next.js）
- Python（Django、FastAPI、Flask）
- Java（Spring Boot、Jakarta EE）

---

## 版本规范

### 主版本 (X.0.0)
- 命令接口的破坏性变更
- 代理的重大重组
- 需要用户迁移的变更

### 次版本 (0.X.0)
- 新增代理或命令
- 新增技能或模板
- 重要功能添加

### 补丁版本 (0.0.X)
- Bug 修复
- 文档更新
- 小幅改进

---

## 计划中

### [1.1.0] - 计划中
- [ ] 额外语言支持（Go、Rust）
- [ ] 增强 UML 生成，支持 PlantUML 选项
- [ ] CI/CD 集成命令
- [ ] 测试生成代理

### [1.2.0] - 计划中
- [ ] 交互式计划细化
- [ ] 代码生成模板
- [ ] 性能基准测试工具
