# DHAKA SHOP

A colorful Bangladesh-focused multi-category e-commerce storefront built with Next.js, Tailwind CSS, Supabase and Vercel.

## Local setup

1. Create a Supabase project and run `supabase/schema.sql` in its SQL Editor.
2. Create an administrator in Supabase Authentication > Users, then add the user UUID to `public.admins`.
3. Copy `.env.example` to `.env.local` and configure the Supabase URL, publishable key, secret key and WhatsApp number.
4. Run `npm install` and `npm run dev`.

Never commit `.env.local` or expose `SUPABASE_SECRET_KEY` or `SSLCOMMERZ_STORE_PASSWORD` to browser code.

## Checkout and payments

- Cash on Delivery (COD) is supported.
- Online checkout uses the SSLCOMMERZ hosted payment session flow.
- The application validates transactions server-side through the SSLCOMMERZ validation API and also exposes an IPN endpoint.
- Risk-level transactions are routed to manual review instead of being marked paid automatically.
- Sandbox credentials must be used for testing. Live payments require merchant approval and live credentials.

Configure these Vercel environment variables:

- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`
- `SUPABASE_SECRET_KEY`
- `NEXT_PUBLIC_APP_URL`
- `NEXT_PUBLIC_WHATSAPP_NUMBER`
- `SSLCOMMERZ_STORE_ID`
- `SSLCOMMERZ_STORE_PASSWORD`

After deployment, configure the SSLCOMMERZ store IPN URL as:

`https://YOUR-VERCEL-DOMAIN.vercel.app/api/payments/sslcommerz/ipn`

See `supabase/sslc-commerz-notes.md` for integration notes.

## Before production

This is an initial implementation, not yet production-certified. Verify the full sandbox callback flow, add stock reservation expiry/release for abandoned or failed online checkouts, implement checkout rate limiting/CAPTCHA, and complete shipping, returns, privacy and merchant-policy configuration before live launch.
