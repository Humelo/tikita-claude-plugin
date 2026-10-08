# Tikita for Claude

![Tikita icon](.claude-plugin/icon.png)

Tikita helps creators build interactive story drafts. Connect your Tikita account to inspect stories you own, create private drafts, and refine characters, episodes, variables, example dialogue, lorebook entries, and image links. Draft edits stay in the creator workspace until you review and save them in Tikita Studio. Publishing a story is a separate action in Studio.

## Connect

Install this plugin in Claude, open its **Connectors** tab, and connect Tikita. Sign in on Tikita's OAuth page and approve the connection. Claude Code can also load the included remote MCP server from `.mcp.json`. The server URL is `https://mcp.tikita.ai/mcp`; no API key is bundled or required.

Try: “Show my Tikita drafts and help me choose one to edit.” For an existing draft, provide its `https://tikita.ai/create/<short_id>` URL. The included skill reads the selected workspace before changes and checks the result afterward.

## Data and actions

When you use a Tikita tool, Claude sends the tool request to Tikita's authenticated MCP server and receives the account data needed for that request. The server enforces the signed-in user's permissions. Some tools can change private drafts or reusable lorebook entries, create a public comment when explicitly requested, or import an image from a user-supplied URL. Image uploads use Tikita's moderation pipeline. This plugin does not run local code or send data to an undeclared service.

Read the [creator guide](https://mcp.tikita.ai/guides/story-creation.md), [privacy policy](https://tikita.ai/ko/privacy), and [terms](https://tikita.ai/ko/terms). For help, use [Tikita support](https://tikita.ai/ko/support).
