# Where To Start

## Best Starting Path For A Beginner
Start in this order:

1. `README.md`
Read this first to understand what the repository is for, which external service it depends on, and which environment variables are required.

2. `lib/contentstack.ts`
This is the most important code file for understanding the app. It shows how the Contentstack client is configured, how preview mode is enabled, and how page content is fetched.

3. `app/page.tsx`
This is the main route entrypoint. It shows the top-level application flow: decide whether preview mode is active, then render either the live preview component or the normal page component.

4. `components/Page.tsx`
Read this to understand what content the app expects and how it is displayed. This file makes the data model concrete because it renders the page title, description, image, rich text, and modular blocks.

5. `lib/types.ts`
Use this as the reference for the Contentstack schema represented in code. It defines the `Page` shape and the nested block structure used by the renderer.

6. `components/Preview.tsx`
Read this after the basics make sense. It explains how live preview works on the client side and how the app refreshes content when entries change.

## Why This Order Helps
This sequence moves from broad context to concrete implementation:
- `README.md` explains the setup and purpose
- `lib/contentstack.ts` explains data access
- `app/page.tsx` explains runtime flow
- `components/Page.tsx` explains UI output
- `lib/types.ts` explains content structure
- `components/Preview.tsx` explains the preview-specific behavior

## Evidence
- Based on review of: `README.md`, `app/page.tsx`, `components/Page.tsx`, `components/Preview.tsx`, `lib/contentstack.ts`, `lib/types.ts`
