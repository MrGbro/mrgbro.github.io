---
title: 从 Prompt 到 Context 再到 Harness：AI 工程的三次进化
date: 2026-03-24 23:00:00
categories: 
  - LLM
tags: 
  - Agent
  - LLM
cover: /images/api-integration-architecture-cover.webp
description: 本文以马为喻，介绍 AI 工程实践三大核心概念：提示工程聚焦优化与 AI 的沟通方式，上下文工程侧重为 AI 精准配置全量信息，驾驭工程则着眼设计约束 AI 的工作环境。三者随 AI 能力演进层层递进，从聊天时代到 Agent 时代，是 AI 开发从简单交互到复杂自主任务的关键工程进化，也为 AI 开发者提供了清晰的学习与实践路径。
keywords: [Agent, LLM]
toc: true
toc_number: true
comments: true
copyright: true
---
如果把 AI 比作一匹马，那么：

- **Prompt Engineering** 是学会怎么跟这匹马说话——"向左转"、"跑快点"
- **Context Engineering** 是给马看路线图、地形资料，让它知道要去哪、路上有什么
- **Harness Engineering** 是给马配上马鞍、缰绳和护栏，确保它不管怎么跑都不会翻车

这三个概念，代表了 AI 工程实践从 2022 年到 2026 年的三次重要进化。理解它们的区别和联系，能帮你看清 AI 开发这个领域到底在往哪走。

---

## 从聊天到自主行动：为什么"写好提示"不够了

2023 年，你和 ChatGPT 的典型交互方式是这样的：

> "请帮我写一封邮件，语气正式，内容是通知客户项目延期。"

那时候，**提示写得好不好**直接决定了 AI 回复的质量。所以大家都在研究怎么写更好的提示——这就是 Prompt Engineering。

但到了 2025 年，事情变了。AI 不再只是"聊天"工具。人们开始用 AI 做更复杂的事：自动检索数据、调用 API、分析文档、写代码。这时候，光靠一条写得好的提示远远不够了——你还需要精心安排 AI 能看到的所有信息。这就催生了 Context Engineering。

再到 2026 年，AI Agent 开始自主执行长链条任务：读代码、改代码、跑测试、提交 PR。这时候问题变了——不是"给 AI 什么信息"的问题，而是"怎么确保 AI 在自主干活时不搞砸"。这就是 Harness Engineering 要解决的事。

三个概念，对应 AI 能力的三个阶段。下面逐个拆解。

---

## Prompt Engineering：怎么跟 AI 说话

### 是什么

Prompt Engineering（提示工程）是最早、也最广为人知的 AI 工程概念。它的核心是：**通过优化你发给 AI 的提示文本，来获得更好的输出**。

简单说，就是研究"怎么跟 AI 说话才能让它表现更好"。

### 核心技术

这些你可能已经见过：

- **Zero-shot**：直接提问，不给任何示例。"翻译这段话成英文。"
- **Few-shot**：给几个示例，让 AI 模仿格式。"以下是几个翻译的例子……请按照同样格式翻译。"
- **Chain-of-Thought (CoT)**：要求 AI 一步步推理。"请一步步分析这个问题，然后给出答案。"
- **角色扮演**：给 AI 一个身份。"你是一名资深 Python 工程师。"

### 一句话总结

Prompt Engineering 的核心是：**调整你说话的方式，来影响 AI 的表现**。

### 局限

当你只是跟 AI 聊天、问问题、写文案时，Prompt Engineering 很好用。但当系统变得复杂——AI 需要读取数据库、调用工具、处理长文档——光靠"写好一段话"就不够了。

你需要管理的不只是一条提示，而是 AI 能看到的**全部信息**。

---

## Context Engineering：给 AI 什么信息

### 是什么

Context Engineering（上下文工程）是 2025 年开始流行的概念。它的关注点从"一条提示"扩展到了"整个上下文窗口"。

Andrej Karpathy（OpenAI 联合创始人之一）给了一个被广泛引用的定义：

> "Context engineering is the delicate art and science of filling the context window with just the right information for the next step."
>
> （上下文工程是一门精细的艺术和科学——用恰到好处的信息填充上下文窗口，为下一步行动做准备。）

Shopify CEO Tobi Lutke 的定义更直白：

> "The art of providing all the context for the task to be plausibly solvable by the LLM."
>
> （为任务提供所有必要上下文，让 LLM 有可能解决它的艺术。）

### 核心关注

Context Engineering 管理的不只是你的提示文本，而是 AI 上下文窗口里的**所有内容**：

- **系统提示**（System Prompt）：给 AI 的基础指令和角色设定
- **检索到的文档**（Retrieved Documents）：通过 RAG 从知识库拉取的相关内容
- **工具定义**（Tool Definitions）：AI 可以调用哪些工具，参数是什么
- **对话历史**（Conversation History）：之前的交互记录
- **状态信息**（State）：当前任务的中间状态

LangChain 团队总结了四大策略：

