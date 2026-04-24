# TrueMarketing — Claude Code Project Context

## What This Is
BSV blockchain messaging SaaS. Users seal messages permanently on-chain
via OP_RETURN transactions. Solo operator. South Africa. Live business.

## The Proven ROI
December 2025: 216 blockchain sends, R0.43 total fees → R24,785 revenue.
64,599% ROI. All verified on WhatsOnChain. This is the core sales story.

## Project Structure
```
truemarketing/
├── app/
│   ├── index.html          ← End-user app (deploy to Netlify)
│   └── wallet-beta.html    ← Standalone beta wallet for testers
├── bsv-server/
│   ├── server.js           ← Node.js BSV signing server (deploy to Railway)
│   ├── package.json
│   ├── railway.toml
│   ├── .env.example        ← Template — never commit actual .env
│   └── test.js             ← Full test suite (44 tests)
├── owner/
│   └── dashboard.html      ← Owner-only: ROI tracker, MDE, faucet queue
└── CLAUDE.md               ← This file
```

## Key Architecture
- **Non-custodial**: Each user gets their own BSV address on signup
- **Faucet model**: Owner sends 50,000 sats ($0.27) to each new user
- **OP_RETURN**: Every sealed message written permanently to BSV blockchain
- **Single signing wallet**: Owner's WIF key in Railway env vars signs all TXs
- **ROI tracking**: All sats in/out flow through one address = permanent P&L

## The Three Files That Matter
1. `app/index.html` — What users see. 4-screen flow: auth → home → seal → certificate
2. `owner/dashboard.html` — What you see. ROI tracker, faucet queue, MDE campaigns
3. `bsv-server/server.js` — The blockchain bridge. Signs and broadcasts all TXs

## Server Endpoints
- `POST /api/broadcast`  — seal a message on-chain
- `POST /api/faucet`     — send 50K sats to new user (owner-only, needs OWNER_SECRET)
- `GET  /api/health`     — status + wallet balance + faucet capacity
- `GET  /api/price`      — live BSV/USD price from WhatsOnChain
- `GET  /api/tx/:txid`   — verify a TX on WhatsOnChain

## Environment Variables (Railway)
```
BSV_WIF_KEY     = WIF key from Exodus wallet (starts with K or L)
OWNER_SECRET    = secret password protecting /api/faucet
BSV_NETWORK     = mainnet
FAUCET_SATS     = 50000
FEE_SATS        = 200
ALLOWED_ORIGIN  = https://your-netlify-url.netlify.app
PORT            = 3001
```

## Connecting Frontend to Server
In both index.html and dashboard.html, find and update:
```javascript
const SERVER_URL = null; // ← change to Railway URL
// becomes:
const SERVER_URL = 'https://your-server.up.railway.app';
```

## Wallet Setup
- **Exodus Desktop** for the hot signing wallet (export WIF key → Railway)
- **AltCoinTrader** (altcointrader.co.za) to buy BSV with ZAR — only SA exchange with BSV/ZAR
- **VALR does not list BSV** — use AltCoinTrader instead
- Keep only 2–4 weeks of float in hot wallet

## Pricing / Plans
- Starter: $9/mo — 50K sats credits
- Pro: $27/mo — 200K sats credits
- Business: $55/mo — 500K sats credits
- CAC: $0.27 per user (50K sats faucet deposit)
- Break-even: 4 paying users

## Target Market (Priority Order)
1. Attorneys & law firms (highest willingness to pay)
2. Property professionals
3. Freelancers & contractors
4. HR & recruitment
5. Construction & trades

## NEVER DO
- Commit .env or any WIF key to git
- Add December 2025 campaign data back into analytics (starts fresh)
- Use "satoshi", "BSV", "OP_RETURN", "WIF" in user-facing copy
- Make dashboard.html public (owner only, run locally)

## Plain Language Replacements
| Technical term | User-facing language |
|---|---|
| Satoshis / BSV | Credits |
| OP_RETURN | Permanent seal |
| Blockchain | Permanent record |
| SHA-256 hash | Digital fingerprint |
| Transaction ID | Proof reference |
| WIF key | (never show users) |

## Deployment Stack
- **Railway** — Node.js server ($5/mo)
- **Netlify** — app/index.html (free, drag-and-drop deploy)
- **Exodus** — hot signing wallet (local, desktop)
- **AltCoinTrader** — buy BSV with ZAR

## Running Costs
~R95/month total (Railway $5 + domain ~R18)

## Demo Credentials (for testing)
- User: demo@truemarketing.co.za / demo123
- Owner: owner@truemarketing.co.za / owner123 / 2FA: 123456

## Common Tasks for Claude Code
- "Update SERVER_URL in both HTML files to [URL]"
- "Run the test suite and fix any failures"
- "Add a new subscription tier at $X/mo with Y sats"
- "Check server.js for security issues"
- "Update ALLOWED_ORIGIN to restrict to my Netlify domain"
- "Generate a git commit message for these changes"
- "Create a deploy checklist for Railway"
