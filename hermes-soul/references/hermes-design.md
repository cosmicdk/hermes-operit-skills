# Hermes Agent 设计参考

> Nous Research 开源的自进化 AI Agent 框架 (2026.02)

## 核心设计理念

1. **The agent that grows with you** — 越用越懂你
2. **自进化学习闭环** — 从成功任务中自动提炼 Skill
3. **渐进式加载** — 默认只加载技能列表(~3K tokens)，需要时才加载完整内容
4. **持久化记忆** — 跨会话自动维护 MEMORY.md + USER.md
5. **无厂商锁定** — 支持 200+ 模型自由切换

## 三层记忆架构

| 层 | Hermes | Operit 对标 |
|---|---|---|
| 短期 | 会话上下文窗口 | 当前对话 |
| 中期 | MEMORY.md (2,200字符) + USER.md (1,375字符) | hermes-soul/references/*.md |
| 长期 | SQLite + FTS5 + Honcho | query_memory 系统 |

## Skill 系统

- Hermes: `~/.hermes/skills/SKILL.md`（agentskills.io 标准）
- Operit: `/sdcard/Download/Operit/skills/<name>/SKILL.md`（同标准）

## 关键命令对照

| Hermes | Operit 等价 |
|---|---|
| `hermes` | 对话入口 |
| `hermes model` | 模型切换 |
| `hermes setup` | — |
| `hermes -c` | — |
| `hermes gateway` | MCP 桥接 |
| `hermes memory search` | `/memory search` |
| `hermes skills install` | Skill 安装 |
| `/plan` | `/hermes-plan` |

## SOUL.md 示例

```markdown
# 灵魂
You are a senior backend engineer. Be terse and direct.
Skip explanations unless asked.
Always consider error handling and edge cases.
```

## 参考资料

- GitHub: github.com/NousResearch/hermes-agent
- 官网: hermes-agent.nousresearch.com
- 中文社区: hermesagent.org.cn
- GitHub Stars: ~95.6K (2026年4月)
