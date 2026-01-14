# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the "i18n-translation-skill" repository - an Agent Skill for handling internationalization and translation tasks. This skill extends Claude's capabilities to efficiently manage multi-language content, localization files, and translation processes.

**Key References:**
- Agent skills documentation: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
- Official skills repository: https://github.com/anthropics/skills

## Repository Structure

This is a skill repository with:
- `README.md` - Main project documentation (English)
- `README.zh-CN.md` - Chinese version documentation
- `LICENSE` - Apache License 2.0
- No build system or dependencies (documentation-only)

## Skill Purpose

The i18n-translation-skill helps Claude:
1. Extract translatable strings from source code
2. Generate and manage translation files (JSON, YAML, etc.)
3. Synchronize translation keys across multiple languages
4. Detect missing or outdated translations
5. Validate translation file syntax

## Development

When working with this repository:
- This is a documentation/skill definition repository
- No build commands, test suites, or package management
- Changes should be made directly to documentation files
- Follow standard Git workflow for updates

## Skill Usage

Claude should use this skill when:
- Users need to add or update internationalization content
- Working with translation files across multiple languages
- Extracting strings for localization
- Synchronizing translation keys
- Validating translation file formats
