# Obsidian Publishing

## Required Behavior

Publish the final onboarding document to Obsidian after writing the local Markdown file. Treat Obsidian publication as required unless MCP tooling is unavailable or fails.

Use this order:
1. Decide the note path. Default to `Onboarding/<repo-name>.md` if the user did not specify one.
2. Check whether the note already exists when the available MCP tools make that practical.
3. Create the note with `obsidian_append_content` when it does not exist.
4. Use `obsidian_patch_content` or append to the existing note when refining an earlier onboarding note.
5. Tell the user which Obsidian note was written and whether it was created or updated.

## Content Rules

- Keep the title at the top of the note.
- Ensure the published content is the same Markdown onboarding document produced on disk.
- Preserve fenced code blocks, especially `mermaid` blocks.
- Include the local file path or project-relative output path near the end of the note when useful.
- If the repository has mandatory output rules, satisfy them before publishing.

## Failure Handling

If Obsidian tools are unavailable or publishing fails:
- keep the generated Markdown on disk
- report the exact MCP limitation or error
- do not discard the onboarding document
