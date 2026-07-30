---
name: Collect a card payment with Klasha
description: Take a card payment in a supported African currency through Klasha, handle the PIN/OTP/3DS challenge, and verify the final state before giving value.
api: https://developers.klasha.com/accepting-payments/payments-api
method: generated
source: https://developers.klasha.com/accepting-payments/payments-api
operations:
  - POST /pay/aggregators/{gateway}/card/payment/v2
  - POST /pay/aggregators/{gateway}/charge/card/v2
  - POST /pay/aggregators/{gateway}/validate/card/v2
  - POST /nucleus/tnx/merchant/status
---

# Collect a card payment with Klasha

Klasha publishes no OpenAPI document, so every step below cites the documented HTTP
endpoint and the page it comes from. Do not invent endpoints or fields.

## Before you start

- Base URL is environment-specific: sandbox `https://dev.kcookery.com`, production
  `https://gate.klasapps.com` (`{{env_url}}` in the docs).
- Send both auth headers on every call: `x-auth-token: <merchant public key>` and
  `Authorization: Bearer <token>`. Get the bearer token from
  `POST {{env_url}}/auth/account/v2/login` with `username` (account email) and `password`;
  read it from `data.token`.
- `{{gateway}}` is the currency rail for the card payment, e.g. `NGN`, `ZAR`, `USD`.
- Generate `tx_ref` yourself as a UUID or another guaranteed-unique value. It comes back
  as `tnxRef` and is the only handle that ties the charge, the webhook and the status
  check together.
- Klasha does **not** support idempotency keys. A retry is a new attempt, so always check
  status before retrying (see `conventions/klasha-conventions.yml`).

## Steps

1. **Initiate the payment** — `POST {{env_url}}/pay/aggregators/{{gateway}}/card/payment/v2`.
   Include your unique `tx_ref` and the source/destination currency pair. Klasha models
   every transaction as `sourceCurrency`/`sourceAmount` converted at a `rate` to
   `destinationCurrency`/`destinationAmount`.
2. **Charge the card** — `POST {{env_url}}/pay/aggregators/{{gateway}}/charge/card/v2`.
3. **Validate the charge** — `POST {{env_url}}/pay/aggregators/{{gateway}}/validate/card/v2`
   when the card requires a PIN, OTP or 3DS challenge. In sandbox the test cards publish
   the exact PIN and OTP to submit (see `sandbox/klasha-sandbox.yml`).
4. **Verify before giving value** — `POST {{env_url}}/nucleus/tnx/merchant/status` with
   body `{"tnxRef": "<your tx_ref>"}`. Klasha explicitly instructs you to confirm both
   the amount and the destination currency, and that `status` is `successful`, before
   releasing goods or services. Never treat the client-side callback as authoritative.
5. **Reconcile asynchronously** — if a webhook URL is configured on the dashboard, Klasha
   also sends a `charge.completed` event with the same `tnxRef`. Use it to reconcile, not
   as the sole confirmation. See `asyncapi/klasha-webhooks.yml`.

## Error handling

Klasha returns HTTP 400 for documented failures regardless of failure class; the
discriminating detail is in the envelope text (`status`/`message`/`data`). Common cases:

- `public key is required` — the `x-auth-token` header is missing.
- `Authorization required` — the bearer token is missing or invalid; re-login.
- `Transaction not found.` — the `tnxRef` does not match a transaction; check you used
  the reference from the initiation call.

Full catalog: `errors/klasha-problem-types.yml`.

## Testing

Use the sandbox base URL and the published test cards, including the deliberate failure
cards (incorrect PIN, fraudulent, AVS decline, do-not-honour, insufficient funds), to
exercise both branches. Any future expiry date is accepted. All values are in
`sandbox/klasha-sandbox.yml`.
