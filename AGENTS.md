# AGENTS.md

Repository-wide guidance for agents maintaining this project. For work on a customer's email system or website, use skills/enterprise-email-operations/SKILL.md instead of transplanting these repository rules.

- Read README.md, the skill and relevant references before editing. Inspect the current branch and diff; preserve unrelated work.
- Keep the skill provider-neutral and practical for international small businesses, including mainland China teams. Reuse working infrastructure when it meets acceptance. Do not add dependencies or automation without a demonstrated need.
- Verify mutable provider, regional, pricing and protocol facts against official sources. Keep original URLs, Chinese explanations, research dates and limitations. Maintain consistency between the Markdown/HTML guides, references and acceptance templates.
- Never invent tenant-specific DNS values, provider eligibility, billing terms or test results. Separate mailbox configuration, transport acceptance, inbox placement, human reply and durable inquiry storage.
- Keep sample domains and tenant values illustrative. Never commit passwords, API tokens, OTPs, private keys, customer email bodies or real acceptance evidence. Avoid real DNS changes, account registration, billing, outbound mail and deployment without authorization.
- For documentation changes, inspect internal links, referenced paths, template syntax and consistency of acceptance IDs. Validate example JSON locally. For implementation changes, use an isolated target environment and report actual checks and failures; this repository has no automated live email test suite.
- Keep unperformed tenant, migration, website and mail tests NOT_RUN or BLOCKED as appropriate. Do not claim deployment from a successful configuration or simulated result.
- Keep changes bounded; report changed files, actual tests, limitations and rollback. Commit or push only when authorized; never force-push.

For terminal installation and invocation, see [docs/AGENT_USAGE.md](docs/AGENT_USAGE.md).
