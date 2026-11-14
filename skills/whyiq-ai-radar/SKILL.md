---
name: whyiq-ai-radar
description: Measure and improve weekly AI visibility across ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini, and Claude using WhyIQ AI Radar. Use whenever the user asks about AI search visibility, AEO, GEO, LLM citations, which competitors win on buyer questions, crawler/SSR readiness, or third-party Reddit and review citations.
---

# WhyIQ AI Radar & Citation Gap Workflow

Use this skill when the user wants to inspect their weekly **AI visibility** (the share of AI answers that named them as **Mentioned** or linked to them as **Cited**) across the 5 engines and close citation gaps against competitors. Call tools through the active WhyIQ MCP server (`whyiq_whyiq` in Antigravity plugins, `plugin:whyiq:whyiq` in Claude plugin bundles, or `whyiq` in Claude connectors and manual IDE installs).

Never expose internal skill names in user-facing responses.

## Inline Scorecard (`<agent-embed>` in Antigravity / Markdown in Claude & Cursor)

When reporting AI Radar findings:
- **In Google Antigravity:** Render [assets/radar-card.html](assets/radar-card.html) filled with live tool metrics into `<Artifact Directory Path>/whyiq-radar-card.html` (`UserFacing: true`) and emit `<agent-embed src="file:///<Artifact Directory Path>/whyiq-radar-card.html"></agent-embed>`.
- **In Claude (`claude.ai`, Cowork, Claude Desktop, Claude Code) and Cursor:** Present the scorecard directly in structured Markdown (without `<agent-embed>` tags).
- Display **Measured Weekly AI Visibility** (`AI visibility %` = Mentioned OR Cited), per-engine visibility bars, and up to 3 buyer questions lost to named competitors.
- Always link back to `https://www.whyiq.ai/radar/app` so the user can inspect full weekly answer transcripts and manage tracked buyer questions.

## 1. Check Headlines First (`whyiq_get_site_overview`)
Call `whyiq_get_site_overview` with `domain` to get the current weekly AI visibility rate, Mentioned vs. Cited split, and open AI Radar moves.
- If no Radar scan or completed audit exists yet, render `whyiq-onboarding-card.html` (`https://www.whyiq.ai/analyse?url=<domain>&autopilot=1`) instead of guessing results.

## 2. Inspect the 5 AI Radar Intelligence Views (`whyiq_inspect_radar_intelligence`)
Choose the `view` matching the user's question (optional filters: `engine_filter`, `query_filter`):

| View | When to Use | What It Returns |
| :--- | :--- | :--- |
| `losses_and_moves` | "Where are competitors beating us?" or "What should we fix first for AI visibility?" | Buyer questions where a named rival was recommended instead of you, paired with ranked on-site and off-site moves. |
| `engine_breakdown` | "How do ChatGPT vs. Perplexity vs. Google AI Overviews describe us?" | Per-engine AI visibility (Mentioned + Cited), sentiment, framing, and engine-specific citation mechanics (see [references/engine-mechanics.md](references/engine-mechanics.md)). |
| `page_comparison` | "Why did the AI cite their page instead of ours?" | Side-by-side structural comparison between your page and the rival URL cited by the AI engine. |
| `foundations` | "Can AI crawlers read our site?" | AI crawler access (`GPTBot`, `OAI-SearchBot`, `PerplexityBot`, `ClaudeBot`, `Google-Extended`), SSR raw HTML word count vs. JS DOM, `llms.txt`, and JSON-LD entity graph checks. |
| `offsite_footprint` | "Which third-party sites, Reddit threads, or G2/Trustpilot pages are AI engines citing?" | Third-party domains and community threads cited across buyer questions, plus review-platform and directory gaps. |

## 3. Turn AI Radar Moves into Guarded Code Changes
When shipping an on-site AI Radar move (answer-first block, comparison table, JSON-LD, or `llms.txt`):
1. Call `whyiq_list_autopilot_fixes` with `product_filter: "radar"`.
2. Protect every phrase listed in `keepAnswers` on the target page so shipping one fix never costs existing citations.
3. Ask the user for any `[fill in: ...]` Honesty Gate facts before editing code.
4. For **off-site moves** (Reddit, Hacker News, G2, Capterra, Trustpilot), never commit to Git or auto-post; direct the user to `https://www.whyiq.ai/radar/app/fixes`.
5. Call `whyiq_prepare_fix_bundle`, apply approved edits, and record via `whyiq_verify_and_record_fix` (`Waiting` until the next weekly AI Radar scan).
