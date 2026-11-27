# AGENTS.md

Repository-maintenance rules only. Do not copy this file into a customer project as the skill's execution instructions.

- Inspect the current branch, diff and repository instructions before editing; preserve unrelated work.
- Single-source policy: README.md owns installation, invocation and updates; skills/enterprise-email-operations/SKILL.md is the sole execution entrypoint. Its references and assets own detailed rules and acceptance criteria. Do not duplicate them in AGENTS.md, README examples or separate agent guides. Chinese human-facing manuals explain the workflow, not a competing agent standard. Update affected representations when their source changes.
- Follow the [Agent Skills specification](https://agentskills.io/specification): one matching skill directory and SKILL.md, concise instructions, directly linked on-demand resources. Keep client-specific setup outside the skill. Do not introduce a second skill manifest or independent local copies of the workflow.
- Verify mutable provider facts, region-specific capabilities, standards and pricing against official sources. Preserve original links, research dates and uncertainties; never invent tenant-specific DNS values.
- Use synthetic fixtures. Never commit credentials, private keys, OTPs, customer email bodies or private evidence.
- For changes, check internal links, referenced paths, template syntax and acceptance-ID consistency. Validate example JSON locally when changed. There is no automated live email test suite; do not claim live tests from document checks or simulations.
- Keep changes bounded. Report actual checks, limitations and rollback. Commit or push only when authorized; never force-push.
