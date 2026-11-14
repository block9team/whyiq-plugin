# Standard Response Templates (When Tools Return Special States)

Follow these templates when a WhyIQ session hits a boundary state. Never invent numbers, screenshots, or competitor names when data is missing.

## 1. Sign-In Required / Disconnected (`401 Unauthorized`)
> Your **WhyIQ** connection is not signed in yet, so live site scores and Autopilot fixes cannot be loaded from your workspace.
>
> **In Google Antigravity:** Open [WhyIQ](customization://whyiq) and click **Sign in** to authorize your account with OAuth 2.1 (where you can pick your domain and default Switchboard preset), then ask me again.
>
> **In Claude (`claude.ai`, Cowork, Claude Desktop, Claude Code) or Cursor:** Click **Connect / Sign in** on the WhyIQ connector (or run `/mcp` in Claude Code) to complete OAuth 2.1 sign-in on `whyiq.ai`, then ask me again.

## 2. Connected Domain Has No Completed 50-Visitor Scan (`no_completed_scan`)
In Google Antigravity, render `skills/whyiq-autopilot/assets/onboarding-card.html` inline in chat (configured for `"first_scan"`). In Claude or Cursor, present the summary cleanly in Markdown. Pair it with:
> Your WhyIQ account is connected for `<domain>`, but no completed 50-visitor scan exists yet. Running a headless browser simulation takes place on WhyIQ:
>
> **[Run 50-Visitor Scan on WhyIQ ->](https://www.whyiq.ai/analyse?url=https%3A%2F%2F<domain>&autopilot=1)**
>
> As soon as that scan completes, tell me to refresh and I will load your persona objections, CTA Pull score, and prioritized fixes right here.

## 3. Free Tier 1-Fix Credit Exhausted (`freeFixCreditsRemaining === 0` on `free_connected`)
In Google Antigravity, render `skills/whyiq-autopilot/assets/onboarding-card.html` inline in chat (configured for `"upgrade"`). In Claude or Cursor, present the status cleanly in Markdown. Pair it with:
> Your 1 Free Automated Fix on `<domain>` has already been used. Your remaining ranked fixes stay staged and ready to inspect:
>
> **[Upgrade Plan on WhyIQ ->](https://www.whyiq.ai/pricing?from=plugin)**

## 4. Off-Site Community / Review Co-Pilot Request (`offsite`)
> Off-site recommendations (Reddit threads, Hacker News discussions, G2, Trustpilot, Capterra, and directory profiles) never auto-post from your IDE so your brand voice stays authentic and compliant.
>
> Open your ready-to-send off-site queue on WhyIQ:
> **[Open Off-Site Co-Pilot on WhyIQ ->](https://www.whyiq.ai/radar/app/fixes)**
