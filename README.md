# REKW Stocks — stonks.rekw.com
Live market terminal dashboard with real-time Finnhub WebSocket streaming.

---

## First-Time Deploy to Railway

### Step 1 — Push to GitHub
```bash
git init
git add .
git commit -m "initial deploy"
git remote add origin https://github.com/YOUR_USERNAME/rekw-stocks.git
git push -u origin main
```

### Step 2 — Create Railway Project
1. Go to [railway.app](https://railway.app) and log in
2. Click **New Project** → **Deploy from GitHub repo**
3. Select `rekw-stocks`
4. Railway auto-detects Node.js and runs `npm start`
5. Wait for the green **Deployed** status

### Step 3 — Add Custom Domain in Railway
1. In your Railway project → **Settings** → **Networking** → **+ Custom Domain**
2. Type `stonks.rekw.com`
3. Click **Add**
4. Railway will show a popup with:
   - A **CNAME target** (looks like `xxxxxxxx.up.railway.app`)
   - A **TXT verification record** (looks like `railway-verify=abc123...`)
5. **Copy both values** before clicking anything

### Step 4 — Add DNS Records in Turbify
Go to your Turbify DNS panel for `rekw.com` and add:

**CNAME Record:**
| Field | Value |
|-------|-------|
| Source | `stonks` |
| Destination | *(the `.up.railway.app` value from Railway popup)* |

**TXT Record:**
| Field | Value |
|-------|-------|
| Host | `_railway-verify.stonks` |
| Text | *(the full `railway-verify=...` value from Railway popup)* |

### Step 5 — Verify in Railway
1. Click **Dismiss** in the Railway domain popup
2. Wait 2–5 minutes for DNS to propagate
3. Visit **stonks.rekw.com** — should be live!

---

## Updating the Site (Standard Process)

Whenever you update `public/index.html` (new dashboard build):

```bash
git add .
git commit -m "update dashboard — describe what changed"
git push
```

Railway auto-deploys on every push to `main`. Live within ~60 seconds.

---

## Project Structure
```
rekw-stocks/
├── public/
│   └── index.html      ← The dashboard (edit this to update the site)
├── server.js           ← Express static file server
├── package.json        ← Node dependencies
├── .gitignore
└── README.md
```

---

## Environment Variables (optional)
If you want to pre-bake the Finnhub API key server-side in future:
In Railway → **Variables** → add:
```
FINNHUB_KEY=your_key_here
```

---

## DNS Summary (for reference)
| Type | Host | Value |
|------|------|-------|
| CNAME | `stonks` | `xxxxxxxx.up.railway.app` |
| TXT | `_railway-verify.stonks` | `railway-verify=...` |
