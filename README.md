# nutrition-pal

Personal nutrition tracker. Single-user, Android-only (Pixel 9 Pro XL). Uses Claude to parse food entries — text now, photos and barcodes later. Built as a PWA so it installs to the home screen like a native app without any Play Store overhead.

## Stack

- **Next.js + TypeScript + Tailwind** — App Router, server-side API routes hide the LLM key.
- **Anthropic Claude** — `claude-sonnet-4-6` for vision, `claude-haiku-4-5` for cheap text parsing.
- **Vercel** — hosting, auto-deploy on `git push`.
- **PWA** — manifest + service worker; install via Chrome on the Pixel.

## Local dev

```bash
cp .env.example .env.local
# fill in ANTHROPIC_API_KEY
npm install
npm run dev
```

To open the dev server on the Pixel: find your machine's LAN IP (`ipconfig getifaddr en0`) and browse to `http://<ip>:3000` in Chrome on the phone. Same Wi-Fi required.

## Deploy

1. Push to GitHub.
2. Import the repo into Vercel.
3. Set `ANTHROPIC_API_KEY` in Vercel → Project → Settings → Environment Variables.
4. Every `git push` to `main` auto-deploys.

## Install on phone

Open the Vercel URL in Chrome on the Pixel → ⋮ menu → **Add to Home Screen** (or **Install app**). It now launches fullscreen with its own icon.
