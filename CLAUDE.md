# Polyglot Engineering Plugin

## Overview

This plugin implements a comprehensive engineering workflow for TypeScript, Python, and Java projects. It provides code review, planning, and documentation generation capabilities following the compounding engineering philosophy.

## Plugin Structure

```
polyglot-engineering/
├── .claude-plugin/
│   └── plugin.json          # Plugin configuration
├── agents/
│   ├── review/              # Code review agents
│   │   ├── typescript-reviewer.md
│   │   ├── python-reviewer.md
│   │   ├── java-reviewer.md
│   │   ├── architecture-strategist.md
│   │   ├── security-sentinel.md
│   │   ├── performance-oracle.md
│   │   └── code-simplicity-reviewer.md
│   ├── research/            # Research agents
│   │   ├── codebase-researcher.md
│   │   └── framework-researcher.md
│   ├── docs/                # Documentation agents
│   │   ├── architecture-doc-generator.md
│   │   ├── api-doc-generator.md
│   │   ├── uml-generator.md
│   │   ├── readme-generator.md
│   │   └── manual-generator.md
│   └── workflow/            # Workflow agents
│       ├── plan-executor.md
│       └── review-coordinator.md
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
└── templates/               # Document templates
    ├── architecture/
    ├── api/
    ├── readme/
    ├── manual/
    └── prd/
```

## Core Commands

### `/polyglot:plan`
Converts feature descriptions into detailed implementation plans with research and acceptance criteria.

### `/polyglot:work`
Executes plans systematically using isolated git worktrees.

### `/polyglot:review`
Performs multi-agent code reviews with language-specific and cross-cutting concerns.

### `/polyglot:docs`
Generates comprehensive documentation (architecture, API, UML, README, manuals).

### `/polyglot:triage`
Presents review findings for approval and prioritization.

## Version Control

When modifying this plugin:
1. Update version in `.claude-plugin/plugin.json`
2. Document changes in `CHANGELOG.md`
3. Verify README.md reflects current state

### Version Types
- **MAJOR**: Breaking changes, major reorganization
- **MINOR**: New agents, commands, or skills
- **PATCH**: Bug fixes, doc updates, minor improvements

## Supported Languages

- **TypeScript/JavaScript**: Full support for React, Node.js, Next.js, Express
- **Python**: Django, FastAPI, Flask, async patterns, type hints
- **Java**: Spring Boot, Jakarta EE, Maven/Gradle, design patterns
