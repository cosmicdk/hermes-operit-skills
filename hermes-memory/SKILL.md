---
name: hermes-memory
description: |-
  基于 Hermes Agent 三层记忆架构的增强记忆管理。
  MEMORY.md (项目规律/偏好) + USER.md (用户画像) + 会话历史检索。
  对标 Hermes 的内置记忆系统 + hermes memory search 命令。
  触发: 用户说"记住这个"、"搜索记忆"、"/memory"、"我之前说过"、
  "回顾一下"、"上次我们怎么做的"、"翻一下聊天记录"、
  以及任何涉及跨会话知识检索/持久化记忆的场景。
metadata:
  inspired_by: Hermes Agent Memory System (Nous Research)
  version: "1.0.0"
  argument-hint: "[search|save|show|clean] <内容>"
---

# Hermes Memory — 三层增强记忆

> *"记忆不是存盘，是理解你。"* — Hermes Agent 设计哲学

---

## 设计对标

Hermes Agent 的三层记忆架构 → Operit 实现：

```
Hermes Agent                    Operit
─────────────────────────────────────────────────
MEMORY.md (2,200字符)    →    本 Skill memory-bank.md
  Agent 自动提炼的项目笔记        项目规律、环境偏好、工作流

USER.md (1,375字符)      →    本 Skill user-profile.md
  Agent 自动构建的用户画像        角色、技术栈、沟通偏好

SQLite + FTS5 全文检索   →    Operit query_memory 系统
  跨会话历史搜索                 原生记忆检索

Honcho (可选)            →    Operit 外部记忆 Provider
  AI 原生用户建模                按需扩展
```

---

## 核心理念

Hermes 和其他 Agent 最本质的区别：**记忆是 Agent 自己维护的，
不是用户手动告诉它记什么。**

> "2,200 字符的上限看起来很小，但这个限制反而迫使 Agent
> 只保留最重要的信息——相当于一种自动的信息压缩机制。"
> — Hermes 官方文档

---

## 三层记忆说明

### 第一层：短期记忆（会话上下文）
- **范围**：当前会话的所有对话
- **生命周期**：会话结束后清空（但会被提炼到第二层）
- **用途**：当前任务的连贯执行

### 第二层：中期记忆（memory-bank.md + user-profile.md）
- **范围**：跨会话的持久化笔记
- **谁维护**：AI 自主决定存什么、何时合并、何时清理
- **容量**：每个文件约 2,000-3,000 字符（借鉴 Hermes 的容量限制）
- **用途**：下次会话自动注入，无需用户重复解释

### 第三层：长期记忆（Operit query_memory 系统）
- **范围**：所有历史会话全文
- **用途**：精确回溯几周前的对话细节

---

## 命令

在对话中使用：

| 命令 | 作用 |
|---|---|
| `/memory save <内容>` | 手动记录一条到 memory-bank |
| `/memory search <关键词>` | 搜索所有记忆（当前+历史） |
| `/memory show` | 显示 memory-bank + user-profile 内容 |
| `/memory show user` | 只显示 AI 对你的画像 |
| `/memory show project` | 只显示项目记忆 |
| `/memory clean` | 清理冗余记忆（合并重复项） |
| `/memory forget <关键词>` | 删除特定记忆 |

---

## 自动记忆沉淀规则

本 Skill 加载后，AI 在以下时机**主动检查并更新记忆**：

### 触发条件 1：会话自然结束
用户说"好的"、"谢谢"、"就这样"等收尾语时：
- 扫描本次会话的关键决策
- 提取新的用户偏好
- 更新 `memory-bank.md` 和 `user-profile.md`

### 触发条件 2：用户纠正 AI
用户说"不对"、"不是这样"、"应该是..."时：
- 记录纠正后的正确做法
- 标注旧做法为"已废弃"

### 触发条件 3：完成复杂任务（5+ 步骤）
- 提炼可复用的流程步骤
- 记录踩过的坑和解决方案

### 触发条件 4：用户明确说"记住"
- 立即写入记忆，不做延迟

---

## 记忆压缩策略

借鉴 Hermes 的有限容量设计：

1. **容量上限**：每个 memory 文件 ~2,500 字符
2. **达到上限时**：
   - 合并重复/相似条目
   - 删除已过时的信息
   - 保留最近 30 天内使用过的信息
3. **压缩原则**：
   - 保留：用户偏好、项目配置、关键决策
   - 压缩：一次性操作记录、已解决的临时问题
   - 删除：明确废弃的做法、过期环境信息

---

## 与 Hermes 原生记忆的区别

| 维度 | Hermes Agent | Operit hermes-memory |
|---|---|---|
| 存储后端 | SQLite + 文件 | query_memory + Markdown |
| 容量限制 | 硬限制 2,200 + 1,375 字符 | 软限制 ~2,500 字符 |
| 自动提炼 | 原生内置 | 本 Skill 规则驱动 |
| 检索方式 | FTS5 + hermes memory search | query_memory 语义搜索 |
| Honcho 集成 | 可选 | Operit 外部 Provider |

---

## 搭配使用

- `/hermes-soul` — 人格配置（SOUL.md 等价物）
- `/hermes-plan` — 任务规划（复杂任务前自动加载）
- `/pua` — 高压执行确保记忆闭环
- Operit `query_memory` 工具 — 底层全文检索
