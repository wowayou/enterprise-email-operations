# 终端 Agent 使用说明

适用：Codex CLI、Claude Code、Pi，以及能够读取本地文件的其他 Coding Agent。本仓库提供企业邮箱操作 Skill、官方资料和验收模板，并非可直接部署的邮件服务器。

## 1. 获取 Skill

以下命令适用于 Bash / Zsh（Linux、macOS、WSL）。先确认目标目录不存在；已有仓库请检查修改后更新，不要覆盖。

```bash
mkdir -p "$HOME/.local/share/agent-skills-src"
git clone https://github.com/wowayou/enterprise-email-operations.git "$HOME/.local/share/agent-skills-src/enterprise-email-operations"
SKILL_DIR="$HOME/.local/share/agent-skills-src/enterprise-email-operations/skills/enterprise-email-operations"
test -f "$SKILL_DIR/SKILL.md"
```

完整技能目录包含 SKILL.md、references、assets 和 agents。不要只复制 SKILL.md。安装前先审阅；进入真实客户项目的私有工作目录再启动 Agent。

## 2. 安装或直接调用（任选一种）

### A. 通用方式：不安装

启动终端 Agent，将 SKILL.md 的实际绝对路径交给它，要求先读取主文件，再按任务读取引用与模板。不依赖自动发现，是最简单的兜底方案。

### B. Codex CLI

用户级技能目录为 ~/.agents/skills/，项目级为目标仓库的 .agents/skills/。以下演示用户级安装；如目标目录已存在，先检查差异，不要覆盖。

```bash
mkdir -p "$HOME/.agents/skills"
test ! -e "$HOME/.agents/skills/enterprise-email-operations" && cp -R "$SKILL_DIR" "$HOME/.agents/skills/"
codex
```

在 Codex 交互输入框输入 `$enterprise-email-operations` 和任务描述，或通过 /skills 选择（以安装版本为准）。

### C. Claude Code

用户级目录为 ~/.claude/skills/，项目级为 .claude/skills/。

```bash
mkdir -p "$HOME/.claude/skills"
test ! -e "$HOME/.claude/skills/enterprise-email-operations" && cp -R "$SKILL_DIR" "$HOME/.claude/skills/"
claude
```

在交互输入框使用 `/enterprise-email-operations` 加任务描述。Claude Code 的仓库级指导通常使用 CLAUDE.md；维护本仓库时明确要求读取 AGENTS.md，不假定其自动加载。

### D. Pi

```bash
pi --skill "$SKILL_DIR"
```

在交互输入框使用 `/skill:enterprise-email-operations` 加任务描述。也可将完整技能目录复制到 ~/.pi/agent/skills/（用户级）或 .pi/skills/（项目级）；支持共享 .agents/skills 的版本可复用该位置。

这些调用表达式属于 Agent 交互输入，而非 Bash 命令。新安装后建议启动新会话，并确认技能名和实际加载路径。

## 3. 直接交给 Agent 的任务

```text
使用 enterprise-email-operations Skill。若未自动发现，请先读取
<本地绝对路径>/skills/enterprise-email-operations/SKILL.md。

为当前客户审计并规划可靠的企业邮箱和网站询盘通知。
先读取现有配置，保留正常工作的邮箱、DNS 和业务数据。
按实际服务商、租户区域、套餐和域名核对官方文档。
复制项目输入、DNS 变更及验收模板到私有工作区。
区分人员邮箱、共享业务地址和网站通知发件身份；
表单先持久化询盘，再发送邮件通知。
先交付实施计划、DNS 差异、客户操作步骤及回滚方法。
只在授权范围内实施，未实测项标记 NOT_RUN 或 BLOCKED。
不得编造 DNS 值或收发测试结果，不在聊天、仓库或日志中存储凭据。
```

需要的输入：实际域名、DNS 托管商、现有邮箱服务与租户区域、人员数量、业务地址、网站架构、现有表单及发送来源、授权范围。参考 assets/intake.example.json。不要把密码、验证码、私钥或客户邮件发送给 Agent。

## 4. 验收与边界

- 先读 references/providers.md 和 dns-and-delivery.md，再按范围读 website-mail.md 与 acceptance-and-operations.md。
- 使用 assets/dns-change-plan.template.md 记录精确 DNS 值、变更依据与回滚；使用 assets/acceptance.template.md 保留逐项证据。
- 客户本人完成必要的开户、身份验证、恢复设置及真实收发。未经授权不修改生产 DNS、不购买套餐、不发真实邮件。
- 本仓库没有自动化真实邮件测试套件。模板检查、API 成功和 DNS 语法正确不能替代外部真实收发与回复。
- 网站联系入口与社媒布局使用 [website-contact-channels](https://github.com/wowayou/website-contact-channels)；本技能负责邮箱与询盘处理基础设施。

## 5. 更新和排查

源仓库无本地改动时执行 git pull --ff-only。复制安装的技能不会自动同步；比较已有版本，备份个人修改后替换整个目录，再启动新会话。若无法发现技能，检查 SKILL.md、目录结构、客户端版本与工作目录，或者使用 A 方式直接读取。

官方资料：
- [Codex Skills](https://developers.openai.com/codex/skills)
- [Claude Code Skills](https://code.claude.com/docs/en/skills)
- [Pi Skills](https://github.com/earendil-works/pi/blob/main/packages/coding-agent/docs/skills.md)

客户端版本与设置可能不同；以上为文档化命令示例，尚未在三款终端逐一执行。以实际客户端帮助与官方文档为准。
