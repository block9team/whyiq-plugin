# What WhyIQ Does Inside Your IDE

WhyIQ combines two diagnostic engines and a guarded fix execution layer inside Google Antigravity, Cursor, and Claude Code:

1. **WhyIQ Page Scanner (Prediction & Behavioral Simulation):**
   - Simulates 50 distinct buyer personas browsing your live rendered page.
   - Scores landing page Clarity and **CTA Pull** (`0` to `100` integer scale) with verbatim objections by archetype and scroll depth.
   - Predicts on-page AI recommendation readiness heuristically across 8 signals and runs 7-dimension WCAG AA + Search Rank technical audits.

2. **WhyIQ AI Radar (Weekly AI Visibility Measurement):**
   - Measures weekly AI visibility (Mentioned OR Cited) on buyer questions across ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini, and Claude.
   - Surfaces exact buyer questions where named competitors win recommendations instead of you, paired with ranked on-site content moves and off-site community/review moves.

3. **Guarded Autopilot & 4-Mode Switchboard:**
   - Governs 18 fix types across 4 modes (`off`, `flag`, `stage`, `auto`).
   - Enforces the **Honesty Gate**: missing business facts stay as `[fill in: ...]` placeholders until you provide real numbers.
   - Captures a pre-change SHA-256 snapshot (`before_snapshot`) and records every edit in the Applied Fixes Ledger with 1-click rollback (`whyiq_rollback_fix`).

## The 4 Interface Surfaces

1. **1-Click OAuth 2.1 + PKCE Sign-In:** Connect your WhyIQ account without copying API tokens manually (`https://www.whyiq.ai/oauth/authorize`).
2. **Inline Chat Scorecards (`<agent-embed>`):** Compact `< 420px` cards showing weekly AI visibility alongside 50-visitor CRO metrics directly in chat.
3. **Interactive Side-Pane Workbenches:** Dynamic HTML selectors (`whyiq-staged-review.html` and `whyiq-autopilot-report.html`) to toggle Fix/Leave, fill Honesty Gate facts, inspect diffs, and trigger rollback.
4. **WhyIQ Web Platform Bridges:** Deep links back to `https://www.whyiq.ai/analyse`, `/results/<scanId>`, `/radar/app`, `/radar/app/fixes`, and `/pricing` whenever headless browser scanning, full 200-answer Radar exploration, or off-site publishing is needed.

## Three Great Starter Prompts

1. `"Run a WhyIQ overview on my site and list the top-ranked CRO and AI Radar fixes"`
2. `"Inspect my 50-visitor simulation to see why visitors hesitate on our hero and pricing"`
3. `"Show which competitors beat us on buyer questions in AI Radar this week and stage a fix"`
