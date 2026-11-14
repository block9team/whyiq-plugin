# WhyIQ Plugin for Google Antigravity, Cursor & Claude Code

Official MIT-licensed plugin for **[WhyIQ](https://www.whyiq.ai)**: 50-visitor CRO behavioral simulations, **CTA Pull** scoring, on-page AI citability readiness predictions, weekly **AI Radar** visibility measurements across ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini, and Claude, and guarded 1-click code fixes inside your IDE.

## 1-Click Sign In (OAuth 2.1 + PKCE)

No manual API token copy-pasting required:
1. Install or enable **WhyIQ** in Google Antigravity (`https://github.com/block9team/whyiq-plugin`).
2. Click **Sign in** on the WhyIQ plugin card.
3. Authorize access in your browser (`https://www.whyiq.ai/oauth/authorize`), select your verified website scope, and pick your default 4-Mode Switchboard preset.
4. Antigravity completes PKCE `S256` token exchange automatically against `https://www.whyiq.ai/api/oauth/token` and scopes `https://www.whyiq.ai/api/mcp`.

## What Is Included (`v1.1.0`)

- **3 Coordinated Skills:**
  - `whyiq-best-practices`: Entry router, OAuth connection check, clean state templates, and web-platform handoffs.
  - `whyiq-autopilot`: 50-visitor CRO simulation drill-down across 5 lenses (`synthesis`, `emotional_and_trust`, `scroll_and_visibility`, `archetype_voices`, `technical_audits`), Switchboard control, and guarded fix execution (`whyiq_prepare_fix_bundle` -> `whyiq_verify_and_record_fix` -> `whyiq_rollback_fix`).
  - `whyiq-ai-radar`: Weekly AI visibility diagnostics across 5 views (`losses_and_moves`, `engine_breakdown`, `page_comparison`, `foundations`, `offsite_footprint`) with `keepAnswers` protection.
- **3 Inline Chat Scorecards (`<agent-embed>`):** `overview-card.html`, `radar-card.html`, and `onboarding-card.html`.
- **2 Dynamic Side-Pane HTML Workbenches:** `staged-review.html` (Fix/Leave selector + `[fill in: ...]` Honesty Gate form) and `autopilot-report.html` (SHA-256 diffs + 1-click rollback).
- **1 Always-On Rule File:** `rules/AGENTS.md` enforcing the Honesty Gate, 4-Mode Switchboard, `keepAnswers` protection, and measurement vs. prediction clarity.
- **1 Remote Streamable HTTP MCP Server:** `https://www.whyiq.ai/api/mcp` exposing 8 progressive-disclosure tools, 6 resource templates, and 3 slash prompts.

## Try These Starter Prompts

1. `Run a WhyIQ overview on my site and list the top-ranked CRO and AI Radar fixes`
2. `Inspect my 50-visitor simulation to see why visitors hesitate on our hero and pricing`
3. `Show which competitors beat us on buyer questions in AI Radar this week and stage a fix`

## Cross-IDE Setup (Cursor, Claude Code, Gemini CLI)

- **Claude Code / Gemini CLI:** Uses `.claude-plugin/plugin.json` and `gemini-extension.json` pointing to `https://www.whyiq.ai/api/mcp`.
- **Manual Token Mode:** Prefer connecting a pre-scoped token from `https://www.whyiq.ai/dashboard/autopilot?tab=mcp`? Pass `Authorization: Bearer whyiq_mcp_...` or `?token=...&domain=yourdomain.com`.

## Repository Boundary & Privacy

This public MIT repository contains only declarative manifests, skill workflows, inline scorecard templates, and safety rules. WhyIQ's headless Chromium 50-visitor simulation engine, weekly AI Radar crawler/dataset, OAuth token store, and user telemetry remain server-side on `https://www.whyiq.ai`.

## Links

- MCP & Plugin Docs: https://www.whyiq.ai/mcp
- Live Autopilot Guide: https://www.whyiq.ai/docs/autopilot
- Support & Website: https://www.whyiq.ai
