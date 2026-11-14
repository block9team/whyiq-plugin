# WhyIQ Plugin

Official public plugin for WhyIQ ([whyiq.ai](https://www.whyiq.ai)). Connect your AI coding assistant directly to your WhyIQ account over remote MCP with 1-click OAuth 2.1 sign-in.

## What This Is

WhyIQ is a conversion rate optimization (CRO) and AI visibility platform. It brings together two complementary systems:

- **WhyIQ Page Scanner:** Simulates 50 realistic buyer personas walking through a live landing page to predict Clarity, **`CTA Pull`** (scored 0 to 100), and heuristic on-page AI recommendation readiness, then ranks exact fixes you can apply in code.
- **WhyIQ AI Radar:** Measures weekly AI visibility (the share of AI answers that name you as Mentioned or link to you as Cited) across ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini, and Claude.

This repository packages WhyIQ's client workflows, guardrails, skills, and remote MCP configuration so supported AI coding assistants can inspect your live WhyIQ findings right where you write code.

## Why It Exists

Most teams waste hours copying audit feedback out of browser dashboards, guessing which headline or pricing change will actually move conversions, or rewriting copy in the dark without knowing which passages AI engines already cite.

The WhyIQ plugin removes that copy-paste loop:

1. Your assistant pulls ranked visitor objections and missed buyer questions straight into your IDE.
2. You review exact before-and-after code changes inside your local files instead of editing by hand from a PDF or screenshot.
3. Every fix follows strict honesty and approval rules so your assistant never ships fabricated claims or unapproved edits.

## What It Does

- **Surfaces visitor hesitation inside your codebase:** Inspect 50-persona simulation objections, Clarity gaps, and `CTA Pull` drivers while looking at the exact component files responsible.
- **Exposes weekly AI visibility gaps:** Check which buyer prompts competitors won in AI Radar and preserve cited passages (`keepAnswers`) before touching copy.
- **Enforces the Honesty Gate:** Automatically pauses and asks you to fill `[fill in: ...]` placeholders whenever a recommendation needs real customer counts, case study metrics, pricing, SLAs, certifications, or testimonials.
- **Follows your 4-Mode Switchboard:** Honors per-category rules (`off`, `flag`, `stage`, or `auto`) configured in your WhyIQ account. Off-site community and review drafts (such as Reddit or review directories) are always held for human review and never posted automatically.
- **Creates 1-click rollback checkpoints:** Calls WhyIQ before editing so your `before_snapshot` and SHA-256 hash are stored in the Applied Fixes Ledger, then records `after_snapshot` once edits land so any fix can be rolled back cleanly.
- **Links back to `whyiq.ai` for heavy workflows:** Provides direct handoffs when you need to run a fresh 50-visitor scan on `whyiq.ai/analyse`, explore full AI Radar history, approve off-site drafts, or manage your plan.

## 1-Click Sign In

The remote MCP endpoint lives at:

`https://www.whyiq.ai/api/mcp`

When an MCP client connects without a bearer token, WhyIQ returns HTTP `401 Unauthorized` with standard OAuth 2.1 Protected Resource discovery (`/.well-known/oauth-protected-resource` and `/.well-known/oauth-authorization-server`), RFC 7591 Dynamic Client Registration (`/api/oauth/register`), and PKCE `S256` consent (`/oauth/authorize`).

During sign-in on `whyiq.ai`, you choose your verified domain and Switchboard preset. No static API keys need to be copied into your repository.

## Try These Starter Prompts

Once signed in, try asking your assistant:

- `Run a WhyIQ overview on my site and list the top-ranked CRO and AI Radar fixes`
- `Inspect my 50-visitor simulation to see why visitors hesitate on our hero and pricing`
- `Show which competitors beat us on buyer questions in AI Radar this week and stage a fix`

## What Is Included (`v1.1.1`)

- **MCP Server (`whyiq_whyiq` / `whyiq`):** Remote Streamable HTTP connection to `https://www.whyiq.ai/api/mcp` exposing 8 tools:
  - `whyiq_get_site_overview`
  - `whyiq_inspect_radar_intelligence`
  - `whyiq_inspect_visitor_simulation`
  - `whyiq_list_autopilot_fixes`
  - `whyiq_prepare_fix_bundle`
  - `whyiq_verify_and_record_fix`
  - `whyiq_rollback_fix`
  - `whyiq_configure_switchboard`
- **Agent Skills (`skills/`):**
  - `whyiq-best-practices`: Entry router, capability scope, and connection diagnostics.
  - `whyiq-autopilot`: Page Scanner review, `CTA Pull` and on-page AI readiness diagnostics, 4-Mode Switchboard controls, and guarded fix execution.
  - `whyiq-ai-radar`: Weekly AI visibility checks across supported engines, competitor citation gap analysis, crawler readiness, and preservation checks.
- **Guardrails (`rules/AGENTS.md`):** Always-on instructions enforcing the Honesty Gate, 4-Mode Switchboard boundaries, ledger recording, and the Bright Line separating measured AI Radar visibility from predicted Page Scanner metrics.
- **Portable Host Configs & Templates:** Manifests (`plugin.json`, `gemini-extension.json`, `.claude-plugin/plugin.json`, `mcp_config.json`, `mcp.json`) plus interactive HTML report templates in `assets/` and skill references.

## Cross-IDE Setup

### Antigravity

Install WhyIQ from the Antigravity Marketplace (or add `https://github.com/block9team/whyiq-plugin`), then complete the OAuth 2.1 Sign-In prompt when invoking any WhyIQ workflow.

### Cursor, Claude Code, and Gemini CLI

Clone this repository or point your client's MCP configuration (`mcp.json` or `mcp_config.json`) to `https://www.whyiq.ai/api/mcp`, then follow your client's OAuth sign-in flow.

For client snippets and setup notes, visit `https://www.whyiq.ai/mcp`.

## Plain-Text Explainers & AI Reference

- [ABOUT.txt](ABOUT.txt): Unformatted plain ASCII overview explaining what WhyIQ is, why this plugin exists, and what it does.
- [llms.txt](llms.txt): Structured plain-text specification of WhyIQ tools, OAuth endpoints, and guardrails for AI agents and crawlers.

## Repository Boundary & License

This public `MIT`-licensed repository contains only open plugin manifests, agent skills, safety rules, and remote MCP configuration. All proprietary crawler pipelines, page simulation engines, and user account records stay on `whyiq.ai` and are accessed strictly through your signed-in OAuth 2.1 session.

## Links

- Website: https://www.whyiq.ai
- Plugin & MCP Portal: https://www.whyiq.ai/mcp
- Run a Page Scan: https://www.whyiq.ai/analyse
- AI Radar Workspace: https://www.whyiq.ai/radar/app
- Plans & Pricing: https://www.whyiq.ai/pricing
