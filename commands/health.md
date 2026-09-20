---
description: Check the AdLigner setup — connections, enabled accounts, data sources and tracking trust
---
Diagnose whether this AdLigner setup is sound, before anyone reads a performance number from it. This is a setup check, not a performance review.

1. Call `list_connected_ad_platforms`. Report, as a table: each connected platform, its enabled ad accounts, token health, and what appears under `dataSources` (Google Analytics 4, Klaviyo).
2. If a platform is connected but has no enabled account, or a token needs reauthorization, say so plainly and link https://adligner.com to fix it. Use `get_platform_connection_status` for detail on a platform that looks wrong.
3. For each enabled account, check that conversion tracking is trustworthy:
   - Run the platform's `analyze_*_conversion_gaps` tool.
   - On Meta, also run `analyze_meta_signal_health`.
   - If a GA4 property is connected, run `compare_conversions_with_ga4` over the last 30 days and flag any campaign where platform-reported conversions exceed GA4 by more than 2x, or where spend produced no GA4-tagged traffic.
4. Call `get_automation_rule_support` to report which connected platforms support native automation rules, so the user knows what is available to them.
5. Finish with a short verdict in three buckets: **working**, **needs attention** (with the one action that fixes each), and **not connected yet** (what connecting it would add). Name specific accounts, never generic advice.

Read-only throughout — call no mutation tool. Reply in the language the user wrote in.
