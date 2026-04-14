# kickstart-next Onboarding

## Overview
`kickstart-next` is a minimal Next.js starter for rendering a Contentstack `page` entry and supporting Contentstack Live Preview / Visual Builder workflows. The main developer workflow is: configure Contentstack credentials, run the app locally, and inspect how the homepage fetches a `page` entry and renders it in normal or preview mode.

## Quick Start
- Prerequisites: Node.js with `npm`, a Contentstack stack, delivery token, preview token, and the Contentstack CLI if you want to seed demo content.
- Install: `npm install`
- Run locally: `npm run dev`
- Build: `npm run build`
- Start production build: `npm run start`
- Lint: `npm run lint`
- Required environment variables: `NEXT_PUBLIC_CONTENTSTACK_API_KEY`, `NEXT_PUBLIC_CONTENTSTACK_DELIVERY_TOKEN`, `NEXT_PUBLIC_CONTENTSTACK_PREVIEW_TOKEN`, `NEXT_PUBLIC_CONTENTSTACK_ENVIRONMENT`, `NEXT_PUBLIC_CONTENTSTACK_REGION`, `NEXT_PUBLIC_CONTENTSTACK_PREVIEW`
- Optional environment variables used by the code: `NEXT_PUBLIC_CONTENTSTACK_CONTENT_DELIVERY`, `NEXT_PUBLIC_CONTENTSTACK_PREVIEW_HOST`, `NEXT_PUBLIC_CONTENTSTACK_CONTENT_APPLICATION`, `NEXT_PUBLIC_CONTENTSTACK_IMAGE_HOSTNAME`

## Structure
- `app/`: App Router entrypoints and root layout. The homepage is implemented in [app/page.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/app/page.tsx>) and the shell is in [app/layout.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/app/layout.tsx>).
- `components/`: Rendering components for normal and preview flows. The shared renderer is [components/Page.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/components/Page.tsx>), and preview-specific behavior lives in [components/Preview.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/components/Preview.tsx>).
- `lib/`: Contentstack integration and content model types. The fetch and preview logic is in [lib/contentstack.ts](</C:/Users/user/Documents/GitHub/kickstart-next/lib/contentstack.ts>) and the data model is in [lib/types.ts](</C:/Users/user/Documents/GitHub/kickstart-next/lib/types.ts>).
- Root config: [package.json](</C:/Users/user/Documents/GitHub/kickstart-next/package.json>) defines the run commands and dependencies; [next.config.mjs](</C:/Users/user/Documents/GitHub/kickstart-next/next.config.mjs>) configures remote image hosts; [.env.example](</C:/Users/user/Documents/GitHub/kickstart-next/.env.example>) shows the required Contentstack variables.

## Key Modules
- [app/page.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/app/page.tsx>): Best first file to read. It shows the top-level branch between preview mode and standard server-rendered mode.
- [lib/contentstack.ts](</C:/Users/user/Documents/GitHub/kickstart-next/lib/contentstack.ts>): Core integration layer. It builds the Contentstack SDK client, configures live preview, and defines `getPage("/")`.
- [components/Page.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/components/Page.tsx>): Shows the actual UI contract for a `Page` entry, including title, description, hero image, rich text sanitization, and block rendering.
- [components/Preview.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/components/Preview.tsx>): Explains how live preview works in the browser by initializing the preview SDK and refetching when entries change.
- [lib/types.ts](</C:/Users/user/Documents/GitHub/kickstart-next/lib/types.ts>): Source of truth for the expected Contentstack fields and block structure.

## Beginner Starting Point
Start with the homepage request flow from [app/page.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/app/page.tsx>). It is beginner-friendly because it is a short end-to-end path that touches routing, Contentstack data fetching, preview mode, and UI rendering without requiring knowledge of additional routes or backend services.

