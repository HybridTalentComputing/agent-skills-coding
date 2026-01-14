# i18n-translation-skill

An Agent Skill for internationalization (i18n) and translation tasks.

**[English](./README.md)** | **[中文](./README.zh-CN.md)**

## Overview

This is an Agent Skill that extends Claude's capabilities for handling internationalization and translation workflows. It provides specialized tools and instructions for efficiently managing multi-language content, localization files, and translation processes.

## What is i18n-translation-skill?

The i18n-translation-skill teaches Claude **how to handle** internationalization and translation tasks through procedural knowledge. Unlike generic prompts, this Skill:

- Provides structured workflows for i18n file management
- Supports multiple translation file formats (JSON, YAML, etc.)
- Ensures consistency across translations
- Handles key matching and missing translations
- Integrates with existing translation workflows

## Getting Started

### Official Documentation
- [Agent Skills Overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) - Official Anthropic documentation
- [Official Skills Repository](https://github.com/anthropics/skills) - Reference implementations
- [Skills Explained](https://claude.com/blog/skills-explained) - How Skills compare to Prompts, Projects, MCP, and Subagents

### Installation

1. Clone this repository to your local skills directory
2. Ensure the skill is properly configured with metadata
3. Claude will automatically detect and load the skill when needed

## Features

### Translation File Formats
- **JSON**: Most common format for web applications
- **YAML**: Human-readable configuration format
- **Properties**: Java-style property files
- **Custom formats**: Extensible for project-specific needs

### Core Capabilities
- Extract translatable strings from source code
- Generate translation files for multiple languages
- Synchronize translation keys across language files
- Detect missing or outdated translations
- Merge translations from different sources
- Validate translation file syntax

### When to Use This Skill

> When you need to add, update, or manage internationalization content in your project, or work with translation files across multiple languages.

## Repository Structure

```
i18n-translation-skill/
├── README.md              # This file
├── README.zh-CN.md        # Chinese version
├── CLAUDE.md              # Guidance for Claude Code
├── LICENSE                # Apache License 2.0
```

## Usage Examples

### Example 1: Creating Translation Files

```json
// en.json
{
  "welcome": "Welcome to our application",
  "goodbye": "Goodbye!"
}

// zh-CN.json
{
  "welcome": "欢迎使用我们的应用",
  "goodbye": "再见！"
}
```

### Example 2: Extracting Strings

When given source code, the skill can identify translatable strings and create appropriate i18n entries.

### Example 3: Synchronizing Keys

The skill can ensure all language files have matching keys and identify missing translations.

## Best Practices

1. **Keep keys consistent**: Use the same key across all language files
2. **Use meaningful names**: Choose descriptive keys that reflect content context
3. **Organize by feature**: Group translations by application features/modules
4. **Handle plurals**: Use appropriate pluralization rules for each language
5. **Test with real content**: Verify translations work in actual UI context

## Contributing

Contributions are welcome! Areas for improvement:

- Add support for additional translation file formats
- Improve extraction accuracy for different programming languages
- Add more sophisticated pluralization handling
- Enhance validation and error reporting
- Support for translation memory systems
- Integration with translation APIs

When contributing:

1. Follow existing code style and patterns
2. Add tests for new functionality
3. Update documentation as needed
4. Ensure cross-platform compatibility

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](./LICENSE) file for details.
