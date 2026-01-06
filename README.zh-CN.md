# agent-skills-coding

用于 vibe coding 的开源 agent skills。

**[English](./README.md)** | **[中文](./README.zh-CN.md)**

## 概述

本仓库作为开源 agent skills 的集合和参考点，用于扩展 Claude 的能力。Agent Skills 是基于文件系统的模块化能力，将指令、元数据和资源打包，帮助 Claude 高效执行专门任务。

## 什么是 Agent Skills？

Agent Skills 通过程序性知识教授 Claude **如何做**特定任务。与 prompts（对话级指令）不同，Skills：

- 采用渐进式加载以优化 token 使用
- 可在对话和项目间重复使用
- 可组合以构建复杂工作流
- 包含可执行代码和参考资料

**核心区别**：Agent Skills（程序性知识）vs. MCP（数据连接）。Skills 教 Claude 如何处理数据；MCP 连接 Claude 到数据源。

## 快速开始

### 官方文档
- [Agent Skills 概述](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) - Anthropic 官方文档
- [官方 Skills 仓库](https://github.com/anthropics/skills) - 参考实现
- [Skills 详解](https://claude.com/blog/skills-explained) - Skills 与 Prompts、Projects、MCP 和 Subagents 的比较

### 最佳实践

📖 **[English Version](./BEST_PRACTICES.md)** | 📖 **[中文版](./BEST_PRACTICES_CN.md)**

创建有效 Agent Skills 的必读内容：
- 渐进式披露设计（3 层加载架构）
- 编写有效的描述和元数据
- 构建你的 Skill 目录
- 安全考虑
- 平台特定约束
- 要避免的常见陷阱

## 仓库结构

```
agent-skills-coding/
├── README.md              # 英文版说明
├── README.zh-CN.md        # 中文版说明（本文件）
├── CLAUDE.md              # Claude Code 工作指南
├── BEST_PRACTICES.md      # 最佳实践指南（英文）
├── BEST_PRACTICES_CN.md   # 最佳实践指南（中文）
└── LICENSE                # Apache License 2.0
```

## 快速参考

### 何时创建 Skill
> 如果你发现自己跨多个对话重复输入同样的 prompt，就是时候创建 Skill 了。

### Skill 结构
```yaml
---
name: your-skill-name
description: 此 Skill 的功能以及何时使用它
---

# Your Skill Name

## 快速开始
[简要概述]

## 何时使用此 Skill
[触发条件]

## 核心工作流程
[分步流程]

## 示例
[具体用例]
```

### 核心原则
1. **渐进式加载**：元数据 → 指令 → 资源
2. **清晰描述**：告诉 Claude 做什么以及何时使用它
3. **分离关注点**：指令 vs. 脚本 vs. 资源
4. **安全第一**：仅使用来自可信来源的 Skills

## 贡献

欢迎贡献！添加新的 skills 或文档时：

1. 遵循[最佳实践指南](./BEST_PRACTICES_CN.md)
2. 确保 Skill 包含正确的元数据（name、description）
3. 提供清晰的示例和用例
4. 如适用，在不同平台上测试
5. 记录任何平台特定的约束

## 许可证

本项目采用 Apache License 2.0 许可 - 详见 [LICENSE](./LICENSE) 文件。
