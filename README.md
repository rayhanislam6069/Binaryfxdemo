# BinaryFX — mobile-first demo trading prototype

This project is a **demo/paper-trading UI**, not a real-money binary options platform. It streams public BTC/USDT or ETH/USDT spot trades from Binance and simulates CALL/PUT positions with a virtual $10,000 balance. It does not take deposits, process withdrawals, or execute financial trades. It is not certified production software and is not guaranteed bug-free.

## Included
- Next.js App Router + TypeScript + Tailwind CSS v4
- Mobile-first dark UI, responsive chart, asset selector, demo wallet, expiration controls, trade history
- Public Binance WebSocket market display
- Supabase PostgreSQL schema with RLS starter policies
- `/api/health` status endpoint
- `.env.example`

## Run locally
1. Install Node.js 20.9+ on a computer, or use a browser-based development environment on your phone.
2. Extract this ZIP and open the `BinaryFX` folder in a terminal.
3. Run:
   ```bash
   npm install
   cp .env.example .env.local
   npm run dev
   ```
4. Open `http://localhost:3000`. The live chart requires an internet connection and may be unavailable in some networks.

## Deploy from an Android phone (free Vercel path)
**Simplest route: GitHub + Vercel.** Vercel's import flow expects a Git repository; a direct ZIP upload is not the standard deployment path.
1. Extract the ZIP using your phone's Files app.
2. Open GitHub in Chrome, create a new empty repository named `binaryfx`, and choose the browser upload option. Upload the project files/folders from the extracted ZIP (do not upload `node_modules`).
3. Open `https://vercel.com` in Chrome and sign in.
4. Choose **Add New → Project**, import the `binaryfx` GitHub repository, then click **Deploy**. Framework should be detected as Next.js.
5. If you add environment variables later, enter them in Vercel → Project → Settings → Environment Variables, then redeploy. This demo works without Supabase variables.
6. Open the deployed URL on your phone. If you get a build error, open Vercel → Deployments → latest deployment → Build Logs and share the error text.

If browser file upload is awkward on mobile, use a cloud IDE such as Replit/GitHub Codespaces to upload/extract the ZIP and push the files to GitHub.

## Supabase (optional database foundation)
1. Create a Supabase project.
2. Open **SQL Editor**, paste `supabase/schema.sql`, and run it.
3. Copy the project URL and anon key into `.env.local` for local development or Vercel Environment Variables.
4. Never put `SUPABASE_SERVICE_ROLE_KEY` in a `NEXT_PUBLIC_*` variable or client-side code. The UI in this starter does not yet persist users/trades to Supabase.

## Important security and regulatory notes
A genuine real-money binary options service requires jurisdiction-specific legal review and licensing where applicable, KYC/AML and age/eligibility checks, responsible-use safeguards, market-data licensing, audited pricing and settlement, fraud controls, idempotent payment processing, monitoring, incident response, and independent security testing. Binary options are restricted or prohibited in many jurisdictions. Do not enable real-money trading or payments by simply adding a payment key.

For a future compliant implementation, design payment-provider webhooks with signature verification, idempotency keys, immutable ledger entries, reconciliation, and server-side-only balance updates. Use provider-supported merchant accounts and confirm the provider permits the product and jurisdiction. This repository intentionally omits automated debits, real-money settlement, and payment webhook crediting.

## Troubleshooting
- **Chart says Connecting:** confirm internet access and that the network allows `wss://stream.binance.com:9443`.
- **No trade can open:** wait for a live price and ensure the amount is at least $1 and within demo balance.
- **Build issue:** use Node.js 20.9 or newer; run `npm install` again and inspect the full build log.
