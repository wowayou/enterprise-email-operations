# Enterprise email acceptance register

Project / domain / tenant / date / tester:

Statuses: PASS, FAIL, BLOCKED, NOT_RUN, N/A. N/A requires a reason. Unperformed checks remain NOT_RUN.

| ID | Check | Expected evidence | Status | Actual result / timestamp / evidence | Owner / next action |
|---|---|---|---|---|---|
| A01 | Ownership and recovery | Owner controls registrar, DNS and tenant; independent recovery | NOT_RUN | | |
| A02 | Access and MFA | Individual accounts; delegated roles; recovery demonstration | NOT_RUN | | |
| A03 | Role address | Inbound, correct reply identity, backup and sent visibility | NOT_RUN | | |
| A04 | DNS | Exact MX; one SPF within limits; enabled DKIM; assessed DMARC | NOT_RUN | | |
| A05 | Direct stream authentication | Recipient-trusted SPF/DKIM/DMARC per sender | NOT_RUN | | |
| A06 | Message round trip | External inbound → human response → external receipt | NOT_RUN | | |
| A07 | Recipient matrix | Actual-market providers, timing and folder placement | NOT_RUN | | |
| A08 | Website email entry | Address, mailto, copy fallback, keyboard/mobile | NOT_RUN | | |
| A09 | Form round trip | Durable record → notification → response → receipt | NOT_RUN | | |
| A10 | Notification outage | Record survives; retry, alert and recovery | NOT_RUN | | |
| A11 | Persistence outage | No success; useful retry/fallback; input retained | NOT_RUN | | |
| A12 | Duplicates and abuse | Durable idempotency; rate limits; safe fixed recipients | NOT_RUN | | |
| A13 | Webhooks if used | Signature checks, event dedupe, state handling | NOT_RUN | | |
| A14 | Failure visibility | Bounce, reject, quarantine and queue error assigned | NOT_RUN | | |
| A15 | Migration if used | Data and permissions reconciled; old service retained | NOT_RUN | | |
| A16 | Offboarding and restore | Revoked access; business continuity; restore evidence | NOT_RUN | | |
| A17 | Ongoing ownership | Renewal, report/queue review and response targets | NOT_RUN | | |

## Sign-off

- Production ready / limited pilot / blocked:
- Unresolved items and accountable owners:
- Next review date:
- Business owner / implementer acknowledgements:

Keep customer bodies and credentials out of public evidence. Refer to authorized private redacted artifacts.
