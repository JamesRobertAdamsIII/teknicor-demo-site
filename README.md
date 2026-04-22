# Teknicor Copilot Lite

Dark-theme presales demo tool built with Next.js, TypeScript, and Tailwind CSS.

## What is included

This project now ships with two answer modes:

- **Demo Mode (works immediately):**
  - No backend dependency
  - Local note retrieval only
  - Great for Webex demos and lightweight static hosting
- **Live Mode (secure backend):**
  - Uses server route at `/api/ask`
  - Searches local notes, then calls OpenAI Responses API
  - Optional tool-based web search (`web_search_preview`)
  - API keys remain server-side only

## Files used

- `app/page.tsx` - Main "Ask Teknicor AI" interface, mode toggle, ask form, answer + sources UI
- `src/data/notes.ts` - Seeded Teknicor consulting notes dataset
- `src/lib/retrieval.ts` - Lightweight keyword/semantic-style retrieval and demo answer builder
- `app/api/ask/route.ts` - Live-mode backend route (notes retrieval + OpenAI call + optional web search)
- `app/api/generate/route.ts` - Original content-generation route (kept for compatibility)
- `.env.example` - Environment variable template

## Local run

1. Install Node.js 18+.
2. Install dependencies:
   ```bash
   npm install
   ```
3. Create an env file:
   ```bash
   copy .env.example .env.local
   ```
4. Optional for Live Mode: set your key in `.env.local`:
   ```env
   OPENAI_API_KEY=your_key_here
   ```
5. Start local dev:
   ```bash
   npm run dev
   ```
6. Open [http://localhost:3000](http://localhost:3000).

## Deployment guidance

### A) Demo version (GitHub Pages friendly)

GitHub Pages is fine for Demo Mode because:
- the app can run from local-note logic without calling private APIs
- no API keys are needed in the browser
- it is cost-effective and fast for internal showcase pages

Deploy pattern:
- Export static assets from a static-only variant of the UI, or host the UI code in a static framework equivalent.
- Keep it in **Demo Mode only**.

### B) Live version (Cloudflare Pages recommended)

GitHub Pages alone is not ideal for private live AI calls because:
- it has no secure serverless runtime for protected API keys
- any key placed in frontend code would be exposed

Cloudflare Pages is better for Live Mode because:
- you can run serverless functions for `/api/ask`
- secrets are stored in Cloudflare environment variables
- you can keep notes retrieval + AI calls fully server-side

Deploy pattern:
1. Push this Next.js project to Git.
2. Create a Cloudflare Pages project from the repo.
3. Configure build command: `npm run build`.
4. Configure output for Next.js via Cloudflare adapter/workers setup (or deploy with a Next.js-compatible Cloudflare flow).
5. Add environment secret `OPENAI_API_KEY` in Cloudflare project settings.
6. Deploy.

## OpenAI Responses API usage

Live route uses `client.responses.create(...)` and supports:
- local context grounding from note retrieval
- optional tool-based web search (`web_search_preview`)
- structured answer + sources response back to frontend
