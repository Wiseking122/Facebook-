# 🦉 WiseEarn Mini App — Setup Guide

## Files
- `index.html` → The Telegram Mini App frontend (host this)
- `app.py`      → Updated Flask backend

---

## Step 1: Host the Mini App (index.html)

Choose any free static host:

**Vercel (recommended):**
```bash
npm i -g vercel
vercel --name wiseearn-app
# Copy the URL it gives you, e.g. https://wiseearn-app.vercel.app
```

**Netlify:** Drag & drop `index.html` at netlify.com → get a URL.

**GitHub Pages:** Push to a repo → Settings → Pages → enable.

> ⚠️ Must be HTTPS — Telegram requires it.

---

## Step 2: Update index.html

In `index.html`, replace:
```js
const BACKEND = "https://YOUR_BACKEND_URL";
```
with your Flask server URL (e.g. from Railway, Render, or your own VPS).

---

## Step 3: Host the Flask backend (app.py)

**Railway (free tier):**
1. Push to GitHub
2. New project → Deploy from GitHub
3. Set env var: `BOT_TOKEN=your_token`
4. Copy the generated URL

**Install dependencies:**
```bash
pip install flask flask-cors requests
```

---

## Step 4: Configure BotFather

1. Open @BotFather in Telegram
2. `/mybots` → Select your bot
3. **Bot Settings → Menu Button → Configure menu button**
4. Set URL = your hosted `index.html` URL
5. Set button text = `Open WiseEarn`

Also run:
```
/setmenubutton
```

---

## Step 5: Set your Webhook

```bash
curl https://api.telegram.org/botYOUR_TOKEN/setWebhook \
  -d "url=https://YOUR_BACKEND_URL/webhook"
```

---

## Step 6: Test

1. Open your bot in Telegram
2. The menu button should launch the Mini App
3. Test /start, /balance, /bonus commands

---

## What's connected

| Mini App Action | Backend Endpoint |
|---|---|
| Load balance | GET `/balance?user_id=X` |
| Claim bonus  | POST `/bonus` |
| Withdraw     | POST `/withdraw` |
| Survey postback | GET `/postback` |
| Bot commands | POST `/webhook` |
