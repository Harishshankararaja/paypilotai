# PayPilot AI — UPI / Razorpay Test Mode

## Included
- Keeps existing PayPal Sandbox checkout.
- Adds Razorpay order creation in INR, using server-side `RAZORPAY_KEY_ID` and `RAZORPAY_KEY_SECRET`.
- Adds Razorpay Checkout with UPI enabled (also allows card, netbanking and wallet methods where supported).
- Verifies checkout signature server-side and fetches the order/payment from Razorpay before accepting the payment.
- Saves verified captured Razorpay payments into the same local transaction JSON store as PayPal.
- Dashboard can filter saved records by PayPal or Razorpay/UPI and refreshes after successful verification.
- `.env.local` is intentionally not included in the ZIP.

## Setup
1. In your Razorpay account, use Test Mode keys. Add to your existing `.env.local` (do not share these values):
   ```
   RAZORPAY_KEY_ID=rzp_test_your_key_id
   RAZORPAY_KEY_SECRET=your_test_key_secret
   ```
2. Keep your existing PayPal Sandbox variables unchanged.
3. Run `npm install` if needed, then restart with `npm run dev`.
4. Open dashboard → Payment Playground → UPI / other methods.
5. Use a Razorpay-supported test payment flow. UPI options shown depend on your account and checkout configuration.

## Important
- This is Test Mode. Live payments require approved Razorpay account, live keys, and production readiness.
- This checkout includes UPI, cards, netbanking, and wallet options supported by Razorpay Checkout. It does not add separate direct integrations with Google Pay/PhonePe/Paytm; users can use those through supported UPI checkout options.
- Local transaction storage remains a JSON file and is not suitable for multi-instance/serverless production. Before production, use a managed database, authentication/tenant isolation, and verified webhooks.
- No private credentials are bundled. Live payment testing was not possible here.


## Troubleshooting "Unable to create Razorpay order"
- Confirm the file is exactly `D:\\paypilot-ai\\.env.local` (project root, beside `package.json`).
- The key ID must start with `rzp_test_`; the secret must be the matching Test Mode secret from the same Razorpay account.
- Do not add quotes unless your existing env parser setup requires them; avoid spaces around values.
- After changing `.env.local`, stop and restart the server (`Ctrl+C`, then `npm run dev`). Next.js does not reliably reload environment values in a running process.
- The order route now returns a clearer safe error and logs the provider code/description to the terminal without printing credentials.
- Razorpay's official docs say API authentication failures commonly mean test/live key mismatch, expired key, or extra whitespace: https://github.com/razorpay/markdown-docs/blob/master/api/orders/create.md
