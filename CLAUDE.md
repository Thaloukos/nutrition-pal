# CLAUDE.md

Context for Claude Code sessions in this repo.

## What this is

Personal nutrition tracker for a single user (Thalis). Runs only on a Pixel 9 Pro XL as a PWA. Uses Claude to parse food entries into calories + nutrients. Inputs: text first; photos, barcodes, voice later.

## Stack decisions (locked, do not relitigate)

- **PWA, not Expo/React Native.** No app store, no signing, no APK distribution. Pixel + Chrome is a first-class PWA host.
- **Next.js, not Vite.** Server-side API routes are required to keep the LLM key off the client.
- **Claude (Anthropic), not OpenAI.** Vision quality for food photos + prompt caching benefits. Models: `claude-sonnet-4-6` for vision, `claude-haiku-4-5` for cheap text parsing.
- **Vercel hosting.** Free tier, zero-config Next.js deploys.

## Critical rules

- **LLM API key is server-side only.** Lives in `.env.local` locally and Vercel env vars in production. Never import `process.env.ANTHROPIC_API_KEY` from a client component or expose it in `NEXT_PUBLIC_*`.
- **Do not use Wonderful corp keys.** `~/wonderful/env_files/` contains Anthropic, OpenAI, Gemini, and Azure keys, but they are org-owned (`sk-svcacct-...`, `sk-proj-...`, Wonderful workspace). Off-limits for this personal project. Always assume a personal Anthropic key in `ANTHROPIC_API_KEY`.
- **Single-user assumption.** No auth, no multi-tenancy, no role system, no rate limiting beyond Vercel defaults. Do not add abstractions for hypothetical other users.

## Deployment / testing

- **Deploy:** `git push` → Vercel auto-deploys `main`.
- **Phone testing:** Open Vercel URL in Chrome on the Pixel 9 Pro XL.
- **Local phone testing:** `npm run dev` on the dev machine, then browse to `http://<lan-ip>:3000` from the Pixel on the same Wi-Fi.

## User context

Thalis is a generalist software engineer with no specific mobile/PWA background. Prefers the easiest, cleanest path; favor boring, well-trodden choices over novel ones.
