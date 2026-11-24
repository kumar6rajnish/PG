# PayKaro: dummy payment gateway

A static, front-end-only practice gateway (cards, UPI, net banking) that accepts test credentials only.
No backend, no build step: `index.html` is the whole app.

## Deploy to Vercel (free Hobby plan)

### Option A: GitHub + Vercel dashboard (auto-redeploys on every push)
1. Create a new GitHub repo and push this folder (`index.html` must be at the repo root).
2. Go to vercel.com and sign in with GitHub.
3. Add New, then Project, and import the repo.
4. Framework Preset: **Other**. Leave Build Command and Output Directory empty.
5. Click Deploy. You get a `https://<name>.vercel.app` URL.

### Option B: Vercel CLI
```bash
npm i -g vercel
cd paykaro-vercel
vercel login
vercel          # first run: link/create the project, accept the defaults (no build)
vercel --prod   # publish to the production URL
```

## Test credentials
- Cards: any future expiry, any CVV, OTP `123456`. Example: `4111 1111 1111 1111` (success), `4000 0000 0000 0002` (declined).
- UPI: `success@paykaro`, `failure@paykaro`, `pending@paykaro`, `timeout@paykaro`
- Net banking: `testuser` / `test123`
- Full list is in the app's Test data tab.

## Playwright hooks
Every control has a `data-testid`. Each payment fires `window` event `paykaro:result` and sets
`document.body.dataset.lastStatus` to `success` or `failed`.
