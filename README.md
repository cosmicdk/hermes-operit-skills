# Hermes Operit Skills

> 🧠 Hermes Agent 设计理念在 Operit 平台的 Skill 实现
> *"The agent that grows with you."* — Nous Research

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![Skills](https://img.shields.io/badge/Skills-3-blue)](./)
[![Platform](https://img.shields.io/badge/Platform-Operit-orange)]()

---

## 📦 概述

本项目将 **Nous Research Hermes Agent** 的核心设计理念移植到 **Operit AI 平台**，
包含三个协同工作的 Skill：

| Skill | 对标 Hermes | 功能 |
|---|---|---|
| **hermes-soul** | SOUL.md + AGENTS.md | 人格配置 + 项目上下文 + 自进化记忆 |
| **hermes-plan** | /plan 内置 Skill | 复杂任务结构化拆解与规划 |
| **hermes-memory** | MEMORY.md + USER.md + FTS5 | 三层记忆架构（短期/中期/长期） |

---

## 🚀 快速安装

### Operit 平台一键安装

```bash
# 克隆到 Operit skills 目录
cd /sdcard/Download/Operit/skills/
git clone https://github.com/cosmicdk/hermes-operit-skills.git temp
mv temp/hermes-* .
rm -rf temp
```

### 手动安装

将 `hermes-soul/`、`hermes-plan/`、`hermes-memory/` 三个目录复制到
`/sdcard/Download/Operit/skills/` 下即可，Operit 会自动识别。

---

## 🎯 三个 Skill 详解

### 1. hermes-soul — 自进化人格配置

对标 Hermes 的 `~/.hermes/SOUL.md` + `~/.hermes/AGENTS.md`。

- **personality.md** — 持久化人格定义（SOUL.md 等价物）
- **user-profile.md** — AI 自动维护的用户画像（USER.md 等价物）
- **memory-bank.md** — 项目规律/偏好/环境（MEMORY.md 等价物）
- **自进化闭环** — 每次会话后自动提炼关键信息

```
触发词: "hermes模式" "/soul" "记住这个偏好" "以后都这样"
```

### 2. hermes-plan — 结构化任务规划

对标 Hermes 内置 `/plan` Skill。在执行前生成结构化计划，
防止 Agent 方向偏差和返工。

```
触发词: "/plan" "规划一下" "先做计划" "拆解任务"
```

### 3. hermes-memory — 三层增强记忆

对标 Hermes 的 MEMORY.md + USER.md + SQLite FTS5 全文检索。

- **第一层**：会话上下文（短期）
- **第二层**：memory-bank + user-profile（中期，跨会话）
- **第三层**：Operit query_memory 系统（长期，全文检索）

```
触发词: "/memory" "记住这个" "回顾一下" "搜索记忆"
```

---

## 📖 设计哲学

本项目严格遵循 Hermes Agent 的以下核心设计理念：

| Hermes 理念 | 本实现 |
|---|---|
| **自进化学习闭环** | AI 主动检查→自主更新记忆文件 |
| **渐进式加载** | metadata → SKILL.md → references |
| **Agent 自主维护记忆** | 4 个触发条件自动沉淀 |
| **有限容量强制信息压缩** | ~2,500 字符软限制 + 自动合并 |
| **无厂商锁定** | MIT 协议，兼容 agentskills.io 标准 |

详见：[hermes-soul/references/hermes-design.md](./hermes-soul/references/hermes-design.md)

---

## 🔗 搭配使用

```
/hermes-soul           ← 定义风格和人格
   +
/hermes-plan           ← 复杂任务先规划
   +
/hermes-memory         ← 跨会话持久记忆
   +
/pua                   ← 高压执行确保闭环（可选）
```

---

## 📂 项目结构

```
hermes-operit-skills/
├── README.md
├── LICENSE
├── hermes-soul/
│   ├── SKILL.md                    # 主 Skill 文件
│   └── references/
│       ├── personality.md          # SOUL.md 等价物
│       ├── user-profile.md         # USER.md 等价物
│       ├── memory-bank.md          # MEMORY.md 等价物
│       ├── hermes-design.md        # Hermes 设计速查
│       └── decision-log.md         # 重要决策记录
├── hermes-plan/
│   └── SKILL.md                    # /plan 等价物
└── hermes-memory/
    ├── SKILL.md                    # 三层记忆管理
    └── references/
```

---

## 🎓 参考资料

- [Hermes Agent 官方文档](https://hermes-agent.nousresearch.com/docs/)
- [Hermes Agent GitHub](https://github.com/NousResearch/hermes-agent)
- [Hermes Agent 中文社区](https://hermesagent.org.cn/)
- [agentskills.io 开放标准](https://agentskills.io/)

---

## 📄 License

MIT © 2026 cosmicdk

基于 Nous Research Hermes Agent (MIT) 的设计理念构建。