# PayPilot AI — real transaction records (next phase)

## What changed
- Added `lib/transactions.ts` to store only server-confirmed, completed PayPal captures.
- Added `GET /api/transactions` to return saved transaction records without caching.
- PayPal capture route saves a transaction only after PayPal returns both order and capture status `COMPLETED`.
- Capture ID is used to avoid duplicate rows on retry.
- Dashboard transaction table now loads saved records from the API, with search/filter and honest loading/empty/error states. Hardcoded demo transactions were removed.
- Local transaction data is stored in `data/transactions.json` and ignored by Git.

## Setup
1. Keep your existing `.env.local` file in the project root. It is not included in this archive.
2. Ensure `PAYPAL_CLIENT_ID` and `PAYPAL_CLIENT_SECRET` are configured for Sandbox. Optional `PAYPAL_BASE_URL` defaults to `https://api-m.sandbox.paypal.com`.
3. Run `npm install` if needed, then `npm run dev`.
4. Complete a Sandbox payment through the app. Once PayPal confirms the capture as `COMPLETED`, the record is saved and should appear in the transaction table.
5. `GET /api/transactions` can be used to inspect the app's own saved records during local development. Do not expose it as a public multi-user financial ledger without authentication/authorization.

## Storage and deployment limitations
This phase uses a small JSON file for local development so it requires no new dependency or database credentials. It is persistent across local app restarts, but it is **not suitable for multi-instance/serverless production** (concurrent writes, backups, user isolation, and database transactions are not provided). Before production, replace this adapter with PostgreSQL or another managed database, add migrations and authentication/tenant scoping, and verify records through PayPal webhooks. Never treat browser query parameters or client-side UI state as payment confirmation.

## Validation
Static source/structure checks are included in the delivery process. A live PayPal Sandbox test requires your private credentials and was not performed here.
