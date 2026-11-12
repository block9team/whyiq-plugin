# WhyIQ Plugin for Google Antigravity

Connect **WhyIQ AI Radar** and the **WhyIQ 50-Visitor CRO & On-Page AI Readiness Scanner** directly to Google Antigravity, Claude Code, Cursor, and Gemini CLI.

## What Included Tools & Skills Do

- **Weekly AI Visibility Measurement (AI Radar):** Inspect your measured **AI visibility** (Mentioned or Cited) across ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini, and Claude. See which competitors win on your buyer questions, which third-party Reddit or review URLs get cited, and which pages need answer-first blocks or schema.
- **50-Visitor CRO Simulation & CTA Pull:** Query your 50-visitor behavioral simulation across 5 lenses (`synthesis`, `emotional_and_trust`, `scroll_and_visibility`, `archetype_voices`, `technical_audits`) to see why buyers hesitate, which proof elements they dismiss, and your **CTA Pull** (`{value} / 100`).
- **Guarded 1-Click Fix Autopilot:** Prepare, stage, verify, and roll back CRO and AEO fixes under your 4-Mode Switchboard (`off`, `flag`, `stage`, `auto`), protected by the `[fill in: ...]` Honesty Gate and SHA-256 Undo Ledger.

---

## Installation

### Install via Antigravity CLI (`agy`)
```bash
agy plugin install https://github.com/block9team/whyiq-plugin
```

### Or Install Locally
```bash
git clone https://github.com/block9team/whyiq-plugin.git
agy plugin install ./whyiq-plugin
```

---

## Bundled MCP Tools (`https://www.whyiq.ai/api/mcp`)

| Tool | Purpose |
| :--- | :--- |
| `whyiq_get_site_overview` | Executive snapshot: WhyIQ Score, CTA Pull (`{value} / 100`), predicted on-page AI readiness, measured weekly AI Radar visibility, and open fix counts. |
| `whyiq_inspect_radar_intelligence` | Drill into AI Radar across 5 views: `losses_and_moves`, `engine_breakdown`, `page_comparison`, `foundations`, and `offsite_footprint`. |
| `whyiq_inspect_visitor_simulation` | Drill into the 50-visitor CRO simulation across 5 lenses: `synthesis`, `emotional_and_trust`, `scroll_and_visibility`, `archetype_voices`, and `technical_audits`. |
| `whyiq_list_autopilot_fixes` | List ranked CRO and AI Radar fixes filtered by product, Switchboard group, or mode (`off`, `flag`, `stage`, `auto`). |
| `whyiq_prepare_fix_bundle` | Enforce the `[fill in: ...]` Honesty Gate and capture a SHA-256 `before_snapshot` before editing files. |
| `whyiq_verify_and_record_fix` | Verify the applied fix, record the `after_snapshot` in the Applied Fixes Ledger, and mark the AI Radar move Shipped. |
| `whyiq_rollback_fix` | Restore the exact pre-change file snapshot from the Undo Ledger in one click. |
| `whyiq_configure_switchboard` | Apply a Switchboard preset (`recommended_safe`, `review_everything`, `hands_free_auto`, `read_only`) or per-element mode overrides. |

---

## Starter Prompts

- *"Run a WhyIQ overview on my site and list the top-ranked CRO and AI Radar fixes"*
- *"Inspect my 50-visitor simulation to see why visitors hesitate on our hero and pricing"*
- *"Show which competitors beat us on buyer questions in AI Radar this week and stage a fix"*

Learn more at [whyiq.ai/mcp](https://www.whyiq.ai/mcp).
