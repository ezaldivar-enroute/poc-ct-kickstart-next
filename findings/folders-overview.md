# Main Folders

## Overview
This repository is intentionally small. Most of the app lives in three source folders: `app`, `components`, and `lib`.

## Folder Map
- `app/`: Next.js App Router files. Contains the root layout (`layout.tsx`), homepage route (`page.tsx`), global styles (`globals.css`), and favicon.
- `components/`: React UI components. Contains the shared page renderer (`Page.tsx`) and the live-preview client component (`Preview.tsx`).
- `lib/`: Shared logic and data definitions. Contains the Contentstack setup and fetching code (`contentstack.ts`) plus TypeScript interfaces for content types (`types.ts`).
- `.github/`: Repository automation and ownership metadata. Contains `CODEOWNERS` and workflow files for policy scanning, dependency scanning, and Jira issue integration.
- `findings/`: Markdown findings produced for onboarding and repository analysis.
- `logs/`: Local log output directory.
- `.next/`: Next.js build output generated locally.
- `node_modules/`: Installed npm dependencies.

## Which Folders Matter Most
For understanding the app itself, start with:
1. `lib/` for configuration and data fetching
2. `app/` for routing and entrypoints
3. `components/` for how content is rendered

## Evidence
- Commands used: `Get-ChildItem app -Recurse`, `Get-ChildItem components -Recurse`, `Get-ChildItem lib -Recurse`, `Get-ChildItem .github -Recurse`