| 策略 | 含义 | 举例 |
|------|------|------|
| **Write（写入）** | 给 AI 创建记忆和草稿区 | scratchpad、记忆存储 |
| **Select（选择）** | 从大量信息中挑选相关内容 | RAG 检索、数据筛选 |
| **Compress（压缩）** | 在有限窗口中塞入更多有效信息 | 摘要、裁剪 |
| **Isolate（隔离）** | 让不同信息互不干扰 | 多 Agent 分工、状态分离 |

### 和 Prompt Engineering 的区别

打个比方：

- Prompt Engineering 像是精心准备一个**面试问题**
- Context Engineering 像是为面试官准备一整套**面试资料包**——不只有问题，还有候选人简历、岗位需求、团队背景、薪资范围

Context Engineering 是 Prompt Engineering 的自然延伸：当 AI 系统变复杂了，你需要管理的信息远不止一条提示。

Simon Willison（知名开发者和技术博主）说得很到位：Prompt Engineering 这个词容易让人觉得就是"在聊天框里打字"，但 Context Engineering 更好地描述了工业级 AI 应用的真正复杂度。

### 一句话总结

Context Engineering 的核心是：**精心管理 AI 能看到的全部信息**。

---

## Harness Engineering：让 AI 在什么环境里工作

### 是什么

Harness Engineering（驾驭工程）是最新的概念，由 HashiCorp 联合创始人 **Mitchell Hashimoto** 于 **2026 年 2 月**提出。

它的核心思路是：**不要只优化你给 AI 的信息，要设计 AI 工作的整个环境**。

如果说 Context Engineering 解决了"给 AI 什么信息"，Harness Engineering 解决的是"让 AI 在什么环境中工作"。

"Harness"这个词，原意是马具——马鞍、缰绳、嚼子。它的作用不是告诉马该怎么跑，而是从物理上确保马不会偏离道路。同样，Harness Engineering 不是靠"说"来约束 AI，而是靠**架构和环境**来约束 AI。

### 为什么会出现

这个概念的出现和 AI Agent 的兴起直接相关。

当 AI 只是回答问题时，你只需要管好提示和上下文。但当 AI Agent 开始自主写代码、跑测试、修 bug、提交代码——它在一个真实的环境中工作，会影响真实的系统。这时候，你需要的不是更好的提示，而是更好的**防护栏**。

举个例子：一个 AI Agent 在帮你写代码时，因为不了解项目规范而用了错误的代码风格。

- **Prompt Engineering 的做法**：在提示里写"请使用 TypeScript 而非 JavaScript"
- **Context Engineering 的做法**：把项目的编码规范文档放进上下文窗口
- **Harness Engineering 的做法**：配置 ESLint + TypeScript 编译器，让 Agent 写了错误格式的代码时自动报错，Agent 根据报错自动修正

看出区别了吗？Prompt 是"口头交代"，Context 是"给参考资料"，Harness 是"设置围栏让错误根本不可能通过"。

### 核心要素

Harness Engineering 有四个关键组成部分：

**1. 渐进式文档（如 AGENTS.md）**

这是一种新兴实践——在代码仓库中放置专门给 AI Agent 阅读的文档。比如创建一个 `AGENTS.md` 文件，写明项目的技术栈、代码规范、目录结构、常见陷阱等。Agent 在工作时会读取这个文件，就像新员工入职时读员工手册一样。

关键在于"渐进式"：每当 Agent 犯一个错误，你就把这个错误的教训写进文档，确保**同样的错误不会再犯第二次**。

**2. 架构约束**

用代码级别的"硬约束"替代提示级别的"软约束"：

- Linter（代码检查器）：自动检查代码风格和规范
- 类型检查：确保类型安全
- 测试框架：验证代码功能正确
- CI/CD 管道：自动化构建和部署流程

这些工具对 Agent 产出的代码做自动化验证。通过验证的代码才算合格，没通过的 Agent 会看到错误信息并自动修正。

**3. 熵管理（清理混乱）**

AI Agent 运行时间越长，产生的"混乱"就越多——多余的临时文件、前后不一致的状态、冗余重复的代码。就像房间住久了会变乱一样，Agent 的工作空间也需要定期"打扫"。Harness Engineering 包含自动化的清理机制，定期整理 Agent 产生的副作用，保持工作环境的整洁。

**4. 反馈循环**

Agent 的每次执行结果都会被收集和分析。成功的模式被强化，失败的模式被记录并转化为新的约束。这让整个系统随着使用不断进化。

### 实际案例

OpenAI 的 Codex 团队在一篇文章中分享了他们的经验：通过持续优化 harness（Agent 的运行环境和约束），而非仅仅优化模型本身，他们显著提升了 Agent 自主完成编程任务的成功率。他们的核心发现是——**给 Agent 更好的工作环境，比给 Agent 更好的模型更有效**。

### 一句话总结

Harness Engineering 的核心是：**设计让 AI 不可能犯错的工作环境**。

---

## 三者对比：一张表看清区别和联系

