# Website mail implementation

Research baseline: **2026-11-27**. Recheck linked documentation against the installed release, tenant and account. Treat examples as unexecuted designs. Follow the main skill for authorization, ownership, DNS planning and operational handoff.

## 1. Select the route

Keep human correspondence at an approved business mailbox provider, such as the customer's applicable Zoho Mail or Microsoft 365 edition. Use a separately authenticated transactional stream for website notifications. Retain existing working mailboxes. Do not assume global Microsoft OAuth integrations support China-operated tenants.

Display a readable address and `mailto:sales@example.com`, with a copy option and selectable-text fallback. [Mailto opens a configured email handler](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a); it does not send anything. Clipboard access can fail. Never count a click as a received inquiry.

### Astro

Inspect `package.json`, the lockfile, adapter and deployed runtime before changing configuration.

- **Endpoint:** add a POST handler such as `src/pages/api/inquiries.ts`; use the matching server adapter and `export const prerender = false` when opting this route out of prerendering. Other pages may remain static.
- **Actions:** use `defineAction`, form acceptance and server-side schema validation. A page invoking an Action through an HTML form action must be rendered on demand. Preserve field values and accessible error feedback.
- **Static-only hosting:** use an independent serverless endpoint or approved hosted form backend with durable entries, export and failure handling. A static HTML upload cannot execute the endpoint. Never substitute a mailto form or browser-side SMTP/API secret.

