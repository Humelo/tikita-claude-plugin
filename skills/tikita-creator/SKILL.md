---
name: tikita-creator
description: Create, inspect, and edit the user's Tikita interactive story drafts, characters, episodes, dialogue, variables, lorebook, and image links through Tikita Creator MCP. Use when the user mentions Tikita or provides a tikita.ai/create URL.
---

# Tikita Creator

Use the connected Tikita MCP tools. The production endpoint is `https://mcp.tikita.ai/mcp`. Preserve an explicitly requested environment and account. A supplied Studio URL `/create/<short_id>` identifies an existing story; extract the short ID and inspect that workspace instead of creating another story.

## Connect

In Claude chat or Cowork, use the plugin's **Connectors** tab to connect Tikita. Claude handles OAuth; the user signs in to Tikita and grants consent. In Claude Code, use the Tikita server loaded from this plugin's `.mcp.json` and complete its OAuth login. Never ask the user to reveal credentials, tokens, or callback codes. If the connection is unavailable, report that state rather than claiming success.

Call `get_capabilities` to verify the authenticated connection. A health response, consent page, or tool transport completion with `ok: false` does not establish success. If OAuth fails, report the observed error and do not repeat authorization blindly.

## Work on a draft

1. Read the Story Creator Guide resource, or the bundled [creator guide](references/creator-guide.md), and inspect the actual available tool schemas. Use the category reference for exact category labels.
2. Use `story_get_creation_context` and `workspace_get_draft` for an existing story. Keep the user's target, premise, tone, language, and requested changes. Ask for missing creative direction only when it prevents the requested task; an explicit request to invent a test draft is sufficient authority to do so.
3. Edit only the named story. Use camelCase story metadata fields and the child field names shown in the schemas. Workspace patches shallow-merge objects and replace arrays; retain existing IDs, unrelated fields, and array items when editing part of a draft. Read immediately before writes and avoid simultaneous Studio edits.
4. Use the dedicated lorebook library and attach tools. Library edits affect reusable account entries, so do not replace or delete a shared entry merely to change one story. Workspace lorebook copies reach conversations only after the creator saves in Studio.
5. Use only owned, completed image assets with terminal moderation. An image attachment, image-group assignment, cover, character avatar, and cinema sprite are separate references. Read back each reference that changed. If only an image URL is available and no library-list tool exists, explain the missing ID; do not invent an ID, scrape private storage, or silently import another copy.
6. Check tool results for `ok: false`, errors, limits, and missing resources. After a timeout or ambiguous write, read the target before deciding whether another write is necessary. Do not blindly repeat creates.
7. Verify changes with `workspace_get_draft`. Summarize the changed fields, counts, and remaining work, and link back to Studio. A workspace update changes a draft; applying it to the story and publishing require the creator's Studio save/publish flow. Do not claim that a live story or conversation was updated by a draft write.

## Scope and data handling

Never print passwords, access/refresh tokens, authorization codes, signed upload URLs, or raw authentication material. Creator-only story fields may be read and edited for their owner when the request requires it; keep them out of public descriptions and comments.

Public comment creation is a separate action and requires an explicit user request. Do not send comments as a connectivity test. Lorebook deletion removes library data and links across stories; explain its scope before executing an explicit deletion request. Ordinary authorized draft edits can proceed without repeated approval requests.

This plugin does not sell subscriptions, credits, digital goods, or paid image generation. Do not introduce purchase links or claim a paid generator exists. Use only the capabilities actually returned by the MCP server.