## Example Explanation
1. The app starts at [app/page.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/app/page.tsx>), which is the home route for the App Router.
2. That file checks `isPreview`, exported from [lib/contentstack.ts](</C:/Users/user/Documents/GitHub/kickstart-next/lib/contentstack.ts>). `isPreview` comes from `NEXT_PUBLIC_CONTENTSTACK_PREVIEW`.
3. If preview mode is off, `Home()` calls `getPage("/")` in [lib/contentstack.ts](</C:/Users/user/Documents/GitHub/kickstart-next/lib/contentstack.ts>).
4. `getPage("/")` uses the Contentstack delivery SDK to query the `page` content type, filter by `url`, and return the first matching entry typed as `Page`.
5. The returned entry is passed into [components/Page.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/components/Page.tsx>), which renders the title, description, image, rich text, and modular blocks.
6. `components/Page.tsx` sanitizes rich text with `isomorphic-dompurify` before using `dangerouslySetInnerHTML`, which is an important safety detail for onboarding.
7. If preview mode is on, [app/page.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/app/page.tsx>) renders [components/Preview.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/components/Preview.tsx>) instead of fetching once on the server.
8. [components/Preview.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/components/Preview.tsx>) initializes Contentstack Live Preview via `initLivePreview()`, then subscribes to `onEntryChange` so the page refetches when an editor changes content in Contentstack.
9. In both modes, the same page data shape is defined by [lib/types.ts](</C:/Users/user/Documents/GitHub/kickstart-next/lib/types.ts>), so that file is the next best reference when you want to understand what Contentstack fields the renderer expects.

## Learning Path
1. Read [README.md](</C:/Users/user/Documents/GitHub/kickstart-next/README.md>) to set up a Contentstack stack and tokens.
2. Trace the normal flow in [app/page.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/app/page.tsx>) and [lib/contentstack.ts](</C:/Users/user/Documents/GitHub/kickstart-next/lib/contentstack.ts>).
3. Read [components/Page.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/components/Page.tsx>) with [lib/types.ts](</C:/Users/user/Documents/GitHub/kickstart-next/lib/types.ts>) open beside it so the content model and renderer stay aligned.
4. Turn preview mode on with `.env` values from [.env.example](</C:/Users/user/Documents/GitHub/kickstart-next/.env.example>) and inspect [components/Preview.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/components/Preview.tsx>).
5. Review [next.config.mjs](</C:/Users/user/Documents/GitHub/kickstart-next/next.config.mjs>) and image-related env vars before changing Contentstack asset hosts.

## Mermaid Diagram
```mermaid
flowchart TD
  A[app/page.tsx Home route] --> B{isPreview?}
  B -- No --> C[lib/contentstack.ts getPage('/')]
  C --> D[Contentstack delivery SDK query]
  D --> E[components/Page.tsx]
  B -- Yes --> F[components/Preview.tsx]
  F --> G[initLivePreview + onEntryChange]
  G --> C
```

## Gotchas
- The metadata in [app/layout.tsx](</C:/Users/user/Documents/GitHub/kickstart-next/app/layout.tsx>) still uses the default `create next app` title and description, so it does not reflect the actual starter.
- Preview behavior depends on `NEXT_PUBLIC_CONTENTSTACK_PREVIEW=true`; without it, the app uses the one-time server fetch path.
- The README documents the primary env vars, but some optional host overrides are only discoverable in [lib/contentstack.ts](</C:/Users/user/Documents/GitHub/kickstart-next/lib/contentstack.ts>) and [next.config.mjs](</C:/Users/user/Documents/GitHub/kickstart-next/next.config.mjs>).
- There is no test suite or `npm test` script in [package.json](</C:/Users/user/Documents/GitHub/kickstart-next/package.json>), so onboarding relies on local running, linting, and code inspection.

## Evidence
- Files reviewed: `AGENTS.md`, `README.md`, `package.json`, `.env.example`, `app/page.tsx`, `app/layout.tsx`, `components/Page.tsx`, `components/Preview.tsx`, `lib/contentstack.ts`, `lib/types.ts`, `next.config.mjs`, `findings/repository-overview.md`
- Commands used: `Get-ChildItem -Force`, `rg --files`, `Get-Content <file>`
- Inferences: The recommended beginner path is an inference based on the shortest visible end-to-end flow in the codebase.
