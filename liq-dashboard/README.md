# LiqDepth — Equity Perp Liquidity Monitor

Live slippage dashboard for Hyperliquid HIP-3, Lighter, and Orderly equity perp markets.

## What it does

- Fetches live order books from all 3 venues every 15s (configurable)
- Computes real slippage for market buys at $1K / $5K / $10K / $25K / $50K
- Highlights the best venue per asset per trade size
- Auto-refreshes with a countdown timer

## Deploy to Vercel (5 minutes, free)

### Option A — Vercel CLI (fastest)

```bash
npm i -g vercel
vercel
```

Follow the prompts, accept defaults. You'll get a URL like:
`https://liq-dashboard-yourteam.vercel.app`

Share that link with your team.

### Option B — Vercel Dashboard (no CLI)

1. Go to https://vercel.com and sign in (or create a free account)
2. Click **Add New → Project**
3. Click **"Import Third-Party Git Repository"** or drag-and-drop this folder
4. Leave all settings as default → click **Deploy**
5. Done — share the URL Vercel gives you

## Project structure

```
liq-dashboard/
├── vercel.json          # Routing config
├── public/
│   └── index.html       # Dashboard frontend
└── api/
    ├── hyperliquid.js   # Proxy → api.hyperliquid.xyz
    ├── lighter.js       # Proxy → mainnet.zklighter.elliot.ai
    └── orderly.js       # Proxy → api-evm.orderly.network
```

## Why the proxy?

Browser CORS policies block direct calls to some exchange APIs.
The `/api/*` serverless functions run on Vercel's servers (no CORS issue)
and forward the data to the frontend. All three venues will show **LIVE** status.

## Customisation

- **Add tickers:** Edit `EQUITY_TICKERS` array in `public/index.html`
- **Change trade sizes:** Edit `ALL_SIZES` array in `public/index.html`
- **Change refresh default:** Edit the `selected` option in the interval dropdown
