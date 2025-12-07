# Polyglot Engineering Plugin

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-purple.svg)](https://claude.ai)

A comprehensive Claude Code plugin for TypeScript, Python, and Java projects implementing the "compounding engineering" philosophy - where each unit of engineering work makes subsequent work easier.

## Features

- **Multi-Language Code Review**: Specialized reviewers for TypeScript, Python, and Java
- **Architecture Analysis**: Design patterns, SOLID principles, and system design review
- **Security Scanning**: OWASP-based vulnerability detection
- **Performance Optimization**: Identify bottlenecks and optimization opportunities
- **Documentation Generation**: Architecture docs, API reference, UML diagrams, README, user manuals
- **Plan-Based Development**: Structured approach following BMAD methodology

## Quick Start

### Installation

#### Method 1: Add as Marketplace (Recommended)

```bash
# In Claude Code, add this repository as a marketplace
/plugin marketplace add kingoliang/polyglot-engineering-claude-plugin

# Install the plugin
/plugin install polyglot-engineering@kingoliang
```

#### Method 2: Interactive Installation

```bash
# Open plugin browser
/plugin

# Select "Browse Plugins" and find polyglot-engineering
```

#### Method 3: Team Configuration

Add to your project's `.claude/settings.json`:

```json
{
  "marketplaces": ["kingoliang/polyglot-engineering-claude-plugin"],
  "plugins": ["polyglot-engineering@kingoliang"]
}
```

When team members trust the repository, the plugin installs automatically.

### Verify Installation

```bash
# Check available commands
/help

# View installed plugins
/plugin
```

### Usage

```bash
# Plan a new feature
/polyglot:plan Add user authentication with JWT

# Execute the plan
/polyglot:work

# Review code changes
/polyglot:review staged

# Generate documentation
/polyglot:docs all

# Triage review findings
/polyglot:triage
```

## Commands

| Command | Description |
|---------|-------------|
| `/polyglot:plan` | Convert feature descriptions into detailed implementation plans |
| `/polyglot:work` | Execute plans systematically with git worktree isolation |
| `/polyglot:review` | Multi-agent code review with language-specific analysis |
| `/polyglot:docs` | Generate comprehensive documentation from code |
| `/polyglot:triage` | Interactively resolve review findings |

## Agents

### Code Review Agents

| Agent | Purpose |
|-------|---------|
| `typescript-reviewer` | TypeScript/JavaScript best practices, React patterns |
| `python-reviewer` | Python patterns, Django/FastAPI/Flask review |
| `java-reviewer` | Java patterns, Spring Boot, Jakarta EE review |
| `architecture-strategist` | Design patterns, system architecture |
| `security-sentinel` | OWASP vulnerabilities, security best practices |
| `performance-oracle` | Performance bottlenecks, optimization |
| `code-simplicity-reviewer` | Clean code, SOLID, maintainability |

### Research Agents

| Agent | Purpose |
|-------|---------|
| `codebase-researcher` | Analyze and map existing codebases |
| `framework-researcher` | Research frameworks and libraries |

### Documentation Agents

| Agent | Purpose |
|-------|---------|
| `architecture-doc-generator` | System architecture documentation |
| `api-doc-generator` | API reference (OpenAPI/REST/GraphQL) |
| `uml-generator` | UML diagrams in Mermaid format |
| `readme-generator` | Project README files |
| `manual-generator` | User manuals and guides |

### Workflow Agents

| Agent | Purpose |
|-------|---------|
| `plan-executor` | Execute implementation plans |
| `review-coordinator` | Coordinate multi-agent reviews |

## Documentation Generation

Generate various documentation types:

```bash
# Generate all documentation
/polyglot:docs all

# Architecture documentation
/polyglot:docs architecture

# API reference
/polyglot:docs api

# UML diagrams
/polyglot:docs uml

# README
/polyglot:docs readme

# User manual
/polyglot:docs manual
```

### Output Structure

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

## Project Structure

```
polyglot-engineering/
├── .claude-plugin/
│   └── plugin.json          # Plugin configuration
├── agents/
│   ├── review/              # Code review agents
│   ├── research/            # Research agents
│   ├── docs/                # Documentation agents
│   └── workflow/            # Workflow agents
├── commands/                # Plugin commands
│   ├── plan.md
│   ├── work.md
│   ├── review.md
│   ├── docs.md
│   └── triage.md
├── skills/                  # Reusable skills
│   ├── docs-generator/
│   ├── code-analysis/
│   └── uml-generator/
├── templates/               # Document templates
│   ├── architecture/
│   ├── api/
│   ├── readme/
│   ├── manual/
│   └── prd/
├── CLAUDE.md               # Plugin instructions
├── CHANGELOG.md            # Version history
└── README.md               # This file
```

## Supported Languages

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

## Philosophy

This plugin follows the **Compounding Engineering** philosophy:

> "Each unit of engineering work should make subsequent units of work easier—not harder."

The plugin achieves this through:
1. **Planning**: Research-backed, detailed implementation plans
2. **Execution**: Systematic, quality-verified implementation
3. **Review**: Multi-agent, comprehensive code review
4. **Documentation**: Auto-generated, always up-to-date docs

## Contributing

Contributions are welcome! Please read our contributing guidelines before submitting PRs.

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Update CHANGELOG.md
5. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) for details.

## Acknowledgments

- Inspired by [compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin)
- Documentation structure influenced by [BMAD Method](https://github.com/bmad-code-org/BMAD-METHOD)

---

Made with [Claude Code](https://claude.ai)
