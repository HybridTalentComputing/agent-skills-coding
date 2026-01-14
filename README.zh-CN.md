# i18n-translation-skill

用于处理国际化（i18n）和翻译任务的 Agent Skill。

**[English](./README.md)** | **[中文](./README.zh-CN.md)**

## 概述

这是一个扩展 Claude 国际化和翻译工作流能力的 Agent Skill。它提供了专业的工具和指令，用于高效管理多语言内容、本地化文件和翻译流程。

## 什么是 i18n-translation-skill？

i18n-translation-skill 通过程序性知识教授 Claude **如何处理**国际化和翻译任务。与通用提示不同，这个 Skill：

- 提供结构化的 i18n 文件管理工作流
- 支持多种翻译文件格式（JSON、YAML 等）
- 确保翻译的一致性
- 处理键值匹配和缺失翻译
- 与现有翻译工作流集成

## 快速开始

### 官方文档
- [Agent Skills 概述](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) - Anthropic 官方文档
- [官方 Skills 仓库](https://github.com/anthropics/skills) - 参考实现
- [Skills 详解](https://claude.com/blog/skills-explained) - Skills 与 Prompts、Projects、MCP 和 Subagents 的比较

### 安装

1. 将此仓库克隆到本地技能目录
2. 确保技能配置了正确的元数据
3. Claude 会在需要时自动检测并加载该技能

## 功能特性

### 翻译文件格式
- **JSON**: Web 应用最常用的格式
- **YAML**: 人类可读的配置格式
- **Properties**: Java 风格的属性文件
- **自定义格式**: 可扩展以支持项目特定需求

### 核心能力
- 从源代码中提取可翻译字符串
- 为多种语言生成翻译文件
- 同步不同语言文件间的翻译键
- 检测缺失或过时的翻译
- 合并来自不同来源的翻译
- 验证翻译文件语法

### 何时使用此技能

> 当你需要在项目中添加、更新或管理国际化内容，或处理多种语言的翻译文件时。

## 仓库结构

```
i18n-translation-skill/
├── README.md              # 英文版说明
├── README.zh-CN.md        # 中文版说明（本文件）
├── CLAUDE.md              # Claude Code 工作指南
└── LICENSE                # Apache License 2.0
```

## 使用示例

### 示例 1：创建翻译文件

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

### 示例 2：提取字符串

给定源代码时，该技能可以识别可翻译字符串并创建相应的 i18n 条目。

### 示例 3：同步键值

该技能可以确保所有语言文件具有匹配的键，并识别缺失的翻译。

## 最佳实践

1. **保持键值一致**：在所有语言文件中使用相同的键
2. **使用有意义的名称**：选择能反映内容上下文的描述性键
3. **按功能组织**：按应用功能/模块分组翻译
4. **处理复数**：为每种语言使用适当的复数规则
5. **使用真实内容测试**：在实际 UI 上下文中验证翻译

## 贡献

欢迎贡献！可以改进的领域：

- 添加对更多翻译文件格式的支持
- 提高对不同编程语言的提取准确性
- 添加更复杂的复数处理
- 增强验证和错误报告
- 支持翻译记忆系统
- 与翻译 API 集成

贡献时请：

1. 遵循现有代码风格和模式
2. 为新功能添加测试
3. 根据需要更新文档
4. 确保跨平台兼容性

## 许可证

本项目采用 Apache License 2.0 许可 - 详见 [LICENSE](./LICENSE) 文件。
