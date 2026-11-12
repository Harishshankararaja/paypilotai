PayPilot AI — consolidated targeted fixes

Based on source files extracted from the uploaded paypilot-ai.zip. No .env.local, node_modules, or .next files are included.

What this patch addresses:
1. PayPal redirect: POST /api/paypal/orders creates a PayPal Sandbox CAPTURE order and returns its approval URL.
2. PayPal capture: success page captures the approved order using /api/paypal/orders/[orderId]/capture and reports the result.
3. Payment cancel route: /payment/cancel provides a clear cancellation state.
4. Next.js cacheComponents: removes the incompatible runtime export from the Razorpay verify route.
5. Theme toggle: header sun/moon control toggles light/dark theme and saves selection in localStorage.
6. Glass/aurora polish: glass transparency, blur, glossy highlights, edge glints, aurora glow and hover sheen.
7. Transaction search/filter: search and status dropdown filter the demo rows.
8. Navigation cleanup: removes the extra “Open profile” CTA and duplicate avatar; the brand mark/wordmark is the profile entry point on dashboard.
9. Keeps existing layout and PayPal environment variable names. No secret values included.

Apply:
- Extract this ZIP into D:\paypilot-ai and allow overwriting matching files.
- Keep .env.local as-is; do not share its contents.
- Restart with Ctrl+C then npm run dev.
- Test PayPal Sandbox using a Sandbox buyer account.

Limits:
- Dashboard transaction rows remain demo data; connect a database/API for live transactions.
- AI Assistant is a UI entry point, not connected to an AI backend.
- Payment redirect requires valid PAYPAL_CLIENT_ID / PAYPAL_CLIENT_SECRET and PAYPAL_BASE_URL (sandbox URL is the default).
- Code was reviewed but not run against your Sandbox credentials here.
