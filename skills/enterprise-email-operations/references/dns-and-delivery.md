# DNS and delivery decisions

Research baseline: 2026-11-27. Recheck current tenant instructions before changes. Use `assets/dns-change-plan.template.md` for exact records, authorization, evidence and rollback; never deploy example values.

## Receiving routes and migration

Copy MX from the actual tenant. Lower preference numbers take priority; equal preferences may be selected in different orders. Independent providers' MX records do not split users or copy messages. Use documented coexistence: Google describes recipient routing through one incoming system; Microsoft allows removing old MX or lowering its priority during its setup process. Neither establishes arbitrary mixed MX as a reliable design. Sources: [SMTP routing](https://datatracker.ietf.org/doc/html/rfc5321#section-5), [Google split delivery](https://knowledge.workspace.google.com/admin/gmail/advanced/send-email-to-2-email-systems-with-split-delivery), [Microsoft DNS setup](https://learn.microsoft.com/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).

Before cutover, inventory recipients, aliases, shared addresses, routing, applications and retained data. Create destinations and permissions first. Export complete affected RRsets and TTLs from the authoritative DNS host. Preserve unrelated website records. Allow existing caches to expire; lowering TTL does not clear earlier cached answers. Keep both services accessible, monitor both, and reconcile incremental mail before retirement. Restoring MX does not move messages already received elsewhere. If MTA-STS is enforced, reconcile its cached allowed-MX policy before changing routes.

## SPF: identity and evaluation budget

Maintain one selectable `v=spf1` TXT record per exact DNS owner. Unrelated TXT records are allowed; multiple quoted strings within one TXT record are not multiple SPF policies. SPF normally authenticates the envelope MAIL FROM domain, not the visible From address.

Count DNS-querying terms recursively across `include` and `redirect`: `include`, `a`, `mx`, `ptr`, `exists` and `redirect` share the ten-term evaluation limit. Do not count only top-level includes or equate this limit with ten actual DNS packets. `ip4`, `ip6` and `all` do not consume that budget. Avoid unnecessary `ptr`.

Authorize actual envelope-domain senders. A website using an external mail API does not automatically need its hosting IP in SPF; a vendor using its own return path does not automatically require an include at the customer's root. Remove obsolete authorization, or use supported return-path subdomains. Do not solve overflow with a second SPF record or unmanaged static flattening. Source: [RFC 7208](https://www.rfc-editor.org/rfc/rfc7208.html), [Google SPF troubleshooting](https://knowledge.workspace.google.com/admin/security/troubleshoot-spf-issues).

## DKIM: publication and signing

Prefer provider-supported 2048-bit RSA keys; do not describe that preference as every receiver's minimum. Copy the tenant's selector and complete TXT/CNAME value. Microsoft uses two selectors for rotation; its current targets must not be reconstructed from old examples. Publish the public key without truncation. If the DNS interface requires string chunks, keep them within one TXT record rather than creating multiple records at one selector; see [RFC 6376 §3.6.2.2](https://www.rfc-editor.org/rfc/rfc6376.html#section-3.6.2.2). Then enable signing in the provider. DNS visibility alone does not prove signing. Google documents a 24–72 hour wait after activating Gmail before a new organization can generate its DKIM key. Follow provider activation dependencies, record pending steps, and complete actual signing verification before passing authentication acceptance.

Verify actual received signatures for every direct sending stream: `d=` identifies the signing domain and `s=` selects its key. Retain old selectors as required for rotation and in-flight mail. Never place private keys in handoff files. Sources: [Google DKIM setup](https://knowledge.workspace.google.com/admin/security/set-up-dkim), [Microsoft DKIM configuration](https://learn.microsoft.com/en-us/defender-office-365/email-authentication-dkim-configure).

## DMARC after the 2026 revision

[RFC 9989](https://www.rfc-editor.org/rfc/rfc9989.html) replaces RFCs 7489/9091. A message passes with aligned, authenticated SPF **or** DKIM; complete participation requires deploying both, and reject must not rely solely on SPF. DNS Tree Walk changes policy discovery: do not infer organizational boundaries from the last two labels. An explicit child policy applies; otherwise evaluate applicable `sp`/`np`/`p` inheritance.

For routine users potentially participating in Internet mailing lists, §7.4 advises against `p=reject`. If nevertheless pursuing it, its conditional guidance is at least one month at none, then equally long at quarantine, reviewing effects and informing users. This is not a universal mailbox-launch delay.

`t=y` lowers requested failure handling one level, not universally to none. Older receivers may ignore it and enforce `p`; therefore it is not a universally safe rollout switch.

The [IANA registry](https://www.iana.org/assignments/dmarc-parameters) marks `pct`, `ri` and `rf` historic. Do not use percentage enforcement as the safety mechanism for a new rollout.

For a new deployment, choose an observation policy with an existing, owned report destination. Preserve an established working policy unless evidence and authorization justify changing it. Map every From domain to its envelope domain, DKIM domain and applicable policy. Before tightening, account for occasional billing/CRM sends, indirect routes, unexplained failures and recovery. Treat reject as a separate decision, not a mandatory completion checkbox. External report destinations may need destination-domain authorization; absence of reports does not prove clean traffic. Source: [aggregate reporting](https://www.rfc-editor.org/rfc/rfc9990.html).

## Indirect delivery and recipient-specific requirements

Forwarding can fail SPF; an intact aligned DKIM signature can preserve DMARC. Rewriting content can break DKIM. SRS rewrites the envelope sender and does not guarantee alignment with the original From. ARC supplies authenticated history; receiver trust and local policy still matter. Test the actual forwarding/list route. Sources: [Microsoft SRS](https://learn.microsoft.com/en-us/exchange/reference/sender-rewriting-scheme), [ARC specification](https://www.rfc-editor.org/info/rfc8617/).

Recheck the applicable recipient's rules rather than inventing one universal bulk threshold:

- [Gmail](https://support.google.com/mail/answer/81126): approximately 5,000 messages daily to personal Gmail triggers bulk requirements; SPF, DKIM and DMARC are required. Marketing/promotional mail needs compliant one-click unsubscribe; ordinary transactional messages are distinguished in the [FAQ](https://support.google.com/mail/answer/14229414).
- [Yahoo](https://senders.yahooinc.com/best-practices/): bulk authentication and subscription controls apply, but its [FAQ](https://senders.yahooinc.com/faqs/) publishes no fixed bulk volume threshold.
- [Outlook.com](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/strengthening-email-ecosystem-outlook%E2%80%99s-new-requirements-for-high%E2%80%90volume-senders/4399730): above 5,000 messages daily, require SPF/DKIM passes and DMARC at least none with alignment. This concerns consumer Outlook/Hotmail/Live recipients, not a universal Microsoft 365 tenant threshold.

Authenticate ordinary business mail fully without treating every personal reply as a newsletter. Treat [MTA-STS/TLS-RPT](https://knowledge.workspace.google.com/admin/gmail/advanced/about-mta-sts-and-tls-reporting) and [BIMI](https://knowledge.workspace.google.com/admin/security/set-up-bimi) as separately justified enhancements, not prerequisites or inbox guarantees.
