---
name: whyiq-autopilot
description: Run 50-visitor landing page CRO audits, inspect CTA Pull and on-page AI citability readiness, configure the 4-Mode Switchboard, and execute or roll back guarded 1-click fixes using the WhyIQ MCP server. Use whenever the user asks to audit a page's conversion rate, inspect simulated visitor objections, list or apply WhyIQ Autopilot fixes, or roll back a change.
---

# WhyIQ CRO Simulation & 1-Click Fix Autopilot

Use this skill to diagnose landing page conversion drops and execute guarded code or CMS fixes through the `whyiq` MCP server.

## Progressive-Disclosure Tool Workflow

Always work from lightweight overview to targeted drill-down before editing files:

### Step 1: Executive Site Overview (`whyiq_get_site_overview`)
Start every session by calling `whyiq_get_site_overview` with the user's `domain` (or `url`):
- Reports the composite WhyIQ Score, **CTA Pull** (`{value} / 100`), predicted on-page AI recommendation readiness, measured weekly AI Radar visibility, active 4-Mode Switchboard counts, and open Autopilot fix queue counts.

### Step 2: 50-Visitor Simulation Drill-Down (`whyiq_inspect_visitor_simulation`)
When the user wants to know *why* visitors bounce or hesitate, call `whyiq_inspect_visitor_simulation` with `url` and the matching `lens`:
- `synthesis`: Executive behavioral synthesis, top friction points, and highest-leverage conversion fixes.
- `emotional_and_trust`: V2 emotional affect breakdown and which trust signals visitors believed vs. dismissed.
- `scroll_and_visibility`: Scroll-depth reach and whether key proof or CTAs sit below the fold where visitors drop off.
- `archetype_voices`: Verbatim objections and quotes from the 50 simulated buyer personas (filterable via `filter_archetype` or `filter_exit_reason`).
- `technical_audits`: 8-signal predicted AI Recommendation readiness, 7-dimension WCAG AA accessibility, and Search Rank checks.

### Step 3: List Ranked Fixes (`whyiq_list_autopilot_fixes`)
Call `whyiq_list_autopilot_fixes` with:
- `domain`: Target domain.
- `product_filter`: `"scanner"` (CRO & on-page readiness fixes), `"radar"` (AI Radar fixes), or `"all"`.
- `group_filter`: `"cro_ux"`, `"foundations"`, `"radar_answers"`, `"offsite"`, or `"all"`.
- `mode_filter`: `"auto"`, `"stage"`, `"flag"`, or `"all"`.

Each item returns its `id`, `effectiveMode`, `unresolvedPlaceholders` (`[fill in: ...]` slots), and `keepAnswers` (facts on the page that must be preserved when editing).

### Step 4: Guarded Preparation (`whyiq_prepare_fix_bundle`)
Before touching any file in the workspace:
1. Check if any selected fix has `unresolvedPlaceholders`. If so, ask the user to supply those real customer facts first. Never guess or fabricate numbers.
2. Call `whyiq_prepare_fix_bundle` with `domain`, `fix_ids`, `target_environment` (for example, `"cursor_local"` or `"github_pr"`), and `resolved_placeholders`.
3. Note the returned `ledgerId` and preserve every phrase listed in `keepAnswers`.

### Step 5: Apply, Verify & Record (`whyiq_verify_and_record_fix`)
1. If `effectiveMode` is `"stage"`, show the proposed diff to the user and wait for approval. If `"auto"` (and all placeholders are resolved), apply the change directly.
2. Call `whyiq_verify_and_record_fix` with `ledger_id`, `domain`, `status: "applied"` (or `"skipped"`), and `after_snapshot` so WhyIQ verifies zero remaining `[fill in: ...]` tokens and records the change in the Applied Fixes Ledger.

### Step 6: Instant Undo (`whyiq_rollback_fix`)
If the user asks to revert a change or a build check fails:
- Call `whyiq_rollback_fix` with `ledger_id` and `reason`, then restore the returned `before_snapshot` to the file.
