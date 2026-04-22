# Teknicor Copilot Lite

Simple internal tool built with Next.js, TypeScript, and Tailwind CSS.

## Features

- One-page UI with:
  - Large textarea for customer notes
  - Output type dropdown
  - Submit button
  - Formatted result panel
- Server-side API route at `/api/generate`
- OpenAI API key read from environment variables on the server

## Setup

1. Install Node.js 18+.
2. Install dependencies:
   ```bash
   npm install
   ```
3. Create env file:
   ```bash
   copy .env.example .env.local
   ```
4. Add your OpenAI key to `.env.local`:
   ```env
   OPENAI_API_KEY=...
   ```
5. Start dev server:
   ```bash
   npm run dev
   ```

Open [http://localhost:3000](http://localhost:3000).
