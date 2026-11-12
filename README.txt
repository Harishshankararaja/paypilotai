# PayPilot AI final UI files

## Files
- `app/page.tsx` — dashboard UI
- `app/profile/page.tsx` — profile page
- `app/globals.css` — responsive styles
- `app/layout.tsx` — root layout and metadata
- `public/paypilot-mark.png` — standalone brand mark

## Install
1. Copy these files into the matching locations in your existing Next.js project. Back up your current files first.
2. Keep your existing `.env.local` private and do not overwrite it.
3. In `app/api/paypal/orders/route.ts`, remove `export const runtime = "nodejs";` if your `next.config.*` has `cacheComponents: true`. Node.js is the default runtime. Verify that the route uses the PayPal SDK, not an accidental Razorpay import.
4. Run `npm run dev`.

The dashboard is a UI starter. Its payment button is deliberately a placeholder and does not create a real order; connect it to your existing PayPal Sandbox API route. Demo transaction rows and profile data are placeholders, not live payment data.

Build fix: The dashboard page is a Server Component, so the PayPal placeholder button has no inline onClick handler. It is disabled until connected to a client-side checkout flow.
