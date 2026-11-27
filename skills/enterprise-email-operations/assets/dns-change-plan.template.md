# DNS and mail change plan

Status: DRAFT. Do not publish placeholders.

- Domain / authoritative DNS / registrar:
- Provider / tenant region / plan / official setup page:
- Existing service and migration inventory:
- Authorized scope and maintenance window:
- Executor / accountable owner / recovery contact:
- Current record export and timestamp:
- Created and tested receiving destinations:
- Rollback owner / trigger / previous TTL waiting period:

| Exact DNS owner | Type | Existing full RRset | Proposed full RRset | Value source | Purpose | TTL | Verification | Rollback |
|---|---|---|---|---|---|---|---|---|
| Confirm owner | TXT | Collect | Tenant challenge | Active tenant | Ownership | Actual | Tenant and DNS | Assess retention |
| Confirm owner | MX | Collect | Exact tenant records | Active tenant | Receiving | Actual | Recipients exist; public DNS; inbound | Restore RRset; reconcile both inboxes |
| Envelope domain | TXT | Collect all SPF policies | One reviewed merged SPF policy | Sender inventory | Authorization | Actual | Recursive SPF check and real headers | Restore previous policy |
| selector._domainkey.domain | TXT or CNAME | Collect | Exact key/target | Active tenant | DKIM | Actual | Signing enabled; aligned signature | Retain old key for in-flight mail |
| _dmarc.author-domain | TXT | Collect | Assessed policy and verified report URI | Approved plan | DMARC | Actual | Single valid policy; alignment; reports | Restore prior working policy if warranted |

Preserve unrelated TXT and other records. Resolve same-name CNAME conflicts and duplicate SPF/DMARC policies. Multiple quoted chunks may belong to one logical TXT record.

## Cutover gates

- Receiving users, role addresses, permissions and licenses exist.
- Current and retained senders are authorized during transition.
- Historical data remains accessible; migration and restore are planned.
- Rollback is an assigned recovery action; messages do not automatically migrate back.
- Observers and authorized test recipients are available.

## Change result

Record timestamps, exact diff, tenant checks, public DNS evidence and observed acceptance. Keep failures and incomplete propagation unresolved.