| 维度 | Prompt Engineering | Context Engineering | Harness Engineering |
|------|-------------------|--------------------|--------------------|
| 一句话定义 | 怎么跟 AI 说话 | 给 AI 什么信息 | 让 AI 在什么环境里工作 |
| 优化对象 | 提示文本 | 上下文窗口 | 整个运行环境 |
| 约束方式 | 文字指令（"软约束"） | 信息编排 | 架构和工具链（"硬约束"） |
| 典型场景 | ChatGPT 对话 | RAG 应用、复杂对话系统 | AI Agent 自主执行 |
| 适用时代 | LLM 聊天时代 (2022-2023) | LLM 应用时代 (2024-2025) | AI Agent 时代 (2026-) |
| 关键人物 | 社区共同实践 | Andrej Karpathy, Tobi Lutke | Mitchell Hashimoto |
| 核心技术 | Few-shot, CoT, 角色扮演 | RAG, 动态检索, 压缩, 隔离 | AGENTS.md, Linter, CI/CD, 反馈循环 |

### 包含关系

三者不是互相替代，而是**层层包含**：

```
┌──────────────────────────────────────────┐
│  Harness Engineering                     │
│  （运行环境：工具链、约束、反馈循环）     │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │  Context Engineering             │    │
│  │  （上下文窗口：RAG、状态、工具） │    │
│  │                                  │    │
│  │  ┌──────────────────────────┐    │    │
│  │  │  Prompt Engineering      │    │    │
│  │  │  （提示文本：指令、格式）│    │    │
│  │  └──────────────────────────┘    │    │
│  └──────────────────────────────────┘    │
└──────────────────────────────────────────┘
```

你仍然需要写好提示（Prompt），也仍然需要编排好上下文（Context）。但在 Agent 时代，这些只是 Harness 的一部分。

---

## 它们不是替代，而是层层递进

三个概念的演进有一条清晰的逻辑线：

**AI 能做的事越多，需要的工程配套就越复杂。**

- 当 AI 只是聊天机器人时，优化提示就够了
- 当 AI 需要处理复杂信息时，需要管理整个上下文
- 当 AI 开始自主行动时，需要设计整个工作环境

打个比方：

- **Prompt Engineering** 像是给新员工交代一项任务时说的话——"请把这份报告写好，注意格式"
- **Context Engineering** 像是给新员工准备的入职资料——需求文档、历史资料、参考案例、公司规范
- **Harness Engineering** 像是公司的工作环境和制度——代码审查流程、自动化测试、CI/CD 管道、编码规范检查器

说得再好不如流程靠谱，给再多资料不如环境自带纠错。三者共同作用，才能让 AI 在复杂场景下可靠地工作。

在实际的 AI 应用开发中，三者通常是共存的：
- 你写一个好的 system prompt（Prompt Engineering）
- 你通过 RAG 检索相关文档、管理对话历史（Context Engineering）
- 你设置代码检查、自动化测试、AGENTS.md 文档（Harness Engineering）

它们是同一个系统的不同层次，不是二选一的关系。

---

## 对于初学者意味着什么

如果你刚进入 AI 开发领域，不需要一步到位。三个概念对应不同的学习阶段：

**阶段一：学会跟 AI 对话（Prompt Engineering）**

- 学习基本的提示技巧
- 理解 few-shot、CoT 等方法
- 这是最基础的技能，任何 AI 应用开发都需要
- 资源丰富，入门门槛低

**阶段二：学会为 AI 准备信息（Context Engineering）**

- 学习 RAG（检索增强生成）
- 理解如何管理上下文窗口
- 学习动态信息检索和组织
- 适合你开始构建真实 AI 应用的阶段

**阶段三：学会为 AI 设计工作环境（Harness Engineering）**

- 学习如何为 AI Agent 设计约束和反馈机制
- 理解 AGENTS.md 等新实践
- 学习用工具链（linter、测试、CI/CD）来约束 Agent
- 适合你开始构建 AI Agent 系统的阶段

不用着急跳到最新的概念。Prompt Engineering 仍然是基础中的基础，掌握好它再往上走，每一步都不会浪费。

---

## 小结

| 概念 | 核心问题 | 时代背景 |
|------|---------|---------|
| Prompt Engineering | 怎么跟 AI 说话 | LLM 聊天时代 |
| Context Engineering | 给 AI 什么信息 | LLM 应用时代 |
| Harness Engineering | 让 AI 在什么环境里工作 | AI Agent 时代 |

AI 的能力在不断增强，围绕 AI 的工程实践也在不断演进。从优化一条提示，到编排整个上下文，再到设计整个工作环境——这条路还在继续。

对于开发者来说，真正重要的不是记住每个术语的定义，而是理解背后的思路：**AI 越自主，你需要管理的东西就越不是"你说什么"，而是"它在什么环境中工作"**。

---

**参考资料**

1. Andrej Karpathy, Twitter/X post on context engineering, June 2025
2. Tobi Lutke (Shopify CEO), context engineering definition, 2025
3. Mitchell Hashimoto, "Harness Engineering" blog post, February 2026
4. Martin Fowler, "Harness Engineering", martinfowler.com
5. OpenAI, "Harness engineering: leveraging Codex in an agent-first world", openai.com
6. LangChain Blog, "Context Engineering for Agents", blog.langchain.com
7. Simon Willison, "Context Engineering", simonwillison.net, June 2025
