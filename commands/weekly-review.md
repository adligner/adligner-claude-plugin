---
description: Cross-platform weekly review of every connected ad account, ranked as one brief
argument-hint: '[time window, e.g. "last 7 days", "last 30 days"]'
---
Run a weekly review across **every** connected ad account and consolidate it into one brief for $ARGUMENTS (default: last 7 days).

The AdLigner MCP server ships per-account review prompts, but they take a single `platform` + `accountId`. This command is the portfolio layer on top of them.

1. Call `list_connected_ad_platforms` to discover which platforms are connected, which ad accounts are enabled on each, and what appears under `dataSources`. If nothing is connected, stop and tell the user to link a platform at https://adligner.com — do not guess account ids.
2. For each enabled account, run the read-only `analyze_*` / `mine_*` tools that exist for that platform — budget pacing, wasted spend, bid efficiency, structure health, conversion gaps, plus whatever else that platform supports (dayparting, creative fatigue, audience overlap, placement waste, signal health). Only call tools whose platform is actually connected.
3. If `dataSources` lists a Google Analytics property, also run `compare_conversions_with_ga4` per account. Lead with campaigns whose platform-reported conversions exceed GA4 by more than 2x, and campaigns whose spend produced no GA4-tagged traffic — these are tracking problems to fix *before* judging performance.
4. If `dataSources` lists Klaviyo, run `compare_owned_vs_paid_revenue` and `get_klaviyo_lifecycle_health` for the same window and fold in findings of medium priority or higher, prefixed "Email/SMS:".
5. Present **one** consolidated brief, ranked across all platforms by expected impact — not one section per platform:
   - **Quick wins** — reversible, high-ROI moves, clearable immediately.
   - **Needs review** — higher-impact or higher-risk changes with the tradeoff spelled out.
   - **Watchlist** — trending wrong, not yet worth acting on.
6. For every item name the platform and account, the finding in plain language, why it matters, the estimated impact from the real numbers, and the exact mutation tool plus `recommendedArgs` you would run.
7. Close with a spend-and-results table, one row per account, so the portfolio is visible at a glance. Then ask which actions to prepare.

Advise only. Do not call any mutation tool during this review, even if the user pre-authorizes it — they confirm each change separately afterwards. Reply in the language the user wrote in.
