# Ductline Briefing

CEO morning dashboard — Gmail-driven view of pending actions, client follow-ups, weekly commitments, and 30-day client roster.

> **Internal use only.** Contains real client and financial data.

## Quick Start

```bash
npm install
npm run dev
```

Open the localhost URL it shows. Sign in:

- **Username:** `Ductline`
- **Password:** `Ductline1$`

## Deployment

### Recommended: Vercel (free, automatic)

1. Push this repo to GitHub (keep it **Private**).
2. Go to [vercel.com](https://vercel.com), sign in with GitHub.
3. Click **Add New → Project** → import this repo.
4. Leave defaults, click **Deploy**.
5. You'll get a URL like `ductline-dashboard.vercel.app`.

Every `git push` to `main` redeploys automatically.

### Alternative: GitHub Pages

```bash
npm install -D gh-pages
```

Add to `package.json`:

```json
"homepage": "https://YOUR-USERNAME.github.io/ductline-dashboard",
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d dist"
}
```

Run `npm run deploy`.

## Refreshing the Data

The dashboard data lives in `src/App.jsx` near the top — `THREADS`, `COMMITMENTS`, `ALL_CLIENTS`, `LAST_REFRESHED`, and `TODAY` constants.

**To refresh:**

1. Tap the refresh icon (🔄) in the dashboard header.
2. It opens Claude in a new tab with a prefilled message.
3. Send the message — Claude pulls your Gmail, classifies threads, and gives you fresh constants.
4. Replace the constants in `src/App.jsx`, also update `LAST_REFRESHED` and `TODAY`.
5. `git add . && git commit -m "Refresh data" && git push`
6. Vercel redeploys in ~30 seconds.

## Security Notes

The login credentials are hardcoded in `src/App.jsx`. Anyone with browser DevTools access can read them. This is a **casual gate**, not real authentication.

**Mitigations:**

- Keep the GitHub repo **Private**.
- Don't share the deployment URL publicly.
- The `<meta name="robots" content="noindex, nofollow">` tag prevents search engines from indexing the page.
- For real auth later, swap in [Clerk](https://clerk.com), [Supabase Auth](https://supabase.com/auth), or [Auth0](https://auth0.com).

## Stack

- React 18 + Vite
- Tailwind CSS 3
- Lucide icons
- Fraunces (display) + Inter (body) via Google Fonts
- No backend — data is static, refreshed manually via Claude

## File Map

```
.
├── index.html               # HTML entry point
├── package.json             # Dependencies and scripts
├── vite.config.js           # Vite build config
├── tailwind.config.js       # Tailwind setup
├── postcss.config.js        # PostCSS for Tailwind
├── vercel.json              # SPA routing on Vercel
├── public/
│   └── favicon.svg          # D mark favicon
└── src/
    ├── main.jsx             # React entry
    ├── index.css            # Tailwind directives
    └── App.jsx              # The entire dashboard (data + UI + auth)
```

## License

Proprietary — Ductline Manufacturing.
