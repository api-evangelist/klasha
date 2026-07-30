---
name: Swap currency between Klasha merchant wallets
description: Quote and execute a conversion between two merchant wallet currencies at internal Klasha rates, then look the swap up by reference or quote token.
api: https://developers.klasha.com/transfers/swap-api
method: generated
source: https://developers.klasha.com/transfers/swap-api
operations:
  - POST /wallet/swap/generate/quote
  - POST /wallet/swap/initiate
  - GET /wallet/swap/fetch/by/reference/{transactionReference}
  - GET /wallet/swap/fetch/by/token/{quoteToken}
---

# Swap currency between Klasha merchant wallets

## Before you start

- Base URL: sandbox `https://dev.kcookery.com`, production `https://gate.klasapps.com`.
- Auth headers: `x-auth-token` (merchant public key) and `Authorization: Bearer <token>`.
- Klasha documents that swap requests must be encrypted, using the same Triple-DES/CBC
  PKCS5Padding Base64 scheme as payouts (`authentication/klasha-authentication.yml`).

## Steps

1. **Generate a quote** — `POST {{env_url}}/wallet/swap/generate/quote` with
   `sourceCurrency`, `destinationCurrency` and `sourceAmount`. Optionally send
   `destinationAmount`, and `mode: "SOURCE"` to price from the source amount. The
   response returns `rate`, `sourceFees`, `destinationFees`, `transactionReference` and
   a `quoteToken`.
2. **Show the quote to the operator** and decide. The quote is the priced offer; the swap
   has not moved money yet.
3. **Confirm the swap** — `POST {{env_url}}/wallet/swap/initiate` with the `quoteToken`
   from step 1. This converts the quote into a transaction.
4. **Look the swap up later** by either handle:
   - `GET {{env_url}}/wallet/swap/fetch/by/reference/{{transactionReference}}`
   - `GET {{env_url}}/wallet/swap/fetch/by/token/{{quoteToken}}`
   Read `transactionStatus` for the outcome.

## Notes

- Swaps are one of the documented wallet funding methods for NGN, KES, ZAR, USD and ZMW.
- There is no idempotency key; if you do not get a response to `initiate`, fetch by the
  quote token before retrying, or you risk a second conversion.
