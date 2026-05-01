# Memory Bank

> 由 AI 自主维护的项目笔记。
> 对标 Hermes Agent 的 `~/.hermes/MEMORY.md`。
> 最后更新: 2026-05-01

## 项目环境
- Operit 运行在 Android 端，通过 PRoot 提供 Ubuntu 24.04.4 LTS
- Skills 目录: /sdcard/Download/Operit/skills/
- MCP 插件: /sdcard/Download/Operit/mcp_plugins/
- PRoot 崩溃会导致所有 MCP 不可用（已发生过）

## 部署环境
- 阿里云 ECS Ubuntu 服务器（用于部署 Hermes Agent）
- SSH 客户端推荐: JuiceSSH / Termius / ServerBox
- 安全组需额外开放 8080/8443 端口

## 编码规范
- 所有文件使用 UTF-8
- Shell 脚本 shebang: #!/bin/bash
- Python 文件编码声明不需要（Python 3 默认 UTF-8）
- 避免 \x 转义序列，直接写 UTF-8 字符

## 已知陷阱
- GitHub README 推送时 \x 转义序列会变乱码（已修复，commit b61d905）
- PRoot 重启后可能崩溃，需重新探测
- 阿里云 ECS 安全组默认只开 22 端口，新增端口需手动配置

## 重要决策
- 2026-05-01: Operamem Skill 已删除，替换为 hermes-memory
- 2026-05-01: 创建 hermes-soul / hermes-plan / hermes-memory 三个 Skill
