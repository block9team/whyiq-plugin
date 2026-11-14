# WhyIQ AI Radar Engine Mechanics & The Bright Line

## 1. Measurement vs. Prediction (The Bright Line)
- **WhyIQ AI Radar MEASURES** weekly **AI visibility**: the share of scanned AI answers across ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini, and Claude that **Mentioned** (named your brand) or **Cited** (linked to your domain).
- Never call WhyIQ AI Radar "real-time"; scans run on a weekly measurement cadence so before/after moves can be verified cleanly on the next weekly run.
- Never call the pooled visibility metric "mentions", "citations", or "citation rate"; always report **AI visibility** alongside the **Mentioned** and **Cited** split when broken down.
- **The WhyIQ Page Scanner PREDICTS** on-page AI recommendation readiness heuristically across 8 signals and simulates 50 buyer personas to score Clarity and **`CTA Pull`** (`{value} / 100`, integer). Keep the Scanner prediction separate from Radar's measured weekly visibility.

## 2. Per-Engine Citation Signals Checked by WhyIQ
1. **Crawler & SSR Accessibility:** `GPTBot`, `OAI-SearchBot`, `PerplexityBot`, `ClaudeBot`, and `Google-Extended` must not be blocked in `robots.txt`; primary pricing, comparisons, and answers must render in initial server HTML (not solely behind client-side hydration).
2. **Answer-First Passage Structure:** Clear 40-to-80-word direct answers directly beneath explicit H2/H3 buyer questions, backed by structured comparison tables and named product categories.
3. **Structured Entity Graph:** Valid `SoftwareApplication`, `Organization`, `Product`, and `FAQPage` JSON-LD using `sameAs` links to authoritative third-party profiles plus `llms.txt`.
4. **Off-Site Third-Party Consensus:** Helpful presence in authentic Reddit threads, Hacker News discussions, G2, Trustpilot, Capterra, and buyer comparisons (handled via the off-site co-pilot on `https://www.whyiq.ai/radar/app/fixes`, never automated from the IDE).
