# querying.ai plugins

Plugins that connect AI coding agents to [querying.ai](https://querying.ai): answers and cited sources from ChatGPT, Gemini, Perplexity, Google AI Overviews, Copilot and other AI engines, prompt research, and GEO monitors.

Every client talks to the remote MCP server `https://mcp.querying.ai/mcp`. The first time the agent uses it, your browser opens the querying.ai sign-in page; approve the connection and the agent is connected to your account. You can see and disconnect connected apps at https://querying.ai/dashboard/keys.

## Install

Claude Code:

```bash
claude plugin marketplace add OPACTOR-DEV/querying-plugins
claude plugin install querying@querying
```

Then run `/mcp` and choose Authenticate for `querying`.

Codex:

```bash
codex plugin marketplace add OPACTOR-DEV/querying-plugins
```

Then open the plugin directory in Codex and install `querying.ai`. If Codex does not open the sign-in page, run `codex mcp login querying`.

Cursor: add this repository as a plugin marketplace and install `querying`. Cursor shows a Connect button for the server.

Gemini CLI:

```bash
gemini extensions install https://github.com/OPACTOR-DEV/querying-plugins
```

Then run `/mcp auth querying`.

Any other MCP client: add a Streamable HTTP server at `https://mcp.querying.ai/mcp`. Clients that support MCP authorization sign in on their own. For a client without a browser, such as a CI job, send the header `Authorization: Bearer <key>` with an API key from https://querying.ai/dashboard/keys. Agents that read Agent Skills can use [skills/querying/SKILL.md](skills/querying/SKILL.md).

## Layout

- `plugins/querying/`: the plugin for Claude Code, Codex and Cursor (manifests, MCP config, skill, icons).
- `gemini-extension.json`, `GEMINI.md`: the Gemini CLI extension at the repository root.
- `skills/querying/`: the skill, copied into `plugins/querying/skills/` by `node scripts/sync-skill.mjs`.
- `server.json`: the MCP Registry entry.

Docs: https://docs.querying.ai. License: MIT.
