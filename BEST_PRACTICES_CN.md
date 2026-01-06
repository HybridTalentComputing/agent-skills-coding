# Agent Skills 最佳实践

本指南基于 Anthropic 官方文档和架构模式，概述了创建高效 Agent Skills 的最佳实践。

## 概述

Agent Skills 是基于文件系统的模块化能力，用于扩展 Claude 的功能。每个 Skill 将指令、元数据和可选资源（脚本、模板）打包，Claude 在相关场景下自动使用。

**核心原则：**
- Skills 教 Claude **如何做**某事（程序性知识）
- Skills 采用渐进式加载以优化 token 使用
- Skills 可在对话和项目间重复使用
- Skills 可组合以构建复杂工作流

## 1. 渐进式披露设计

Skills 使用三层加载架构。设计你的 Skill 时应充分利用这一特性：

```
Level 1: 元数据 (~100 tokens)
├── 启动时加载
├── 提供发现信息
└── 告诉 Claude 何时触发此 Skill

Level 2: 指令 (<5k tokens)
├── Skill 触发时加载
├── 包含核心程序性知识
└── Claude 的主要指导

Level 3: 资源（无限量，按需）
├── 仅在引用时加载
├── 脚本、参考文档、模板
└── 通过 bash 访问，不消耗上下文
```

### 最佳实践
不要把所有内容都放在 `SKILL.md` 中。将大型参考资料、示例和文档移到单独的文件中，只在需要时加载。

## 2. 编写有效的描述

YAML frontmatter 中的 `description` 字段对于发现至关重要。它必须同时告诉 Claude 这个 Skill **做什么**以及**何时使用**。

### 示例

```yaml
---
name: excel-data-analysis
description:
  使用 pandas 和 openpyxl 分析 Excel 电子表格。
  当用户提到 Excel、.xlsx 文件、电子表格，
  或需要从 Excel 文件进行数据分析/可视化时使用。
---
```

### 指南
- **具体明确**：提及具体的用例和关键词
- **包含触发条件**：列出 Claude 应激活此 Skill 的场景
- **保持聚焦**：在 1024 字符以内
- **像 Claude 一样思考**：什么信息能帮助识别何时使用此 Skill？

## 3. 选择正确的内容类型

每种内容类型都有不同的优势：

| 内容类型 | 最适合 | Token 消耗 | 加载时机 |
|--------------|----------|------------|-------------|
| **指令** | 工作流程、最佳实践、指导 | 低（5k 以内） | Skill 触发时 |
| **脚本** | 确定性操作、自动化 | 零（只计算输出） | 执行时 |
| **资源** | API 文档、数据模式、模板、示例 | 零（直到访问时） | 按需通过 bash |

### 决策框架

- **使用指令**用于需要推理的灵活指导
- **使用脚本**用于重复的确定性操作
- **使用资源**用于事实查找和参考资料

## 4. 构建你的 Skill 目录

像新员工入职指南一样组织你的 Skill：

```
your-skill/
├── SKILL.md              # 必需：主要指令
├── QUICKSTART.md         # 可选：快速参考
├── EXAMPLES.md           # 可选：使用示例
├── REFERENCE.md          # 可选：详细文档
├── TROUBLESHOOTING.md    # 可选：常见问题
└── scripts/              # 可选：可执行工具
    ├── validate.py
    └── transform.py
```

### 必需字段

每个 `SKILL.md` 必须包含：

```yaml
---
name: your-skill-name
description: 简要描述此 Skill 的功能以及何时使用它
---
```

### 字段要求

**name:**
- 最多 64 个字符
- 仅限小写字母、数字和连字符
- 不能包含："anthropic"、"claude" 或 XML 标签

**description:**
- 最多 1024 个字符
- 不能包含 XML 标签
- 必须非空

## 5. 编写风格指南

将 `SKILL.md` 视为团队新成员的入职指南。

### 应该做
- ✅ 提供清晰的、分步指令
- ✅ 包含具体示例
- ✅ 覆盖常见场景和边缘情况
- ✅ 引用其他文件以获取详细信息
- ✅ 使用代码块展示示例

