# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

@AGENTS.md

## Project status

LinkBase is at the `create-next-app` starter stage: `app/page.tsx` and `app/layout.tsx` still hold the template content and metadata. The product designs (Welcome, Landing, Dashboard, Public Profile pages) are in `../Linkbase+Claude+Designs.zip` (nested zips, one per page). The build prompts are in `../Project+1+Prompts.docx`. Both are in the parent folder, outside this git repo.

## Commands

Run from this directory (`linkbase/`):

- `npm run dev`: dev server at http://localhost:3000 (Turbopack)
- `npm run build` / `npm run start`: production build and serve
- `npm run lint`: ESLint 9 flat config (`eslint.config.mjs`, Next core-web-vitals + TypeScript presets)
- Type-check: `npx tsc --noEmit`

No test framework is set up yet.

## Stack and non-obvious configuration

- **Next.js 16.4 (App Router) + React 19.3 + TypeScript (strict).** As AGENTS.md warns, APIs differ from older Next.js versions. Check `node_modules/next/dist/docs/` before using framework APIs.
- **`next.config.ts` turns on `cacheComponents` and `partialPrefetching`.** Caching and dynamic rendering follow the Cache Components model (`"use cache"`, Suspense boundaries around dynamic data), not the older `fetch`-cache and route-segment-config conventions.
- **Tailwind CSS v4 is loaded through the `@tailwindcss/turbopack` loader**, set in `next.config.ts` under `turbopack.rules`. There is no PostCSS config and no `tailwind.config.*`. Theme tokens live in `app/globals.css` under `@theme inline`; light/dark colors are CSS variables (`--background`, `--foreground`) that switch on `prefers-color-scheme`.
- **Route props use the global generated types**, for example `LayoutProps<"/">` in `app/layout.tsx`. These come from `.next/types` / `.next/dev/types` after `dev` or `build` runs.
- **Path alias:** `@/*` resolves to the project root (for example `@/app/...`).
- **Fonts:** Geist and Geist Mono come from `next/font/google` and are exposed as `--font-geist-sans` / `--font-geist-mono`.
