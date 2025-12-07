# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-12-07

### Added

#### Core Infrastructure
- Initial plugin configuration (`.claude-plugin/plugin.json`)
- Plugin documentation (`CLAUDE.md`)

#### Code Review Agents
- `typescript-reviewer`: TypeScript/JavaScript code review with React patterns
- `python-reviewer`: Python code review with Django/FastAPI/Flask support
- `java-reviewer`: Java code review with Spring Boot/Jakarta EE patterns
- `architecture-strategist`: Architecture and design pattern review
- `security-sentinel`: OWASP-based security vulnerability scanning
- `performance-oracle`: Performance bottleneck identification
- `code-simplicity-reviewer`: Clean code and SOLID principles review

#### Research Agents
- `codebase-researcher`: Analyze and map existing codebases
- `framework-researcher`: Research frameworks and best practices

#### Documentation Agents
- `architecture-doc-generator`: Generate architecture documentation
- `api-doc-generator`: Generate API reference (OpenAPI/REST/GraphQL)
- `uml-generator`: Generate UML diagrams in Mermaid format
- `readme-generator`: Generate project README files
- `manual-generator`: Generate user manuals and guides

#### Workflow Agents
- `plan-executor`: Systematic plan execution with quality gates
- `review-coordinator`: Multi-agent review coordination

#### Commands
- `/polyglot:plan`: Convert feature descriptions to implementation plans
- `/polyglot:work`: Execute plans with git worktree isolation
- `/polyglot:review`: Multi-agent code review
- `/polyglot:docs`: Documentation generation
- `/polyglot:triage`: Interactive review finding resolution

#### Skills
- `docs-generator`: Documentation generation skill
- `code-analysis`: Code structure and pattern analysis
- `uml-generator`: UML diagram generation in Mermaid

#### Templates
- Architecture documentation template
- API reference template
- README template
- PRD (Product Requirements Document) template
- User manual template

### Languages Supported
- TypeScript/JavaScript (React, Node.js, Next.js)
- Python (Django, FastAPI, Flask)
- Java (Spring Boot, Jakarta EE)

---

## Version Guidelines

### Major Version (X.0.0)
- Breaking changes to command interface
- Major reorganization of agents
- Changes requiring user migration

### Minor Version (0.X.0)
- New agents or commands
- New skills or templates
- Significant feature additions

### Patch Version (0.0.X)
- Bug fixes
- Documentation updates
- Minor improvements

---

## Upcoming

### [1.1.0] - Planned
- [ ] Additional language support (Go, Rust)
- [ ] Enhanced UML generation with PlantUML option
- [ ] CI/CD integration commands
- [ ] Test generation agents

### [1.2.0] - Planned
- [ ] Interactive plan refinement
- [ ] Code generation templates
- [ ] Performance benchmarking tools
