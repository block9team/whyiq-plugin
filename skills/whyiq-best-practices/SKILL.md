---
name: whyiq-best-practices
description: Entry router and connection diagnostics for the WhyIQ plugin. Read this first when a user asks what WhyIQ can do, whether WhyIQ is connected, what plan or Switchboard rules are active, or requests an action outside MCP scope (such as auto-posting to Reddit or running a live 50-visitor Chromium simulation locally).
---

# WhyIQ Best Practices & Entry Router

Use this skill first whenever the request is about WhyIQ capabilities, connection/authentication status, plan limits, or when routing between WhyIQ's two products (50-visitor CRO Page Scanner vs. weekly AI Radar visibility).

Never expose internal skill names in user-facing responses. Describe outcomes in plain product terms.

## Step 1: Resolve the Active MCP Server Name
Depending on how WhyIQ was installed in the user's IDE, its MCP server registers under one of these server names:
- Google Antigravity plugin installs: `whyiq_whyiq`
- Manual user `mcp_config` / Cursor / Claude Code / Gemini CLI installs: `whyiq`

Inspect whichever WhyIQ MCP server is available in the current session and call its tools through that server name.

## Step 2: Check Connection Before Guessing
If authentication status is uncertain or a tool call returns `401 Unauthorized`:
1. Call `list_plugin_accounts` (if available in Antigravity) to verify whether the WhyIQ OAuth 2.1 connection is signed in.
2. Never guess, fabricate, or extrapolate scores, buyer questions, or visitor quotes when WhyIQ is disconnected or unauthenticated.
3. Read [references/reply-templates.md](references/reply-templates.md) and give the user the **Sign-In Needed** template together with `[WhyIQ](customization://whyiq)` (or follow tool error instructions if asked to render `<plugin-card>`).

## Step 3: Route to the Right Workflow
Once signed in, route immediately based on intent:
- **Site health check, CRO simulation, page friction, CTA Pull, Switchboard, or applying/rolling back code fixes:** follow [../whyiq-autopilot/SKILL.md](../whyiq-autopilot/SKILL.md).
- **Weekly AI visibility, ChatGPT / Perplexity / Google AI Overviews / Gemini / Claude citations, rival wins, AI crawler foundations, or Reddit/review co-pilot:** follow [../whyiq-ai-radar/SKILL.md](../whyiq-ai-radar/SKILL.md).
- **Overview of what WhyIQ does:** summarize from [references/introduction.md](references/introduction.md) and suggest the 3 starter prompts cleanly.

## Step 4: Handle Out-of-Scope or Web-Platform Handoff States Calmly
Use the exact response patterns in [references/reply-templates.md](references/reply-templates.md) when any of these states appear:
- `no_completed_scan`: Direct the user to run a 50-visitor simulation at `https://www.whyiq.ai/analyse?url=<domain>&autopilot=1` and render `onboarding-card.html` inline.
- `freeFixCreditsRemaining === 0` (on `free_connected` tier): Direct the user to `https://www.whyiq.ai/pricing?from=plugin` to unlock unlimited fixes.
- `offsite` moves (Reddit, Hacker News, G2, Trustpilot, Capterra, directories): Never automate off-site posting; direct the user to review and copy/publish on `https://www.whyiq.ai/radar/app/fixes`.

## Standing WhyIQ Bright Line
- **WhyIQ AI Radar MEASURES** weekly AI visibility (the share of AI answers where your brand is **Mentioned** or **Cited**) across ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini, and Claude. Never describe Radar as real-time or call pooled visibility "mentions" or "citation rate".
- **The WhyIQ Page Scanner PREDICTS** on-page AI recommendation readiness heuristically across 8 signals and simulates 50 buyer personas to score Clarity and **CTA Pull** (`{value} / 100`, integer, never `%`). Never tie Google to the 50-visitor simulation.