### 不应该做
- ❌ 不要陈述显而易见的内容（Claude 已经知道如何编码）
- ❌ 不要编写没有具体上下文的通用内容
- ❌ 不要重复通用文档中的信息
- ❌ 不要写没有结构的大段文字

### 示例结构

```yaml
---
name: excel-data-analysis
description:
  使用 pandas 和 openpyxl 分析 Excel 电子表格。
  当用户提到 Excel、.xlsx 文件、电子表格、
  数据分析、图表、数据透视表或从 Excel 文件
  进行数据可视化时使用。支持读取、操作和导出。
---

# Excel 数据分析

## 快速开始
此 Skill 帮助你使用 Python 的 pandas 和 openpyxl 库处理 Excel 文件（.xlsx）。
它处理来自电子表格数据的分析、可视化和报告生成。

## 何时使用此 Skill
- 用户提到 Excel、.xlsx 或电子表格文件
- 用户需要表格数据的数据分析或可视化
- 用户请求图表、数据透视表或统计分析
- 用户希望从数据生成 Excel 报告

## 核心工作流程
1. 使用 pandas/openpyxl 加载 Excel 文件
2. 分析数据结构和内容
3. 执行请求的操作（过滤、转换、分析）
4. 根据需要生成可视化或报告
5. 如果请求则导出结果

## 示例
### 示例 1：基本数据分析
用户请求："分析 sales.xlsx 中的销售数据并显示趋势"

你的响应：
1. 加载文件：`pd.read_excel('sales.xlsx')`
2. 检查列和数据类型
3. 计算趋势和统计信息
4. 创建可视化
5. 用具体数据点呈现发现

### 示例 2：创建报告
用户请求："从 data.xlsx 生成月度汇总报告"

你的响应：
1. 加载和验证数据
2. 按月分组
3. 计算汇总统计
4. 创建包含多个工作表的格式化 Excel 输出
5. 保存报告文件

## 其他资源
- 参见 [EXAMPLES.md](EXAMPLES.md) 了解更多用例
- 参见 [REFERENCE.md](REFERENCE.md) 了解详细的 pandas/openpyxl API 文档
```

## 6. 何时使用 Skills vs. 其他构建块

### 使用 Skills 当
- 你发现自己跨多个对话重复输入同样的 prompt
- 你需要适用于多个项目的程序性知识
- 你想要组合多个能力构建工作流
- 你有组织工作流程或标准要执行

### 使用 Prompts 当
- 你提供一次性指令
- 提供即时上下文
- 进行对话式来回
- 在正式化之前测试想法

### 使用 Projects 当
- 你需要持久的背景知识
- 围绕特定 initiative 组织工作
- 为团队构建知识库

### 使用 MCP 当
- 你需要访问外部数据源（Google Drive、Slack、数据库）
- 连接业务工具（CRM、项目管理）
- 你有自定义系统要集成

### 使用 Subagents 当
- 你需要独立的任务执行
- 你想要限制工具权限
- 你在 Claude Code 中构建专门的工作流

**核心区别：**
- **MCP** 连接 Claude 到数据
- **Skills** 教 Claude 如何处理这些数据
- 结合使用：MCP 用于连接，Skills 用于程序性知识

## 7. 安全最佳实践

Skills 通过指令和代码为 Claude 提供新能力。遵循这些安全指南：

### 基本实践
- ✅ 仅使用来自可信来源的 Skills（由你或 Anthropic 创建）
- ✅ 审计所有文件：SKILL.md、脚本、图像、资源
- ✅ 审查异常模式（意外的网络调用、文件访问）
- ✅ 验证操作与 Skill 的声明目的匹配

### 高风险模式
- ⚠️ 从外部 URL 获取数据的 Skills
- ⚠️ 有意外网络调用的 Skills
- ⚠️ 访问敏感数据的脚本
- ⚠️ 与 Skill 描述不匹配的操作

