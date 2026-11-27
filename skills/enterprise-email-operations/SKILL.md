---
name: enterprise-email-operations
description: Plan, configure, migrate, secure and verify business email for international small businesses, including mainland China teams. Use for provider and tenant selection, domain ownership, employee and shared mailboxes, MX/SPF/DKIM/DMARC, website email links and inquiry notifications, Astro or WordPress mail integration, delivery troubleshooting, recovery, offboarding and evidence-based acceptance. Produce an owner-friendly runbook and an implementation handoff without inventing DNS values or claiming unperformed delivery tests.
---
# Enterprise Email Operations

Build a recoverable business communication system, including the people who operate it. A domain address, DNS badge, API success response or provider delivery status alone is not end-to-end acceptance.

Research baseline: **2026-11-27**. Recheck mutable provider rules, regional eligibility, plan features and authentication standards before implementation. Use primary official sources, preserve their original URLs and add short Chinese explanations when preferred.

## 1. Establish scope and evidence

1. Read project instructions and inspect the existing website, DNS, email and inquiry workflows through authorized access.
2. Fill [assets/intake.example.json](assets/intake.example.json) with verified facts. Treat example.com, empty values and unverified regions as placeholders; never deploy them.
3. Identify the domain owner, authoritative DNS host, tenant region, current mailboxes, all sending services, operators, recovery contacts and authorized change scope.
4. Distinguish a new domain from a live migration. Keep working email and historical data intact while preparing changes.
5. Use existing task authorization; do not repeatedly request approval. If live DNS changes, billing, registration or external messages are outside scope, prepare the complete reviewable plan and mark only those actions blocked.
6. Never request passwords, recovery codes, private DKIM keys or API secrets in chat. Use approved secret stores. Keep credentials and customer bodies out of source control, analytics, public logs and examples.

Read [references/providers.md](references/providers.md) for tenant selection and onboarding. International and China-operated editions are different environments; do not mix admin URLs, MX, DKIM, OAuth endpoints or feature claims.

## 2. Choose the smallest reliable architecture

- Retain an existing provider if it passes acceptance.
- Give every human an individual identity and MFA. Use delegated/shared access for role addresses, never a password shared among employees.
- For one operator, a role alias may suffice if inbound routing and reply identity work. For several operators, use a shared mailbox/queue with an owner, backup, assignment and shared sent-message visibility.
- Separate human correspondence from authenticated website notifications, for example person@example.com and notify@notify.example.com. Add a separately governed marketing stream only when required.
- Do not promise complete reputation isolation from subdomains; organizational-domain or infrastructure reputation may be shared.
- Keep a durable inquiry record as the source of truth. Treat email as a notification channel.
- Keep administrative recovery independent of the domain or mailbox being recovered.
- Do not add MCP, self-hosted SMTP, a CRM or help desk without a requirement that justifies ongoing operation.

## 3. Prepare identity, mailboxes and a change plan

1. Have the owner register/select a business tenant using truthful regional, billing and identity details.
2. Separate daily and administrative access. Configure MFA, least privilege, emergency recovery and a backup operator.
3. Verify domain ownership with the exact challenge from the active tenant. Ownership verification must not by itself change receiving routes.
4. Create/license users and receiving destinations before switching MX. Verify role-address licensing, reply rights and sent-items behavior for the actual plan.
5. Inventory forms, CRM, invoices, scanners, newsletters, forwarding, aliases and applications that send or relay email.
6. Complete [assets/dns-change-plan.template.md](assets/dns-change-plan.template.md). Preserve full before/after RRsets, source of each provider value, propagation assumptions, evidence and rollback.
7. For migration, inventory folders, contacts/calendars, delegation, routing and archives. Select a currently supported migration method. Keep the old service until delta migration and reconciliation pass.

## 4. Configure authentication

Read [references/dns-and-delivery.md](references/dns-and-delivery.md) before changing DNS.

