# enterprise-email-operations

出海企业邮箱配置与运营：中文操作指南、英文 Agent Skill、项目模板与联合验收。

- [完整中文手册](docs/enterprise-email-guide.zh-CN.md)
- [HTML 阅读版（下载后打开）](docs/enterprise-email-guide.zh-CN.html)
- [开工与验收清单](docs/enterprise-email-checklist.zh-CN.md)
- [英文 Skill](skills/enterprise-email-operations/SKILL.md)

## 终端 Agent 使用与维护

- [终端 Agent 使用说明](docs/AGENT_USAGE.md)：Codex CLI、Claude Code、Pi 的安装、调用、更新与排查。
- [AGENTS.md](AGENTS.md)：维护本仓库时遵循的项目规范。

## 使用

将 `skills/enterprise-email-operations/` 复制到目标 Agent 支持的技能目录，或直接要求 Agent 阅读其中的 SKILL.md。项目模板复制到私有项目填写，禁止提交客户凭据、邮件内容和敏感验收证据。

研究基线：2026-11-27。实施前复核官方资料及实际租户配置。真实开户、DNS 修改、网站接入和邮件往返验收尚未执行。本仓库为操作指南与模板，并非已部署的邮箱服务。

相关项目：[website-contact-channels](https://github.com/wowayou/website-contact-channels)。
