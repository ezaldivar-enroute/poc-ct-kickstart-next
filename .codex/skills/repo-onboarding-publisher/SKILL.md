---
name: repo-onboarding-publisher
description: Analyze software repositories and produce a Markdown onboarding document that includes an overview, structure summary, key modules, a beginner starting point, a step-by-step example explanation, a learning path, and a Mermaid diagram, then publish the final document to Obsidian through MCP. Use when a user asks for repo onboarding docs, newcomer guides, architecture walkthroughs for an existing codebase, or wants repository analysis exported to Obsidian.
---

# Repo Onboarding Publisher

## Overview

Analyze the repository before writing. Build the onboarding guide from repository evidence, not guesses.

Always produce a Markdown onboarding document. Treat the document as the primary deliverable, not an optional artifact.

The onboarding document must include these sections:
- Overview
- Structure
- Key Modules
- Beginner Starting Point
- Example Explanation
- Learning Path
- Mermaid Diagram

Keep the document practical and evidence-based. Add supporting sections such as setup, gotchas, or evidence when they help a newcomer get productive faster.

Read [references/onboarding-template.md](references/onboarding-template.md) before drafting the final document. Read [references/obsidian-publishing.md](references/obsidian-publishing.md) before publishing.

## Workflow

1. Read repository instructions first.
   - Open `AGENTS.md`, `README*`, `CONTRIBUTING*`, and package/build manifests when present.
   - Follow any repo-specific output rules exactly. If the repository requires findings in a folder such as `./findings`, save the generated Markdown there before publishing.
2. Build a minimal codebase map.
   - Prefer `rg --files` and focused file reads.
   - Identify the app entrypoints, core libraries, config files, tests, and environment files.
   - Record the concrete files and commands you used so the final document includes evidence.
3. Extract the onboarding essentials.
   - Summarize project purpose and the primary user or developer workflow for the `Overview` section.
   - Summarize the top-level structure for the `Structure` section.
   - Identify the few modules a newcomer should read first for the `Key Modules` section.
   - List setup prerequisites, environment variables, and run/build/lint/test commands when they are relevant to understanding or running the project.
   - Call out third-party services, APIs, and important risks or documentation gaps.
4. Choose one beginner-friendly example.
   - Prefer the shortest end-to-end path that shows how the app works.
   - Favor a single route, command, or data flow with limited branching.
   - Avoid examples that require broad domain knowledge or many hidden prerequisites.
   - Use this example to anchor both the `Beginner Starting Point` and `Example Explanation` sections.
   - State why the example is beginner-friendly in one sentence.
5. Explain the example step by step.
   - Walk through the exact request path or execution flow using file references.
   - Explain what each module contributes and how data moves through the example.
   - Keep the explanation sequential and newcomer-readable.
   - End with a short `Learning Path` section that tells the newcomer what to read or try next after the example.
6. Generate one Mermaid diagram.
   - Use a simple flowchart or sequence diagram.
   - Keep labels aligned to real code concepts and file names.
   - Focus the diagram on the beginner-friendly example, not the entire repository.
   - Place it under a `Mermaid Diagram` section in the Markdown document.
7. Write the onboarding document in Markdown.
   - Use the template in `references/onboarding-template.md`.
   - Keep it concise, factual, and evidence-based.
   - Always include the required sections: `Overview`, `Structure`, `Key Modules`, `Beginner Starting Point`, `Example Explanation`, `Learning Path`, and `Mermaid Diagram`.
   - Include clickable file references when the environment supports them.
8. Publish to Obsidian through MCP.
   - Publish the final Markdown document to Obsidian as a required final step.
   - Default note path: `Onboarding/<repo-name>.md` unless the user gives another location.
   - Create a new note with `obsidian_append_content` when no note exists.
   - Update an existing note with append or patch operations when refining prior output.
   - Preserve Mermaid code fences so the diagram renders in Obsidian.
9. Close the task clearly.
   - Tell the user where the Markdown was saved locally.
   - Tell the user which Obsidian note was created or updated.
   - Mention any gaps you could not verify.
   - If Obsidian publication fails, report that failure explicitly instead of implying completion.

## Evidence Rules

Include an `Evidence` section in the onboarding document.

List:
- Files reviewed
- Commands used
- Any assumptions that were necessary because evidence was missing

Prefer direct repository evidence over inferred behavior. If you infer something, label it as an inference.

## Quality Bar

Ensure the onboarding document:
- helps a newcomer run or inspect the project quickly
- is written in Markdown every time
- includes `Overview`, `Structure`, `Key Modules`, `Beginner Starting Point`, `Example Explanation`, `Learning Path`, and `Mermaid Diagram`
- names the first files to read
- explains one real code path end to end
- includes one Mermaid diagram that matches the example
- avoids large changelog-style inventories
- avoids unsupported claims

## Output Handling

Save the generated Markdown to disk before publishing when the repository instructions require local output. If there is no repo-specific rule, still save a local Markdown copy in a sensible project folder such as `findings/` or another user-requested location.

If Obsidian publishing fails, still leave the Markdown on disk and report the failure with the exact missing prerequisite or tool issue.
