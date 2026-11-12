# PayPilot AI — Payment reliability phase

This patch builds on the supplied PayPilot AI project and keeps its existing UI and routes.

## Implemented
- PayPal create-order requests now require a client-generated UUID and send it as `PayPal-Request-Id`, so a retried create request can be idempotent at PayPal.
- PayPal capture requests send a stable per-order `PayPal-Request-Id` to reduce duplicate capture risk when the success page retries or React Strict Mode runs effects more than once.
- The capture endpoint only reports success when PayPal returns both order and capture status as `COMPLETED`.
- Existing PayPal Sandbox redirect and success/cancel UI remain in place.

## Existing setup
Keep your existing `.env.local` unchanged. Required server-side variables are `PAYPAL_CLIENT_ID` and `PAYPAL_CLIENT_SECRET`. `PAYPAL_BASE_URL` is optional and defaults to PayPal Sandbox. Never expose the secret in client code or commit it.

## Apply
1. Back up `D:\paypilot-ai`.
2. Extract the full ZIP over the existing project, preserving folder structure.
3. Keep `.env.local` in place.
4. Restart with `npm run dev` and test using PayPal Sandbox buyer credentials.

## Important: transaction persistence is not enabled yet
The uploaded source does not contain a configured database or transaction repository. This phase deliberately does not pretend the demo dashboard rows are real, and does not write payment records to an unsafe local JSON file. A database choice and credentials/schema are needed before completed captures can become durable transaction history. The capture API response is verified against PayPal, but it is not yet persisted to a database or available as real dashboard history.

## Validation
Static source checks are included in the build notes; PayPal API calls still need to be exercised against your Sandbox credentials.
