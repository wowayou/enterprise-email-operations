# Acceptance and continuing operations

Research baseline: 2026-11-27. Use `assets/acceptance.template.md`; retain its IDs and statuses instead of creating a second competing register. All unperformed tenant checks and mail tests remain NOT_RUN. Explain every N/A and identify an owner for BLOCKED or failed work.

## Prove progressively stronger outcomes

Separate reviewed documentation, observed DNS, tenant configuration, sending-service acceptance, destination-server acceptance, recipient folder placement and completed human response. Evidence at one layer does not establish the next. In particular, Microsoft Message Trace “Delivered” can include junk or quarantine; inspect events. Google Email Log Search delivery to a third-party SMTP server does not prove that server's final inbox placement. Sources: [Microsoft trace FAQ](https://learn.microsoft.com/en-us/exchange/monitoring/trace-an-email-message/message-trace-faq), [Google status definitions](https://knowledge.workspace.google.com/admin/gmail/advanced/email-log-search-delivery-status-definitions).

Build the recipient matrix from actual markets: controlled Gmail, Outlook.com, Yahoo and relevant Chinese mailboxes such as QQ/163, plus an authorized partner domain when useful. Record exactly which were tested; a Gmail pass does not stand in for Yahoo. Lack of an authorized account leaves that case NOT_RUN or BLOCKED, not PASS.

For each path, send representative Chinese/English business content with normal signatures, links and attachments. Verify external inquiry → correct business recipient → authorized human reply → external receipt. Exercise each real sending service and intended desktop/mobile client. Record test ID, UTC time, sender/recipient, provider IDs, Message-ID, initial folder, trusted authentication results and actual reply identity. Observe first placement before allowlisting or moving mail; retain the original failure when retesting a fix.

For forms, also require the durable inquiry and outage checks in `references/website-mail.md`. Test indirect routes only if used. Test failures with controlled recipients or isolated simulation; account for catch-all behavior and avoid uncontrolled spoofing or bulk tests. For migration, reconcile sampled messages, attachments, folders, permissions and post-cutover increments before closing the old service.

## Use trustworthy evidence

Export original messages from the actual receiving mailbox. Interpret Authentication-Results only within the receiving provider's trusted boundary, with its authserv-id, Received chain and administrative trace where available. A sender can forge that header; an arbitrary line containing `pass`, quoted headers in a body, or a sender's saved copy is insufficient. Message-ID correlates evidence; it is not an authentication signature. Source: [RFC 8601](https://www.rfc-editor.org/rfc/rfc8601.html).

Keep redacted evidence privately. Do not upload customer message bodies, addresses or IPs to public analyzers without authorization. Do not count tracking-pixel opens as read or inbox proof: [Apple Mail Privacy Protection](https://www.apple.com/legal/privacy/data/en/mail-privacy-protection/) can preload remote content without a human opening the message.

## Verify access and recovery

Give people individual identities and least-privileged delegated roles. Verify MFA enforcement with a fresh test login, not enrollment alone. Prefer supported phishing-resistant methods; protect recovery codes outside the affected mailbox. Retain a working recovery path while testing, rather than locking out every administrator. Source: [Google administrator security](https://knowledge.workspace.google.com/admin/users/security-best-practices-for-administrator-accounts).

For Microsoft shared mailboxes, block direct sign-in. Check read access separately from Send As/Send on Behalf and test shared Sent Items visibility with two authorized operators. An alias alone supplies neither collaborative assignment nor independent access control. Sources: [shared mailboxes](https://learn.microsoft.com/en-us/microsoft-365/admin/email/about-shared-mailboxes), [shared Sent Items](https://learn.microsoft.com/en-us/microsoft-365/admin/email/configure-a-shared-mailbox).

Offboarding must address sign-in, applicable sessions/tokens, delegation, forwarding, inbox rules and application grants. Preserve or transfer required data and receiving continuity before license removal/deletion. Test revocation with a safe test identity; changing a password alone is insufficient evidence. Source: [Microsoft employee removal](https://learn.microsoft.com/en-us/microsoft-365/admin/add-users/remove-former-employee). Where backup or retention is in scope, restore an authorized sample and inspect its content; an export job's success is not restoration evidence.

## Hand over an operating service

Assign a primary and backup inquiry owner, customer-approved response targets, daily queue/quarantine review, periodic sender/permission/report review, renewals and escalation. Demonstrate finding an inquiry, replying correctly, investigating a failure and recovering access. Schedule low-volume DMARC observation with an owner and review date; missing reports must not be recorded as zero failures or automatically delay every basic mailbox launch. Record production-ready, limited-pilot or blocked scope with unresolved items. Configuration success never guarantees future inbox placement or that every inquiry will receive a business response.
