# querying.ai

querying.ai runs real-browser prompts against AI answer engines and returns each answer with its sources. The tools come from the `querying` MCP server and need the `QUERYING_API_KEY` environment variable (a `vt_` key from https://querying.ai/dashboard/keys).

## Pick the tool

- One answer now: `run_prompt` with `taskType` (for example `CHATGPT`, `GEMINI`, `PERPLEXITY`, `GOOGLE`, `AIMODE`, `COPILOT`, `NAVER_AI_BRIEF`), `prompt` (`query` for Google and Naver engines), and `country`. It waits up to 50 seconds.
- Many prompts or slow engines: `submit_prompt` for each, then `get_task` with `waitSeconds`.
- A run that timed out is still running. Read it with `get_task`. Submitting again is charged again.
- What people ask about a topic: `research_prompts` with a `seed` and `country` (`KR` or `US`). It returns prompts with monthly search demand.
- Storefront product pages: `read_product` with a product URL.
- Track a brand over time: `get_monitor_capabilities`, then `create_monitor`, then `get_monitor_analytics`, `get_monitor_sources` and `get_monitor_answer`. Use `suggest_monitor_prompts` to choose prompts. `test_monitor_alert` only when the user asks to test alert delivery.

## Working rules

- Credits are charged per answer (about 1 to 1.25 for answer engines). Say how many calls you will make before a large batch.
- Use the engine and country the user's buyers use. Compare the same prompt across engines by running it once per `taskType`.
- Report answers with their `sources`. Say which engine and country each answer came from, and do not merge answers from different engines.
- If a call reports `MISSING_API_KEY`, ask the user to create a key at https://querying.ai/dashboard/keys and set `QUERYING_API_KEY`. Do not ask for the key in chat.
- Engine details and fields: https://docs.querying.ai/engines/overview
