# Day MCP setup

Goal
- Let Kero answer day planning questions by querying Asana, Notion, and Google Calendar.
- Save a daily summary file in this folder and respond in chat at the same time.
 - Accept Japanese questions and respond in Japanese.

What you get in this folder
- `day/mcp-config.template.json`: MCP server config template you will adapt to your MCP client.
- `day/kerro-system.md`: System instructions for Kero on how to route requests.
- `day/daily-template.md`: A daily report template.
- `day/prompts.md`: Example prompts and expected outputs.

Step 1) Pick MCP servers
You need one MCP server per service (Asana, Notion, Google Calendar). Each server comes with a command and required env vars.
Because server names and packages differ, you must choose the servers you trust and then fill in the template.

Safety-first selection guidelines (recommended)
- Prefer servers that are actively maintained, have clear documentation, and do not require any cloud relay.
- Run servers locally only; avoid any servers that ask you to upload tokens to a third party.
- Use least-privilege scopes for each service (only read/write what you need).
- Keep tokens in a local env file and never commit them to git.

Example of what “least-privilege” means
- Google Calendar: read/write events only, not full account access.
- Notion: only the specific databases you share with the integration.
- Asana: only the workspace/projects you need.

Example (placeholder only, NOT real package names)
- Asana server command: `node /path/to/asana-mcp-server/index.js`
- Notion server command: `node /path/to/notion-mcp-server/index.js`
- Google Calendar server command: `node /path/to/gcal-mcp-server/index.js`

Step 2) Create API credentials
Asana (Personal Access Token)
- Create a PAT in Asana developer settings.
- Save it as `ASANA_TOKEN`.

Notion (Internal integration)
- Create an internal integration and copy the token.
- Share the target pages/databases with the integration.
- Save it as `NOTION_TOKEN`.

Google Calendar (OAuth)
- Create a Google Cloud project and enable Google Calendar API.
- Create OAuth client credentials.
- Obtain a refresh token for your account.
- Save the client id, client secret, and refresh token in env vars.

Note: OAuth flows vary by tool. Use the MCP server docs for the exact process. If a server supports a service account, that is another option.

Step 3) Fill MCP config
- Copy `day/mcp-config.template.json` to wherever your VSCode Codex MCP client expects it.
- Replace the placeholders with the actual command, args, and env vars.

Example
- `ASANA_TOKEN` and `NOTION_TOKEN` values go into the `env` fields for their servers.
- `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, `GOOGLE_REFRESH_TOKEN` go into the Google Calendar server env.

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
1) Decide servers for Asana/Notion/Google Calendar.
2) Create tokens and save them in a local env file.
3) Fill `day/mcp-config.template.json` with the server commands and env vars.
4) Add `day/kerro-system.md` to your Codex system prompt.
5) Ask: 「今日の予定は？」 → Calendar is queried → response + daily file update.
