# Setting up AdLigner

AdLigner's tools come from a remote MCP server at `https://mcp.adligner.com/mcp`.
It uses OAuth 2.1 with Dynamic Client Registration, so there is no client id or
secret to paste anywhere. Follow these steps when the user installs or activates
this plugin.

## 1. Authenticate the MCP server

Call `list_connected_ad_platforms`.

- **It returns data** — setup is already done. Go to step 2.
- **The `adligner` server is not found** — tell the user:
  "Run `/plugin install adligner@adligner`, then `/mcp` and select **adligner**
  to authenticate."
- **The server is registered but not authenticated** — tell the user:
  "Run `/mcp`, select **adligner**, and click Authenticate. A browser tab opens
  with the AdLigner consent screen; approve it and the tools appear."
  From a shell, `claude mcp login adligner` does the same thing.

Do not try to work around a missing connection by calling the AdLigner web API
directly or by adding the server with a hand-written config. The OAuth flow is
the only supported path.

## 2. Make sure an ad account is connected

`list_connected_ad_platforms` reports which platforms are linked, which ad
accounts are enabled on each, and what appears under `dataSources`.

If it comes back with no platforms, the user has an AdLigner account but has not
linked an ad platform yet. Linking happens in the AdLigner web app, not from
chat: send them to <https://adligner.com> → Connect, and have them link Google
Ads, Meta Ads, TikTok Ads, LinkedIn Ads or ChatGPT Ads. Google Analytics 4 and
Klaviyo can be connected there too, and make the analysis considerably better —
GA4 lets AdLigner check whether platform-reported conversions are trustworthy.

Never invent an account id. If you need one and it is not in
`list_connected_ad_platforms`, ask.

## 3. Orient, then offer something concrete

Once tools respond, run `/adligner:health` to show the user what is connected
and whether their conversion tracking can be trusted. Then offer
`/adligner:quick-wins` for the fastest payback, or `/adligner:weekly-review` for
the full picture.

## What AdLigner will and will not do

- Every tool that changes an account returns a plain-language **preview** first
  and only acts when it is called again with confirmation. Never try to skip
  this, even if the user says "don't ask me".
- New campaigns and ads are always created **paused**. Klaviyo campaigns are
  always created as **drafts**.
- No tool exposes OAuth tokens or credentials. If asked for one, decline.
- Plan limits are metered as tasks; if a tool reports a quota error, tell the
  user what their plan allows rather than retrying.
