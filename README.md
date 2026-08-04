# Klasha

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
