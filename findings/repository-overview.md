# Repository Overview

## What It Does
This repository is a minimal Next.js starter for Contentstack. It fetches a `page` entry from Contentstack, renders it as a homepage, and supports Contentstack Live Preview / Visual Builder so editors can see content updates in real time.

## Structure
- `app/`: Next.js App Router entrypoints and global app shell.
- `components/`: UI rendering for page content and preview mode.
- `lib/`: Contentstack SDK setup, data-fetching helpers, and TypeScript content models.
- `.github/workflows/`: repository automation for policy, SCA, and Jira issue integration.
- Root config files: Next.js, ESLint, Tailwind/PostCSS, TypeScript, and environment examples.

## Key Modules
- `app/page.tsx`: main route. Chooses preview vs standard rendering, then loads the homepage content from Contentstack.
- `components/Preview.tsx`: client component that initializes Contentstack Live Preview and refetches content when entries change.
- `components/Page.tsx`: shared content renderer for the page title, description, image, rich text, and modular blocks.
- `lib/contentstack.ts`: core integration layer. Builds the Contentstack stack client, initializes live preview, and defines `getPage(url)`.
- `lib/types.ts`: TypeScript interfaces for the Contentstack content model, especially the `Page` entry and its block structure.
- `app/layout.tsx`: root layout and top-level page container.

## Where To Start
1. Read `README.md` for setup, required Contentstack credentials, and the intended starter workflow.
2. Open `lib/contentstack.ts` to understand environment variables, API configuration, preview mode, and how content is queried.
3. Follow the request path in `app/page.tsx` to see how the app switches between normal rendering and preview rendering.
4. Read `components/Page.tsx` to understand the actual homepage UI and the shape of content expected from Contentstack.
5. Use `lib/types.ts` as the source of truth for the data model while writing onboarding docs.

## Evidence
- Files reviewed: `README.md`, `package.json`, `app/page.tsx`, `app/layout.tsx`, `components/Page.tsx`, `components/Preview.tsx`, `lib/contentstack.ts`, `lib/types.ts`, `next.config.mjs`, `.env.example`
- Commands used: `rg --files app components lib .github`, `Get-Content <file>`
