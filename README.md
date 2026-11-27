# Enterprise Email Operations

出海企业邮箱配置与运营：中文操作指南、英文 Agent Skill、项目模板与联合验收。

- [SKILL.md](skills/enterprise-email-operations/SKILL.md)：唯一业务执行入口，按需加载 references 和 assets。
- [中文操作手册](docs/enterprise-email-guide.zh-CN.md) · [HTML 阅读版](docs/enterprise-email-guide.zh-CN.html) · [客户开工与验收清单](docs/enterprise-email-checklist.zh-CN.md)：人工阅读与协作资料，不是另一套 Agent 执行标准。
- [AGENTS.md](AGENTS.md)：仓库维护规范。

## 安装与使用

本节是本仓库唯一维护的终端 Agent 安装、调用和更新说明。业务执行从 [SKILL.md](skills/enterprise-email-operations/SKILL.md) 开始；按它的指引读取配套资源，不另行维护一份执行提示词。

### 获取源码（Linux / macOS / WSL）

在终端执行。已有 checkout 时复用原目录，不重复克隆。

```bash
REPO_DIR="$HOME/.local/share/agent-skills-src/enterprise-email-operations"
mkdir -p "$(dirname "$REPO_DIR")"
git clone https://github.com/wowayou/enterprise-email-operations.git "$REPO_DIR"
SKILL_DIR="$REPO_DIR/skills/enterprise-email-operations"
test -f "$SKILL_DIR/SKILL.md"
```

先审阅完整技能目录，包括脚本和引用文件，再进入实际客户项目的私有工作目录启动 Agent。不要将本技能仓库当作邮件服务器部署。

### 方式一：直接使用（无需安装）

从目标项目启动 Agent，要求其读取 `$SKILL_DIR/SKILL.md` 的实际绝对路径，按文件及相关引用完成任务。将变量展开后的真实路径提供给 Agent。

### 方式二：长期使用（推荐共享同一份源码）

Codex CLI 与支持共享目录的 Pi 可共同使用以下符号链接：

```bash
mkdir -p "$HOME/.agents/skills"
DEST="$HOME/.agents/skills/enterprise-email-operations"
if [ ! -e "$DEST" ] && [ ! -L "$DEST" ]; then
  ln -s "$SKILL_DIR" "$DEST"
fi
```

Claude Code 若也需要使用，再建立指向**同一个**技能目录的链接：

```bash
mkdir -p "$HOME/.claude/skills"
DEST="$HOME/.claude/skills/enterprise-email-operations"
if [ ! -e "$DEST" ] && [ ! -L "$DEST" ]; then
  ln -s "$SKILL_DIR" "$DEST"
fi
```

如果目标已存在，请检查实际指向或内容，必要时手动迁移；不要覆盖已有技能或安装多个同名版本。无法使用符号链接时，复制完整技能目录作为发行快照，更新时重新同步，不直接修改副本。

| 终端 Agent | 从目标项目启动 | 在交互输入框调用 |
|---|---|---|
| Codex CLI | `codex` | `$enterprise-email-operations` |
| Claude Code | `claude` | `/enterprise-email-operations` |
| Pi | `pi` | `/skill:enterprise-email-operations` |

Pi 未安装或不支持共享目录时，可用 `pi --skill "$SKILL_DIR"` 临时加载，避免同时自动发现同名技能。项目级安装位置和版本差异以客户端官方文档为准。

### 示例任务

```text
使用 enterprise-email-operations Skill，为当前客户审计企业邮箱及网站询盘通知，制定可验收的实施计划。
参考技能内的输入模板，按 SKILL.md 和其引用的验收标准交付。
本轮只做审计与计划，不修改生产 DNS、不开通付费服务、不发送真实邮件。
```

上述是用户任务示例，不是第二套执行规范。

### 更新及排查

```bash
git -C "$REPO_DIR" status --short
# 确认工作区干净后
git -C "$REPO_DIR" pull --ff-only
```

符号链接不需要重新复制。启动新 Agent 会话，确认发现的是所需技能及正确路径；无法发现时使用方式一。项目团队也可以固定经过审核的提交，避免无意升级。

参考：[Agent Skills 开放规范](https://agentskills.io/specification) · [Anthropic Skills 示例仓库](https://github.com/anthropics/skills) · [Codex Skills](https://developers.openai.com/codex/skills) · [Claude Code Skills](https://code.claude.com/docs/en/skills) · [Pi Skills](https://github.com/earendil-works/pi/blob/main/packages/coding-agent/docs/skills.md)。

客户端路径和调用方式依据官方资料核对（2026-11-27），未在三款终端逐一实测。


## 仓库维护及验证边界

维护本仓库时阅读 [AGENTS.md](AGENTS.md)。研究基线：2026-11-27；实施前复核官方资料及实际租户配置。本仓库为操作指南与模板，并非已部署的邮箱服务；真实开户、DNS 修改、网站接入和邮件往返验收尚未执行。

相关 Skill：[website-contact-channels](https://github.com/wowayou/website-contact-channels)。
