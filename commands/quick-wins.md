---
description: Rank reversible, low-risk wins across every connected account by expected savings
argument-hint: '[time window, e.g. "last 30 days"]'
---
Find the fastest wins across **all** connected ad accounts for $ARGUMENTS (default: last 30 days) and rank them as one list.

1. Call `list_connected_ad_platforms` for connected platforms, enabled accounts and `dataSources`. If nothing is connected, send the user to https://adligner.com to link a platform and stop.
2. Per enabled account, run only the read-only tools that surface reversible, low-risk upside: wasted spend, negative-keyword mining, budget pacing, and — where the platform has them — placement waste, demographic waste and geo waste. Skip structural or strategic checks; those belong in `/adligner:weekly-review`.
3. If a GA4 property appears under `dataSources`, run `compare_conversions_with_ga4` and put tracking discrepancies at the top: a campaign reporting 2x GA4's conversions is not a win to harvest, it is a measurement problem.
4. If Klaviyo appears under `dataSources`, run `get_klaviyo_lifecycle_health` and include medium-or-higher findings prefixed "Email/SMS:".
5. Return **one** ranked list, highest expected monthly savings or lift first, across every platform. For each: platform and account, the finding in plain language, the number it is based on, the estimated impact, and the exact mutation tool plus `recommendedArgs`.
6. State the total recoverable spend at the top so the user sees the size of the prize before the detail.
7. Ask which ones to prepare for confirmation.

Advise only — call no mutation tool here. Reply in the language the user wrote in.
