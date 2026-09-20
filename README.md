# AdLigner for Claude

A senior paid-media strategist for the ad accounts you already run — inside
Claude Code and Cowork.

This plugin bundles AdLigner's remote MCP server plus three portfolio-level
commands. AdLigner itself is a hosted service; you need a free account at
<https://adligner.com> to connect your ad platforms.

## What it does

**Connect once, ask in plain language.** Link Google Ads, Meta Ads, TikTok Ads,
LinkedIn Ads and ChatGPT Ads, plus Google Analytics 4 and Klaviyo, in the
AdLigner web app. Then ask things like "how did last week go", "where am I
wasting spend", or "compare Meta's conversions with what GA4 saw".

**Findings, not dashboards.** The analysis tools work through the checklist an
experienced media buyer would: wasted spend, budget pacing, creative fatigue,
bid efficiency, placement and demographic waste, dayparting gaps, duplicate
targeting, audience overlap, signal health and conversion gaps — applied to your
live data and explained in context.

**Owned and paid together.** Reconcile platform-reported conversions against
GA4, and compare paid revenue with Klaviyo email and SMS revenue, to see which
channel actually drove the sale.

**Changes only with your approval.** Any tool that would modify an account —
pausing, resuming, budgets, targeting, negative keywords, new campaigns —
returns a plain-language preview first and runs only when you confirm. New
campaigns and ads are created paused; Klaviyo campaigns are created as drafts.

**Alerts that watch while you don't.** Set monitors from the conversation
("tell me if Meta CPA goes above 40 this week") and get an email when a
threshold trips.

## Install

Until AdLigner is published in the Claude plugin directory:

```
/plugin marketplace add adligner/adligner-claude-plugin
/plugin install adligner@adligner
/mcp          → select "adligner" → Authenticate
```

The AdLigner consent screen opens in your browser. Approve it and the tools
appear. See [SETUP.md](./SETUP.md) for troubleshooting.

## Commands

The MCP server already exposes per-account expert prompts as slash commands
(`weekly_account_review`, `find_quick_wins`, `explain_finding`) — each takes one
platform and one ad account. These three commands are the layer above them: they
discover every connected account and rank findings across the whole portfolio.

| Command | What it does |
| --- | --- |
| `/adligner:weekly-review` | Reviews every connected account and consolidates one ranked brief: quick wins, needs review, watchlist. |
| `/adligner:quick-wins` | Ranks only reversible, low-risk wins across all accounts by expected savings, with ready-to-run arguments. |
| `/adligner:health` | Setup diagnostic: what is connected, which accounts are enabled, and whether conversion tracking can be trusted. |

## Privacy and data

The plugin adds no hooks and no telemetry. The only network destination is
AdLigner's own MCP server at `https://mcp.adligner.com/mcp`. AdLigner stores
encrypted OAuth tokens, ad account ids and names, and an audit log of tool calls;
metric data is not retained beyond alert evaluations.

- Privacy policy: <https://adligner.com/privacy>
- Terms: <https://adligner.com/terms>
- Support: <https://adligner.com/support> or support@adligner.com

## License

MIT — see [LICENSE](./LICENSE).