### 将 Skills 视为软件
安装 Skill 就像安装软件。仅使用来自可信来源的 Skills，特别是在集成到具有敏感数据访问权限的生产系统时。

## 8. 环境约束

不同平台有不同的限制。相应地设计你的 Skill：

### Claude API
- ❌ 无网络访问
- ❌ 无运行时包安装
- ✅ 仅预装包可用

### Claude Code
- ✅ 完整网络访问
- ✅ 本地包安装（本地安装，避免全局）
- ✅ 所有系统功能

### Claude.ai
- ⚠️ 网络访问可变（取决于用户/管理员设置）
- ⚠️ 检查环境的文件创建设置

### 可移植性设计
如果你希望 Skill 跨平台工作，请为最 restrictive 的环境（Claude API）设计。

## 9. Skill 生命周期

### 创建 Skills
1. 从识别工作流程中重复的 prompts 开始
2. 设计 Skill 结构（SKILL.md + 支持文件）
3. 编写有效的元数据（name + description）
4. 创建渐进式披露结构
5. 使用 Claude 测试并迭代

### 测试 Skills
- 验证 Claude 在适当时机触发 Skill
- 检查指令清晰并被正确遵循
- 确保引用文件在需要时加载
- 测试脚本正确执行
- 验证 token 效率（你是否预先加载了太多内容？）

### 迭代 Skills
- 监控 Claude 何时未能适当使用 Skill
- 如果触发不一致，优化 description
- 为常见故障模式添加示例
- 如需要，将大型 Skills 拆分为多个专注的 Skills

## 10. 要避免的常见陷阱

### 1. SKILL.md 内容过载
**问题**：将所有内容放在一个文件中浪费 tokens

**解决方案**：使用渐进式披露。将参考材料移到单独文件。

### 2. 模糊的描述
**问题**：Claude 不知道何时触发你的 Skill

**解决方案**：在 description 中具体说明用例和关键词。

### 3. 重复造轮子
**问题**：编写 Claude 已经知道的内容

**解决方案**：专注于特定领域、组织或程序性知识，而非通用能力。

### 4. 忽略平台约束
**问题**：Skill 假设了在所有环境中都不存在的功能

**解决方案**：为你计划支持的最 restrictive 平台设计。

### 5. 缺少渐进式披露
**问题**：所有内容同时加载，浪费 tokens

**解决方案**：将内容结构化为多个按需加载的文件。

## 11. 创建有效 Skills 的检查清单

在最终确定你的 Skill 之前使用此检查清单：

- [ ] **描述**：清晰说明 Skill 的功能以及何时使用它
- [ ] **元数据**：遵循命名约定（无保留词、小写）
- [ ] **结构**：主要指令在 SKILL.md，参考资料在单独文件中
- [ ] **示例**：包含具体的使用示例
- [ ] **渐进式加载**：大型参考资料分离
- [ ] **平台兼容性**：在目标环境约束内工作
- [ ] **安全性**：审计潜在风险，特别是外部调用
- [ ] **测试**：验证 Claude 正确触发和使用它
- [ ] **文档**：为 Claude 和人类维护者提供清晰的指令

## 资源

- [官方 Agent Skills 文档](https://console.anthropic.com/docs/en/agents-and-tools/agent-skills/overview)
- [Agent Skills 工程博客](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
- [官方 Skills 仓库](https://github.com/anthropics/skills)
- [Skills 说明：如何与 Prompts、Projects、MCP 和 Subagents 比较](https://claude.com/blog/skills-explained)

## 总结

**黄金法则**：如果你发现自己跨多个对话重复输入同样的 prompt，就是时候创建 Skill 了。

有效的 Skills：
1. 渐进式加载（元数据 → 指令 → 资源）
2. 具有清晰、具体的描述
3. 分离关注点（指令 vs. 脚本 vs. 资源）
4. 在平台约束内工作
5. 遵循安全最佳实践
6. 像入职指南：清晰、结构化和可操作

将 Skills 视为教授 Claude 任何 agent 都可以应用的专业知识，而不仅仅是自定义一个特定的交互。
