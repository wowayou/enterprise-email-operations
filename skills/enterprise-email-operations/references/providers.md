# Provider selection and onboarding

Baseline: **2026-11-27**. Recheck regional eligibility, current plans and authentication rules before implementation. Treat recommendations below as starting points; require evidence from the customer's actual tenant and networks. Follow SKILL.md for authorization, DNS change control, migration and acceptance.

## Choose by operating context

| Situation | Suggested starting point |
|---|---|
| Small mainland team needing domain email and standard clients | Evaluate a paid Zoho Mail China plan. |
| Existing Alibaba Cloud administration and preference for domestic procurement/support | Evaluate Alibaba Mail China. Check current seat requirements. |
| Outlook, delegated role addresses and structured administration | Evaluate Exchange Online; consider 21Vianet for mainland operations. |
| Established international Microsoft tenant or overseas Google collaboration | Retain the established environment if mainland access, billing and required features pass testing. |
| Working Tencent, NetEase or another existing provider | Audit and retain it when acceptance passes; avoid migration without a demonstrated need. |

Separate human mailboxes from website notification delivery. Neither registration success nor “international email” marketing guarantees reliable access or inbox placement.

## Microsoft 365 / Exchange Online

1. **Select the cloud and subscription first.** Use [Microsoft's China offers](https://www.microsoft.com/zh-cn/microsoft-365/business-china-offers) for the official purchase route. Consult the [21Vianet service description](https://learn.microsoft.com/office365/servicedescriptions/office-365-platform-service-description/microsoft-365-operated-by-21vianet). China-operated and global tenants have different operations, endpoints and feature availability. Do not copy global settings into China. Microsoft documents [mainland connectivity risks for global tenants](https://learn.microsoft.com/en-us/microsoft-365/enterprise/microsoft-365-networking-china?view=o365-worldwide).
2. **Have the owner establish administrative access.** Follow the [business signup guide](https://learn.microsoft.com/en-us/microsoft-365/admin/simplified-signup/signup-business-standard?view=o365-worldwide) or the purchased China subscription's setup route. Record the tenant/cloud, customer-controlled recovery and billing. Choose Exchange Online or a suite including it; Microsoft 365 Apps for business alone does not include email.
3. **Verify the domain, then provision recipients.** Follow [Add a domain](https://learn.microsoft.com/en-us/microsoft-365/admin/setup/add-domain?view=o365-worldwide). Create/license users and role addresses before changing MX. Confirm each wizard's DNS changes instead of accepting automatic cutover blindly.
4. **Configure shared access deliberately.** A [shared mailbox](https://learn.microsoft.com/en-us/microsoft-365/admin/email/about-shared-mailboxes) generally needs no separate license up to 50 GB, but accessing members need licensed Exchange Online mailboxes. Advanced retention/archive requirements may change licensing. Block direct sign-in; configure appropriate read/send rights and shared sent-item copies. Verify China-plan availability.

**SMTP:** The [January 2026 revised timeline](https://techcommunity.microsoft.com/blog/exchange/updated-exchange-online-smtp-auth-basic-authentication-deprecation-timeline/4489835) leaves Basic SMTP AUTH behavior unchanged through December 2026. At December's end, existing tenants default to disabled but administrators can re-enable it; subsequently created tenants default to unavailable. Final removal timing is scheduled to be announced in the second half of 2027. Recheck before implementation.

[Security defaults disable SMTP AUTH](https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission); OAuth alone does not bypass that policy. Prefer a reviewed API or transactional-mail design over weakening tenant security. [Graph sendMail](https://learn.microsoft.com/en-us/graph/api/user-sendmail?view=graph-rest-1.0) supports the China cloud with its corresponding endpoints. Scope permissions; `202 Accepted` is not delivery confirmation.

## Google Workspace

1. **Establish eligibility and practical access separately.** The [availability page](https://knowledge.workspace.google.com/admin/support/troubleshooting/countries-or-regions-where-google-workspace-is-available) does not establish guaranteed mainland signup, payment or connectivity. Check [payment options by country](https://knowledge.workspace.google.com/admin/billing/payment-options-in-my-country). Use the real business billing location; never substitute an invented overseas address. Test the actual office/mobile environment before committing to migration.
2. **Register the organization and protect the owner administrator.** Follow [organization setup](https://knowledge.workspace.google.com/admin/getting-started/set-up-google-workspace-for-your-organization); establish recovery and two-step verification. Check account-specific administrator enforcement notices.
3. **Verify the domain, create licensed users and role destinations, then activate Gmail.** Follow the [MX guide](https://knowledge.workspace.google.com/admin/domains/set-up-mx-records-for-google-workspace). Current onboarding uses `smtp.google.com`; older tenants may retain legacy MX. Use the active wizard.
4. **Select the collaboration model.** Compare [mailbox delegation](https://knowledge.workspace.google.com/admin/users/delegate-a-users-email-address) with [Groups Collaborative Inbox](https://support.google.com/a/users/answer/9259857?hl=en). An alias is not a delegatable account. Check licensing, external posting permissions and reply identity; do not share one user's credentials among staff.

Since May 2025, ordinary password-only [less-secure app access](https://knowledge.workspace.google.com/admin/apps/control-access-to-less-secure-apps) is unsupported. Prefer OAuth; use application passwords or SMTP relay only when the specific [device/application guidance](https://knowledge.workspace.google.com/admin/gmail/send-email-from-a-printer-scanner-or-app) and tenant policy permit them.

## Zoho Mail

1. **Choose the region explicitly.** Enter through [Zoho Mail China](https://www.zoho.com.cn/mail/) or the appropriate international site. Record the organization's data center. [Cross-data-center migration](https://help.zoho.com/portal/en/kb/accounts/manage-your-zoho-account/articles/dc-migration) requires assessment and coordination, not a different login URL.
2. **Choose the required plan.** China's [subscription guide](https://www.zoho.com.cn/mail/help/adminconsole/subscription.html) describes free service as web-only. Do not promise IMAP/POP or equivalent international features on a free China account.
3. **Follow [hosting setup](https://www.zoho.com/mail/help/adminconsole/email-hosting-setup.html):** establish the owner administrator, verify the domain, create users/groups, prepare migration, then configure provider-issued MX and authentication records.
4. **Configure clients from the account's [server configuration details](https://www.zoho.com/mail/help/imap-access.html).** Region and account type affect parameters. Enable permitted protocols and supported MFA/application-password access. Verify shared-mailbox availability in the selected China plan before promising assignment or shared history.

## Alibaba Mail China

Follow the mainland [purchase workflow](https://help.aliyun.com/zh/document_detail/36702.html), not international-site seat or billing assumptions. Have the owner choose the version/domain, complete purchase and establish the mailbox administrator. Follow [initial setup](https://help.aliyun.com/zh/document_detail/36698.html) to create employees, prepare migration and configure DNS. Distinguish the cloud account from `postmaster` mailbox credentials.

New purchases [restrict third-party clients by default](https://help.aliyun.com/zh/document_detail/606337.html). Allow only required users, enable needed protocols and use independently revocable client passwords. The [current server guide](https://help.aliyun.com/zh/document_detail/36576.html) specifies IMAP SSL 993 and SMTP SSL 465; SMTP 587 is not open. Verify overseas round trips rather than assuming worldwide delivery.

## Existing NetEase or Tencent accounts

Confirm current entitlements, recovery/MFA, custom-domain authentication, client access and team permissions through the actual account or official support. Treat historical NetEase “50 free accounts” material as unverified current entitlement. Do not infer free-plan security features from paid-plan documentation or reseller claims.
