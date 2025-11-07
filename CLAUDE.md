# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a documentation and template repository for Claude Code agents and subagents (German: "Unsere fleissigsten Mitarbeitenden" / "Our most diligent employees"). It serves as both a learning resource and a collection of reusable agent definitions for common development workflows.

## Repository Structure

- **Agent Definition Files** (`.md` files in root): These are agent/subagent configuration files with frontmatter defining specialized AI assistants:
  - `accessibility-reporter.md`: Lighthouse-based accessibility testing and report generation
  - `accessibility-fixer.md`: WCAG 2.2 Level AA compliance fixes based on accessibility reports
  - `translation-validator.md`: Post-commit i18n/l10n validation and translation completion

- **Documentation Files** (German):
  - `README.md`: Main repository overview with Claude Code introduction and agent creation workflows
  - `CLAUDE_CODE_UEBERBLICK.md`: Quick start guide for Claude Code
  - `AGENTS_UND_SUBAGENTS_ANLEITUNG.md`: Detailed guide for creating and managing agents/subagents

- **Resources**:
  - `/accessibility-reports/`: Directory where accessibility reports are saved (format: `report-YYYY-MM-DD-HH:mm:ss.md`)

## Agent Architecture Pattern

Agent definition files follow this structure:

```markdown
---
name: agent-name
description: When to use this agent with examples
model: sonnet
color: green
---

[System prompt defining the agent's behavior, expertise, and workflow]
```

**Key sections in agent system prompts:**
1. Expertise statement and role definition
2. Step-by-step workflow (numbered list)
3. Standards and quality requirements
4. Output format and file locations
5. Error handling and edge cases

## Agent Storage Locations

- **Project agents**: `.claude/agents/` (can be version controlled, shared with team)
- **User agents**: `~/.claude/agents/` (local only, cross-project)
- Project agents take precedence over user agents when names conflict

**Note**: This repository currently stores agent definitions as documentation files in the root directory rather than in `.claude/agents/`. To use these agents, either:
- Copy them to `.claude/agents/` in your project
- Use `/agents` command to import them
- Reference them when creating new agents

## Common Workflows

### Working with Accessibility Agents

1. **Running accessibility audit:**
   ```
   Use the accessibility-reporter agent to audit [URL]
   ```
   - Installs dependencies: `chrome-launcher`, `lighthouse`, `puppeteer` (as dev dependencies)
   - Runs Lighthouse in Chromium
   - Saves report to `/accessibility-reports/report-YYYY-MM-DD-HH:mm:ss.md`

2. **Fixing accessibility issues:**
   ```
   Use the accessibility-fixer agent to fix WCAG violations from the latest report
   ```
   - Reads latest report from `/accessibility-reports/`
   - Prioritizes: Level A → Level AA → High-impact issues → Semantic HTML → Forms
   - Modifies existing files (never creates unnecessary new files)
   - Focuses on WCAG 2.2 Level AA compliance

### Working with Translation Validation

After committing changes with user-facing text:
```
Use the translation-validator agent to check for missing translations
```
- Analyzes changed files in recent commit
- Identifies hardcoded strings and missing translation keys
- Auto-generates translations for all supported languages
- Updates translation files maintaining proper formatting

## Agent Design Best Practices

When creating or modifying agents:

1. **Clear Scope**: One primary task with defined outputs (markdown reports, JSON, code fixes)
2. **Deterministic Outputs**: Specify exact formats, file paths, naming conventions
3. **Minimal Tool Access**: Grant only necessary tools
4. **Quality Gates**: Include verification steps, error handling, edge case management
5. **No Unnecessary Documentation**: Agents should avoid creating gratuitous `.md` files; focus on actionable outputs

## Language Context

Documentation is primarily in German. The project serves the Digital Democracy Hub and uses German terminology:
- "Subagents" = Spezialisierte Assistenten
- "Agents" = KI-Assistenten
- Target audience: German-speaking development teams

## Important Notes

- This is a template/documentation repository, not an application codebase
- No build/test/lint commands are needed
- Focus is on agent definitions and their documentation
- When modifying agents, ensure frontmatter format remains valid
- Agent descriptions should include specific examples of when to use them
