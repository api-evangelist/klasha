---
name: Pay out to an African bank account or mobile money wallet
description: Disburse funds from a Klasha merchant wallet to a bank account or mobile money wallet, including bank-code lookup, Triple-DES payload encryption, and settlement confirmation.
api: https://developers.klasha.com/transfers/payout
method: generated
source: https://developers.klasha.com/transfers/payout
operations:
  - GET /nucleus/business/api/wallets
  - GET /wallet/merchant/bank/transfer/request/banks/{currency}
  - POST /wallet/merchant/{businessId}/bank/transfer/v2/request
---

# Pay out to an African bank account or mobile money wallet

Klasha publishes no OpenAPI document; every step cites the documented endpoint and page.

## Before you start

- Base URL: sandbox `https://dev.kcookery.com`, production `https://gate.klasapps.com`.
- Every call needs `Content-Type: application/json`, `x-auth-token: <merchant public key>`
  and `Authorization: Bearer <token>`.
- **The payout payload must be encrypted.** Klasha requires Triple-DES/CBC with
  PKCS5Padding, Base64-encoded, and the ciphertext submitted as a single `message` field:
  `{"message": "<encrypted-request-body>"}`. This applies to payouts, mobile money
  payouts and swaps.
- There is no idempotency key. Supply your own unique `requestId` on the payload and
  reconcile on the `payout` webhook rather than blind-retrying.

## Steps

1. **Check the funding wallet** — `GET {{env_url}}/nucleus/business/api/wallets` returns
   the merchant wallet balances. Klasha wallets exist per currency (NGN, KES, ZAR, USD,
   ZMW, GHS) and are funded by collections, virtual accounts, or swaps.
2. **Look up the bank code** — `GET {{env_url}}/wallet/merchant/bank/transfer/request/banks/{currency}`
   for the destination currency, and use the returned code as `bankCode`.
3. **Build the transfer payload** with the documented fields: `amount`, `country`,
   `currency`, `bankCode`, `bankName`, `accountNumber`, `accountName`, `requestId`,
   `description`.
4. **Encrypt the payload** using Triple-DES as above.
5. **Submit the payout** — `POST {{env_url}}/wallet/merchant/{businessId}/bank/transfer/v2/request`
   with body `{"message": "<ciphertext>"}`.
6. **Confirm settlement** — Klasha sends a `payout` webhook whose `data.status` is
   `successful` or `failed`, carrying `reference`, `amount`, `currency`, `bankName`,
   `accountNumber` and `accountName`. If the webhook was not delivered, replay it with
   `GET {{env_url}}/nucleus/tnx/webhook?reference={{tx_ref}}`.

## Currency and rail notes

Klasha documents per-currency payout endpoints in a "new encryption" generation for ZAR,
NGN, GHS, KES, ZMW, TZS and CNY, and mobile money payout endpoints for ZMW, RWF, UGX,
GHS, NGN, XOF (Ivory Coast, Benin, Senegal, Burkina Faso), XAF (Cameroon, Gabon, Republic
of the Congo), CDF, TZS, MWK, MZN, KES and SLL. CNY payouts additionally support wallet
destinations (Alipay, WeChat). Pick the endpoint documented for your destination currency
rather than assuming one generic route.

## Testing

The sandbox publishes test phone/network pairs per currency for mobile money (see
`sandbox/klasha-sandbox.yml`). Klasha publishes no test bank accounts for payouts.
