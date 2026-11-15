# querying.ai plugins

Plugins that connect AI coding agents to [querying.ai](https://querying.ai): answers and cited sources from ChatGPT, Gemini, Perplexity, Google AI Overviews, Copilot and other AI engines, prompt research, and GEO monitors.

Every client talks to the remote MCP server `https://mcp.querying.ai/mcp`. Create an API key at https://querying.ai/dashboard/keys and export it before starting the agent:

```bash
export QUERYING_API_KEY=vt_...
```

## Install

Claude Code:

```bash
claude plugin marketplace add OPACTOR-DEV/querying-plugins
claude plugin install querying@querying
```

Codex:

```bash
codex plugin marketplace add OPACTOR-DEV/querying-plugins
```

Then open the plugin directory in Codex and install `querying.ai`.

Cursor: add this repository as a plugin marketplace and install `querying`.

Gemini CLI:

```bash
gemini extensions install https://github.com/OPACTOR-DEV/querying-plugins
```

Any other MCP client: point a Streamable HTTP server at `https://mcp.querying.ai/mcp` with the header `Authorization: Bearer $QUERYING_API_KEY`. Agents that read Agent Skills can use [skills/querying/SKILL.md](skills/querying/SKILL.md).

## Layout

- `plugins/querying/`: the plugin for Claude Code, Codex and Cursor (manifests, MCP config, skill, icons).
- `gemini-extension.json`, `GEMINI.md`: the Gemini CLI extension at the repository root.
- `skills/querying/`: the skill, copied into `plugins/querying/skills/` by `node scripts/sync-skill.mjs`.
- `server.json`: the MCP Registry entry.

Docs: https://docs.querying.ai. License: MIT.