- Copy tenant-specific MX and DKIM values. Never derive selector targets from memory. Publishing DKIM and enabling signing are distinct checks.
- Publish one SPF policy per exact DNS owner. Merge approved senders if they share that envelope domain; evaluate recursive DNS lookups, not just visible include tokens.
- Configure aligned SPF and aligned DKIM on each controllable direct stream. Inspect actual envelope identity and trusted recipient headers.
- A single message passes DMARC through **aligned SPF OR aligned DKIM**. Do not demand both on every forwarded message; aim for both on the original direct stream.
- Start a new DMARC deployment with monitoring, a verified report destination and an accountable review process. Do not weaken working enforcement without diagnosed cause and authorization.
- Apply the 2026 update: RFC 9989 replaces RFC 7489/9091; pct, ri and rf are historic. Do not use percentage rollout as a reliable current default. Older receivers may ignore t=y.
- Do not require p=reject as the universal endpoint for human correspondence domains. Assess forwarding and mailing-list interoperability. Evaluate controlled transactional domains separately and document policy choices.
- Do not combine unrelated MX sets as automatic backup, user splitting or dual delivery. Use only a supported, documented coexistence route with loop prevention.
- Preserve unrelated DNS records. Do not change website A/AAAA or nameservers merely to set up email. Follow DNS-only requirements for mail-related CNAME targets.
- Account for previous TTL and caches. Restoring MX changes future routing after caching; it does not move already-delivered messages back.

## 5. Connect the website

Read [references/website-mail.md](references/website-mail.md). Use the website-contact-channels skill for contact layouts and social channels when available.

1. Display a verified, readable, copyable role email in the footer/contact page. Add mailto with encoded subject/body. Keep a fallback for devices without a mail client; a click does not send mail.
2. Make floating controls accessible without covering mobile content or consent controls. Preserve a non-JavaScript path.
3. Use a real server endpoint/action or approved hosted backend for forms. A static host cannot keep an API key secret or durably accept inquiries by itself.
4. Keep To fixed to an approved destination. Use an authenticated business From and validated visitor Reply-To. Never impersonate the visitor's domain or accept arbitrary client-supplied recipients/headers.
5. Validate on the server, bound request/field sizes, reject CR/LF in headers, escape displayed content, rate-limit and server-verify bot tokens when used. CAPTCHA does not replace database idempotency.
6. Persist the inquiry and outbox job atomically, or use an equivalent platform guarantee. Return success only after durable acceptance. Preserve input on errors.
7. Send through a worker where available, with durable idempotency, bounded retry/backoff, provider IDs, failure alerts and manual recovery. Provider deduplication windows are finite.
8. Verify webhook signatures on the raw body using official libraries; deduplicate event IDs and tolerate retries/out-of-order delivery. Delivered does not prove inbox placement, reading or business follow-up.
9. Enable visitor auto-replies only after abuse controls, sending limits and reply routing are verified.
10. Prefer supported OAuth/API flows for new integrations. Do not bypass SMTP changes by disabling MFA tenant-wide.

## 6. Verify reality

Use [references/acceptance-and-operations.md](references/acceptance-and-operations.md) and [assets/acceptance.template.md](assets/acceptance.template.md).

- Record PASS, FAIL, BLOCKED, NOT_RUN or N/A with timestamp, observer, evidence and remediation owner. Never infer PASS from a plan or simulation.
- Test external inbound, business reply and confirmed external receipt using authorized recipients representing actual markets and providers. Test role identity and delegation, not just the admin account.
- Collect sanitized SPF/DKIM/DMARC results from the trusted recipient's headers. An arbitrary Authentication-Results header supplied by a sender is not trustworthy.
- Verify public website → durable record → notification → human response → external receipt. Simulate notification failure without losing the record and record failure without showing success.
- Check retries, duplicate requests, bad input, authentication failure and access revocation using isolated data. Do not create uncontrolled external spoofing or bulk tests.
- Separate configuration validity, API acceptance, destination-server acceptance, folder placement, reading and business response.
- If domain/access is unavailable, deliver the complete staged plan and leave live acceptance NOT_RUN. Do not claim deployment.

## 7. Handoff and maintain

Deliver an owner-facing sequence, final architecture, provider/region/plan, responsibility table, DNS diff, original official sources, known limitations, recovery/rollback and acceptance register.

Assign daily inquiry/queue/quarantine review; periodic sending-source, delivery-error, permissions and aggregate-report review; domain/subscription renewals; and offboarding that revokes sign-in, sessions, tokens and delegated access while preserving business data. Label example response targets as proposals, not vendor SLAs.

For suspected compromise, contain access, revoke sessions/tokens, inspect forwarding/rules/delegates, preserve evidence and recover through the provider. Verify bank-account changes through a separately known contact channel.
