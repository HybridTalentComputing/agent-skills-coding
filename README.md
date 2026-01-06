# agent-skills-coding

Open source agent skills for vibe coding.

**[English](./README.md)** | **[中文](./README.zh-CN.md)**

## Overview

This repository serves as a collection and reference point for open source agent skills that extend Claude's capabilities. Agent Skills are filesystem-based modular capabilities that package instructions, metadata, and resources to help Claude perform specialized tasks efficiently.

## What are Agent Skills?

Agent Skills teach Claude **how to do** specific tasks through procedural knowledge. Unlike prompts (conversation-level instructions), Skills:

- Load progressively to optimize token usage
- Can be reused across conversations and projects
- Combine to build complex workflows
- Include executable code and reference materials

**Key Distinction**: Agent Skills (procedural knowledge) vs. MCP (data connectivity). Skills teach Claude what to do with data; MCP connects Claude to data sources.

## Getting Started

### Official Documentation
- [Agent Skills Overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) - Official Anthropic documentation
- [Official Skills Repository](https://github.com/anthropics/skills) - Reference implementations
- [Skills Explained](https://claude.com/blog/skills-explained) - How Skills compare to Prompts, Projects, MCP, and Subagents

### Best Practices

📖 **[English Version](./BEST_PRACTICES.md)** | 📖 **[中文版](./BEST_PRACTICES_CN.md)**

Essential reading for creating effective Agent Skills:
- Progressive disclosure design (3-level loading architecture)
- Writing effective descriptions and metadata
- Structuring your Skill directory
- Security considerations
- Platform-specific constraints
- Common pitfalls to avoid

## Repository Structure

```
agent-skills-coding/
├── README.md              # This file
├── CLAUDE.md              # Guidance for Claude Code
├── BEST_PRACTICES.md      # Best practices guide (English)
├── BEST_PRACTICES_CN.md   # 最佳实践指南 (中文)
└── LICENSE                # Apache License 2.0
```

## Quick Reference

### When to Create a Skill
> If you find yourself typing the same prompt repeatedly across multiple conversations, it's time to create a Skill.

### Skill Structure
```yaml
---
name: your-skill-name
description: What this Skill does and when to use it
---

# Your Skill Name

## Quick Start
[Brief overview]

## When to Use This Skill
[Trigger criteria]

## Core Workflow
[Step-by-step process]

## Examples
[Concrete use cases]
```

### Key Principles
1. **Progressive Loading**: Metadata → Instructions → Resources
2. **Clear Descriptions**: Tell Claude what to do AND when to use it
3. **Separate Concerns**: Instructions vs. Scripts vs. Resources
4. **Security First**: Only use Skills from trusted sources

## Contributing

Contributions are welcome! When adding new skills or documentation:

1. Follow the [Best Practices](./BEST_PRACTICES.md) guide
2. Ensure your Skill includes proper metadata (name, description)
3. Provide clear examples and use cases
4. Test across different platforms if applicable
5. Document any platform-specific constraints

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](./LICENSE) file for details.
