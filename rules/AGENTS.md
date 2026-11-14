# WhyIQ Agent Guardrails & Safety Rules

When executing conversion rate optimization (CRO), answer engine optimization (AEO), or AI visibility fixes through the WhyIQ MCP server (`whyiq_whyiq` or `whyiq`), you must follow these non-negotiable guardrails:

## 1. The Honesty Gate (`[fill in: ...]` Placeholders)
- Never invent, guess, or fabricate customer numbers, case study metrics, pricing, SLAs, security certifications, or testimonials.
- Whenever `whyiq_list_autopilot_fixes` or `whyiq_prepare_fix_bundle` returns unresolved `[fill in: ...]` placeholder slots, pause and ask the user for the real facts first, then pass their exact answers via `resolved_placeholders` in `whyiq_prepare_fix_bundle`.

## 2. Respect the 4-Mode Switchboard
- Every fix in WhyIQ belongs to one of 18 sub-elements governed by the user's 4-Mode Switchboard (`off`, `flag`, `stage`, `auto`):
  - `off`: Do not surface or touch items in this category.
  - `flag`: Report the finding to the user as read-only intelligence; do not stage or edit files.
  - `stage`: Prepare the fix and present a diff or preview for explicit user approval before applying.
  - `auto`: Permitted for direct execution once `whyiq_prepare_fix_bundle` succeeds with zero unresolved `[fill in: ...]` placeholders.
- Off-site community and review drafts (Reddit, Hacker News, G2, Capterra, Trustpilot) are always held for human review and must never be posted automatically.

## 3. Mandatory Ledger Recording & 1-Click Rollback
- Always call `whyiq_prepare_fix_bundle` before modifying code or CMS content so WhyIQ captures the `before_snapshot` and SHA-256 hash.
- Preserve every passage returned in `keepAnswers` on pages with existing AI Radar citations.
- After applying or skipping a prepared fix, always call `whyiq_verify_and_record_fix` with the `ledger_id` and `after_snapshot` so the Applied Fixes Ledger stays synchronized and 1-click rollback (`whyiq_rollback_fix`) remains available.

## 4. Measurement vs. Prediction (The Bright Line)
- **WhyIQ AI Radar MEASURES** weekly AI visibility (the share of AI answers that named you as Mentioned or linked to you as Cited) across ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini, and Claude. Never describe AI Radar as real-time.
- **The WhyIQ Page Scanner PREDICTS** on-page AI recommendation readiness heuristically across 8 signals and simulates 50 buyer personas to score Clarity and **CTA Pull** (`{value} / 100`, integer).
- Never conflate measured weekly AI Radar visibility with predicted on-page readiness scores, and never mention Google in sentences describing the 50-visitor behavioral simulation.

## 5. OAuth Connection & Web Platform Handoffs
- If the WhyIQ MCP server returns `401 Unauthorized` or is disconnected, never fabricate audit scores or objections from memory. Direct the user to sign in via OAuth 2.1 on their WhyIQ plugin page so their domain and Switchboard preset are scoped automatically.
- Direct unscanned sites (`no_completed_scan`) to run a 50-visitor scan on `https://www.whyiq.ai/analyse`, off-site moves to `https://www.whyiq.ai/radar/app/fixes`, and exhausted Free Tier credits to `https://www.whyiq.ai/pricing?from=plugin`.
