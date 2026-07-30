# Klasha

Klasha is a cross-border payments company for emerging markets that lets international businesses sell into Africa and accept payments online in local African currencies. The platform covers payment collection (cards, bank transfer, USSD, M-Pesa and mobile money, Klasha wallet), payouts to bank accounts and mobile money wallets across Africa and to China, currency swap between merchant wallets, virtual account creation, payment links, and an embeddable JavaScript checkout.

- Website: https://www.klasha.com
- Developer portal: https://developers.klasha.com/
- Status: https://status.klasha.com/
- Dashboard: https://dashboard.klasha.com/signup

Backed by: seedcamp

## APIs

| API | Docs |
|---|---|
| Klasha Payments API | https://developers.klasha.com/accepting-payments/payments-api |
| Klasha Payout API | https://developers.klasha.com/transfers/payout |
| Klasha Swap API | https://developers.klasha.com/transfers/swap-api |
| Klasha Virtual Account API | https://developers.klasha.com/bank-account-collection/virtual-account-creation |
| Klasha Payment Link API | https://developers.klasha.com/accepting-payments/payment-link/payment-link-api |

## Artifacts in this repo

| Artifact | Path | Method |
|---|---|---|
| Authentication | `authentication/klasha-authentication.yml` | searched |
| Packages / SDKs | `packages/klasha-packages.yml` | searched |
| Embedded components | `components/klasha-components.yml` | searched |
| Sandbox / test data | `sandbox/klasha-sandbox.yml` | searched |
| API conventions | `conventions/klasha-conventions.yml` | searched |
| Error catalog | `errors/klasha-problem-types.yml` | searched |
| Lifecycle | `lifecycle/klasha-lifecycle.yml` | searched |
| Webhooks | `asyncapi/klasha-webhooks.yml` | searched |
| Data model | `data-model/klasha-data-model.yml` | searched |
| Conformance | `conformance/klasha-conformance.yml` | searched |
| llms.txt | `llms/klasha-llms.txt` | searched (verbatim) |
| Trust center | `security/klasha-trust-center.yml` | searched |
| Domain security | `security/klasha-domain-security.yml` | probed |
| Well-known | `well-known/klasha-well-known.yml` | searched (none published) |
| MCP server | `mcp/klasha-mcp.yml` | derived (candidate) |
| Agent skills | `skills/` | generated |

## Notes

Klasha publishes no OpenAPI, AsyncAPI, GraphQL or Protobuf description, no `/.well-known/`
discovery documents, no dated changelog, no CLI, no OAuth scope surface, no published
rate limits and no vulnerability disclosure program. It does publish PCI DSS compliance
and ISO 27001 certification, a status page, a real `llms.txt`, first-party web and mobile
SDKs, e-commerce plugins, and a documented webhook surface.