Read [on-demand rendering](https://docs.astro.build/en/guides/on-demand-rendering/), [Actions](https://docs.astro.build/en/guides/actions/) and [API form routes](https://docs.astro.build/en/recipes/build-forms-api/). Keep secrets server-side; `PUBLIC_` variables are client-visible, and runtime access differs between adapters: [environment variables](https://docs.astro.build/en/guides/environment-variables/).

### WordPress

1. Configure a form that retains submissions. Verify Fluent Forms Entries, or pair Contact Form 7 with Flamingo; [CF7 alone does not store messages](https://contactform7.com/save-submitted-messages-with-flamingo/).
2. Configure one internal notification with the headers below. Check for duplicate notification rules and disabled storage.
3. Select one maintained mail integration. [WP Mail SMTP's Resend API mailer](https://wpmailsmtp.com/docs/how-to-set-up-the-resend-mailer-in-wp-mail-smtp/) is a documented route. Its complete logging, alerts and backup features include [Pro-only capabilities](https://wordpress.org/plugins/wp-mail-smtp/); inspect the actual edition.
4. Alternatively, follow [Resend's SMTP setup](https://resend.com/docs/send-with-wordpress-smtp): `smtp.resend.com`, port `465`, SSL, authentication enabled, username `resend`, password supplied as a securely stored Resend API key. This is not the human mailbox password.
5. Test entry persistence, provider records and failure recovery separately. [FluentSMTP](https://wordpress.org/plugins/fluent-smtp/) offers another maintained implementation, including supported OAuth/API connections, logs, manual resending and fallback. These features do not establish durable retries or duplicate prevention automatically.

[wp_mail returning true](https://developer.wordpress.org/reference/functions/wp_mail/) does not prove recipient delivery. If retries depend on [WP-Cron](https://developer.wordpress.org/plugins/cron/), account for its page-load trigger; configure dependable scheduling where required. Document manual daily reconciliation as a limitation when automatic recovery is absent.

## 2. Configure sender identity

For visitor `buyer@example.net`, use:

| Field | Internal notification | Optional visitor receipt |
|---|---|---|
| From | `Website <forms@mail.example.com>` | Same authenticated sender |
| To | Fixed `sales@example.com` | Validated visitor address |
| Reply-To | Validated visitor address | `sales@example.com` |
| Subject | Server-generated inquiry reference | Fixed receipt subject plus reference |

Validate email syntax, length and control characters; this does **not** establish address ownership. Never impersonate the visitor through From. Reject client-selected recipients, Bcc and raw headers. Escape content; default to no attachments. Prevent receipts from becoming arbitrary-address spam relays.

For Resend, REST uses `reply_to`; its Node SDK uses `replyTo`. Consult the [send API](https://resend.com/docs/api-reference/emails/send-email) and installed SDK types. Keep marketing traffic separately governed. Sender-domain verification does not create a human inbox.

## 3. Apply the Resend example carefully

Require a customer-owned account, verified sending domain and protected application credential. Resend states that [production approval is not required](https://resend.com/docs/knowledge-base/does-resend-require-production-approval). Do not invent a sandbox-removal procedure or guarantee mainland-China signup, billing or account eligibility; check current terms and actual access.

Add `mail.example.com` using the exact dashboard records. [Current DNS guidance](https://resend.com/docs/knowledge-base/how-do-i-avoid-conflicting-with-my-mx-records) allows CNAME-based sending configuration for some domains created after August 2026. Do not hardcode historical MX/TXT values. Preserve root-domain receiving MX; enabling Resend receiving is a separate decision.

Prefer an application-specific sending credential with available domain restrictions. Keep key values in approved secret storage, outside frontend bundles, chat and source control.

## 4. Persist before notifying

Commit the inquiry and outbox notification atomically, or verify an equivalent platform guarantee. Only then acknowledge receipt with a reference. A background Promise or process-local queue is insufficient.

- Enforce unique submission keys and payload fingerprints. Reject the same key with different content. Uniquely identify each intended notification.
- Freeze the outbound payload. Store attempt count, next attempt, worker lease, provider message ID and status timestamps. Claim jobs atomically across workers.
- Apply bounded backoff for transient failures; honor applicable `Retry-After`. Stop permanent authentication/domain/payload errors and alert an operator.
- Resend [idempotency keys](https://resend.com/docs/dashboard/emails/idempotency-keys) last **24 hours**. API uses `Idempotency-Key`; SMTP supports `Resend-Idempotency-Key`. Verify that the chosen integration actually supplies it. Beyond the window, reconcile ambiguous acceptance before resending or changing providers.
- Separate API-submission retries from the provider's recipient-delivery retries. A delayed webhook is not permission to create another email.

If storage fails, preserve input and show a retry/copy-address fallback without success. If notification fails after persistence, retain the inquiry for operator handling. Alert on stalled jobs and permanent failures through an independent channel.

## 5. Validate requests and events

Bound fields and body size, validate server-side, use shared rate limiting, trust only documented proxy headers, and apply appropriate origin/CSRF controls. CORS is not bot protection.

When using [Turnstile](https://developers.cloudflare.com/turnstile/get-started/server-side-validation/), validate tokens server-side and check expected hostname/action. Tokens expire after 300 seconds; replay detection is eventually consistent, so retain database idempotency. China-domain widgets require their documented Siteverify domain, not a switch inferred from visitor location.

[Verify Resend webhooks](https://resend.com/docs/webhooks/verify-webhooks-requests) against the raw body, signing secret and timestamp using supported libraries. Persist and deduplicate `svix-id`; associate provider message IDs. Acknowledge after durable processing, tolerate reordered events, and avoid regressing delivered/complaint facts. Return failure when persistence fails so retries remain possible.

## 6. Record acceptance honestly

Start each check as **NOT_RUN**. Attach sanitized evidence, timestamp, observer and remediation owner:

- Mailto/copy works or degrades clearly on desktop/mobile.
- Valid submission creates one durable inquiry and notification; repeated/concurrent requests do not duplicate them.
- Invalid input, forged bot tokens and rate-limit tests cause no unauthorized messages.
- Provider outage preserves entries; retries, ambiguous timeouts and expired idempotency windows recover safely.
- Forged/repeated/reordered webhooks are handled correctly; queue failure produces an independent alert.
- Authorized external recipients confirm receipt, correct Reply-To and an actual human reply; inspect spam/quarantine and authentication headers.

Distinguish saved, provider-accepted, recipient-server-delivered and operator-replied. [Delivered events](https://resend.com/docs/webhooks/event-types) do not establish inbox placement, reading or completed business follow-up. Do not mark missing recovery capabilities PASS.
