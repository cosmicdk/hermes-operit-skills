# 决策日志

> 记录重要的设计决策及其理由。

## 2026-05-01: 创建 hermes-* Skill 系列

**决策**: 创建 hermes-soul / hermes-plan / hermes-memory 三个 Skill
**理由**: 
- 用户希望 Operit 学习 Hermes Agent 的设计理念
- hermes-soul: 人格配置 + 自进化（对标 SOUL.md + AGENTS.md）
- hermes-plan: 任务规划（对标 /plan 内置 Skill）
- hermes-memory: 三层记忆管理（对标 Hermes 记忆系统）
- 替代已删除的 operamem Skill

## 2026-05-01: 删除 operamem Skill

**决策**: 删除 operamem
**理由**: 用户直接要求删除；功能被 hermes-memory 吸收

## 2026-04-30: PRoot 崩溃

**问题**: 手机重启后 PRoot 启动探测失败
**影响**: 所有 MCP 不可用
**教训**: PRoot 运行时不等于稳定系统，需关注环境健康
