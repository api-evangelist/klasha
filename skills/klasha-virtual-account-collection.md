---
name: Collect funds through a Klasha virtual account
description: Provision an NGN or GHS virtual account for a customer, receive bank transfers into it, and poll or reconcile the resulting collection.
api: https://developers.klasha.com/bank-account-collection/virtual-account-creation
method: generated
source: https://developers.klasha.com/bank-account-collection/virtual-account-creation
operations:
  - POST /wallet/virtual/v3/business/create/account
  - GET /wallet/virtual/v2/account/{email}
  - POST /nucleus/tnx/collection/status
---

# Collect funds through a Klasha virtual account

## Before you start

- Base URL: sandbox `https://dev.kcookery.com`, production `https://gate.klasapps.com`.
- Auth headers: `x-auth-token` (merchant public key) and `Authorization: Bearer <token>`.
- Virtual accounts are documented for **NGN and GHS only**.

## Steps

1. **Create the virtual account** — `POST {{env_url}}/wallet/virtual/v3/business/create/account`
   with `currency` (NGN or GHS) and `email`. For an individual account also send
   `firstName` and `lastName`. The response carries `accountNumber`, `accountName`,
   `bankName`, `bankCode`, `businessId`, `enabled` and the reference set
   (`orderRef`, `txRef`, `flwRef`).
2. **Give the account details to the payer** and have them transfer into it.
3. **Requery the account** at any time with
   `GET {{env_url}}/wallet/virtual/v2/account/{{email}}` — the email is the lookup key,
   so store it alongside the customer record.
4. **Confirm an inbound collection** — `POST {{env_url}}/nucleus/tnx/collection/status`
   with `{"gateRef": "<bank session id>"}`. The response returns the
   source/destination currency and amount pair, `status`, and the `customer` object.
5. **Reconcile on the webhook** — funded virtual accounts raise the standard
   `charge.completed` event. See `asyncapi/klasha-webhooks.yml`.

## Related

- Balance and statement endpoints: https://developers.klasha.com/bank-account-collection/va-balance-and-statement
- Business identification service: https://developers.klasha.com/bank-account-collection/business-identification-service
- Entity shapes: `data-model/klasha-data-model.yml`
- Error envelopes: `errors/klasha-problem-types.yml`
