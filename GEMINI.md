# querying.ai

querying.ai runs real-browser prompts against AI answer engines and returns each answer with its sources. The tools come from the `querying` MCP server, which connects by signing in to a querying.ai account.

## Pick the tool

- One answer now: `run_prompt` with `taskType` (for example `CHATGPT`, `GEMINI`, `PERPLEXITY`, `GOOGLE`, `AIMODE`, `COPILOT`, `NAVER_AI_BRIEF`, `NAVER_AI_TAB`), `prompt`, and `country`. It waits up to 50 seconds. `GOOGLE_NEWS` and `GOOGLE_PLACES` take their own fields (`pages`; `city` or `uule`, `limit`).
- Many prompts or slow engines: `submit_prompt` for each, then `get_task` with `waitSeconds`. For thousands of tasks use `create_batch`, `get_batch` and `list_batch_items`.
- A run that timed out is still running. Read it with `get_task`. Submitting again is charged again.
- Web search with the passages that answer: `web_search`.
- What people ask about a topic: `research_prompts` with a `seed` and `country` (`KR` or `US`). It returns prompts with monthly search demand.
- Storefront product pages: `read_product`. How AI shopping engines show a product: `run_product_lookup`.
- One store's record across AI engines: `submit_place_lookup`, then `get_place_lookup`.
- How an answer changes by place: `submit_location_grid`, then `get_location_grid`.
- What ChatGPT cannot read on a page: `run_geo_score`. How an answer relates to the pages it cited: `analyze_citations`.
- Track a brand over time: `get_monitor_capabilities`, then `create_monitor`, then `get_monitor_analytics`, `get_monitor_sources`, `get_monitor_citations`, `get_monitor_results` and `get_monitor_answer`. Use `suggest_monitor_prompts` to choose prompts. `test_monitor_alert` only when the user asks to test alert delivery.
- Balance, usage, engines and countries: `get_credits`, `get_usage`, `get_capabilities`, `list_countries`, `list_states`, `get_queue_status`.

## Working rules

- Credits are charged per task (about 1 to 1.25 for answer engines; `web_search` 0.5 or 2). Read `get_credits` and state how many calls and credits a large batch or a location grid will spend before you start it.
- Use the engine and country the user's buyers use. Compare the same prompt across engines by running it once per `taskType`.
- Report answers with their `sources`. Say which engine and country each answer came from, and do not merge answers from different engines.
- If the `querying` tools are missing or a call says the server needs authentication, ask the user to sign in: `/mcp` in Claude Code, `codex mcp login querying` in Codex, `/mcp auth querying` in Gemini CLI, or Connect in Cursor. Do not ask for an API key in chat.
- Engine details and fields: https://docs.querying.ai/engines/overview
