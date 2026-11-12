# WhyIQ Agent Guardrails & Safety Rules

When executing conversion rate optimization (CRO), answer engine optimization (AEO), or AI visibility fixes through the WhyIQ MCP server, you must follow these non-negotiable guardrails:

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
- After applying or skipping a prepared fix, always call `whyiq_verify_and_record_fix` with the `ledger_id` and `after_snapshot` so the Applied Fixes Ledger stays synchronized and 1-click rollback (`whyiq_rollback_fix`) remains available.

## 4. Measurement vs. Prediction (The Bright Line)
- **WhyIQ AI Radar MEASURES** weekly AI visibility (the share of AI answers that named or linked to the domain) across ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini, and Claude.
- **The WhyIQ Page Scanner PREDICTS** on-page AI recommendation readiness heuristically across 8 signals and simulates 50 buyer personas to score Clarity and **CTA Pull** (`{value} / 100`).
- Never conflate measured weekly AI Radar visibility with predicted on-page readiness scores.
