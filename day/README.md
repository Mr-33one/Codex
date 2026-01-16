# Day MCP setup

Goal
- Let Kero answer day planning questions by querying Google Calendar and Google Tasks via a Google Workspace MCP server.
- Save a daily journal file in this folder and respond in chat at the same time.
 - Accept Japanese questions and respond in Japanese.

What you get in this folder
- `day/mcp-config.template.json`: MCP server config template you will adapt to your MCP client.
- `day/kerro-system.md`: System instructions for Kero on how to route requests.
- `day/daily-template.md`: A daily journal template.
- `day/prompts.md`: Example prompts and expected outputs.

Step 1) Pick MCP server
You need one MCP server that supports both Google Calendar and Google Tasks. The server comes with a command and required env vars.
Because server names and packages differ, you must choose the server you trust and then fill in the template.

Safety-first selection guidelines (recommended)
- Prefer servers that are actively maintained, have clear documentation, and do not require any cloud relay.
- Run servers locally only; avoid any servers that ask you to upload tokens to a third party.
- Use least-privilege scopes for each service (only read/write what you need).
- Keep tokens in a local env file and never commit them to git.

Example of what “least-privilege” means
- Google Calendar: read/write events only, not full account access.
- Google Tasks: read/write tasks only.

Example (placeholder only, NOT real package names)
- Google Workspace MCP server command: `uvx workspace-mcp --tools calendar tasks`

Step 2) Create API credentials
Google OAuth (Calendar + Tasks)
- Create a Google Cloud project and enable Google Calendar API.
- Create OAuth client credentials.
- Obtain a refresh token for your account.
- Save the client id, client secret, and refresh token in env vars.
 - Enable Google Tasks API in the same project.

Note: OAuth flows vary by tool. Use the MCP server docs for the exact process.

Step 3) Fill MCP config
- Copy `day/mcp-config.template.json` to wherever your VSCode Codex MCP client expects it.
- Replace the placeholders with the actual command, args, and env vars.

Example
- `GOOGLE_OAUTH_CLIENT_ID`, `GOOGLE_OAUTH_CLIENT_SECRET` go into the Google Workspace server env.

Step 4) Use Kero in VSCode Codex
- Paste `day/kerro-system.md` into your Codex system prompt or profile instructions.
- Ask questions like in `day/prompts.md`.
- Kero should both answer and update the daily file.

Step 5) Daily output
- Copy `day/daily-template.md` to `day/daily-YYYY-MM-DD.md` each day.
- Kero should append new results to the current day file.

Example daily file name
- `day/daily-2025-01-13.md`

If anything is unclear, we can pick the exact MCP servers together and fill the config.

Beginner-friendly quick flow (example)
1) Decide a Google Workspace MCP server.
2) Create OAuth credentials and save them in a local env file.
3) Fill `day/mcp-config.template.json` with the server command and env vars.
4) Add `day/kerro-system.md` to your Codex system prompt.
5) Ask: 「今日の予定は？」 → Calendar/Tasks are queried → response + daily file update.
