---
name: whyiq-ai-radar
description: Measure and improve weekly AI visibility across ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini, and Claude using WhyIQ AI Radar. Use whenever the user asks about AI search visibility, AEO, GEO, LLM citations, which competitors win on buyer questions, crawler/SSR readiness, or third-party Reddit and review citations.
---

# WhyIQ AI Radar & Citation Gap Workflow

Use this skill when the user wants to inspect their weekly **AI visibility** (the share of AI answers that named them as **Mentioned** or linked to them as **Cited**) across the 5 real engines and close citation gaps against competitors.

## 1. Check Headlines First (`whyiq_get_site_overview`)
Call `whyiq_get_site_overview` with `domain` to get the current weekly AI visibility rate, Mentioned vs. Cited split, and open AI Radar moves.

## 2. Inspect the 5 AI Radar Intelligence Views (`whyiq_inspect_radar_intelligence`)
Choose the `view` that matches the user's question (optional filters: `engine_filter`, `query_filter`):

| View | When to Use | What It Returns |
| :--- | :--- | :--- |
| `losses_and_moves` | "Where are competitors beating us?" or "What should we fix first for AI visibility?" | Buyer questions where a named rival was recommended instead of the user, paired with the ranked on-site and off-site moves to win those questions. |
| `engine_breakdown` | "How do ChatGPT vs. Perplexity vs. Google AI Overviews describe us?" | Per-engine AI visibility (Mentioned + Cited), sentiment, framing, and engine-specific citation mechanics. |
| `page_comparison` | "Why did the AI cite their page instead of ours?" | Side-by-side structural comparison between the user's page and the rival URL cited by the AI engine (answer-first blocks, tables, schema, freshness). |
| `foundations` | "Can AI crawlers read our site?" | AI crawler access (`GPTBot`, `OAI-SearchBot`, `PerplexityBot`, `ClaudeBot`, `Google-Extended`), SSR raw HTML word count vs. JS-rendered DOM, `llms.txt`, and JSON-LD entity graph checks. |
| `offsite_footprint` | "Which third-party sites, Reddit threads, or G2/Trustpilot pages are AI engines citing?" | Third-party domains and community threads cited across buyer questions, plus review-platform and directory gaps. |

## 3. Turn AI Radar Moves into Guarded Code Changes
When the user wants to ship an on-site AI Radar move (such as adding an answer-first section, a comparison table, FAQPage/SoftwareApplication JSON-LD, or `llms.txt`):
1. Call `whyiq_list_autopilot_fixes` with `product_filter: "radar"`.
2. Check `keepAnswers` on the target page: never delete passages that already win citations on other tracked buyer questions.
3. Check `unresolvedPlaceholders`: ask the user for any `[fill in: ...]` facts before editing.
4. Call `whyiq_prepare_fix_bundle`, apply the update, and record it with `whyiq_verify_and_record_fix` so the AI Radar Move is marked Shipped and queued for verification on the next weekly scan.
