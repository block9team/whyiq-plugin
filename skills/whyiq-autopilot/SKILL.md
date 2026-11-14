---
name: whyiq-autopilot
description: Run 50-visitor landing page CRO audits, inspect CTA Pull and on-page AI citability readiness, configure the 4-Mode Switchboard, and execute or roll back guarded 1-click fixes using the WhyIQ MCP server. Use whenever the user asks to audit a page's conversion rate, inspect simulated visitor objections, list or apply WhyIQ Autopilot fixes, or roll back a change.
---

# WhyIQ CRO Simulation & 1-Click Fix Autopilot

Use this skill to diagnose landing page conversion drops, render visual executive scorecards and interactive review workbenches, and execute guarded code or CMS fixes through the WhyIQ MCP server (`whyiq_whyiq` in Antigravity plugins, or `whyiq` in manual IDE configs).

Never expose internal skill names in user-facing responses.

## Surface 1: Inline Chat Card (`<agent-embed>`)

When starting an overview or site audit (`whyiq_get_site_overview`), always render one compact inline card directly in chat by populating the matching HTML template, writing it to `<Artifact Directory Path>` with `UserFacing: true`, and emitting `<agent-embed src="file:///<Artifact Directory Path>/<filename>.html"></agent-embed>`:

1. **No completed scan (`no_completed_scan`) or exhausted Free Tier fix credit (`tier === "free_connected"` and `freeFixCreditsRemaining === 0`):**
   - Use [assets/onboarding-card.html](assets/onboarding-card.html) saved as `whyiq-onboarding-card.html`.
   - Never fabricate scores or simulated quotes when no scan exists; link the user straight to `https://www.whyiq.ai/analyse?url=<encoded_url>&autopilot=1` (or `https://www.whyiq.ai/pricing?from=plugin`).
2. **Active scan / Radar workspace:**
   - Use [assets/overview-card.html](assets/overview-card.html) saved as `whyiq-overview-card.html`.
   - Separate **Measured Weekly AI Visibility** (`AI visibility %`, `Cited %`, `Mentioned %` across the 5 engines) from **50-Visitor CRO Simulation** (`Clarity`, **`CTA Pull {value} / 100`** integer, never `%`, and `Predicted AI Readiness`).

## Surface 2: Full-Height Side-Pane Interactive Workbenches

Whenever the user asks to visually review, select, fill facts, verify, or roll back fixes:
1. Read `whyiq://domain/<domain>/staged-review.html` via `read_resource` (`whyiq-staged-review.html` in `<Artifact Directory Path>`, `UserFacing: true`) so the user can toggle **Fix** or **Leave**, fill `[fill in: ...]` **Honesty Gate** inputs, and review Off-Site Co-Pilot handoff links (`https://www.whyiq.ai/radar/app/fixes`).
2. After applying fixes via `whyiq_verify_and_record_fix`, read `whyiq://domain/<domain>/autopilot-report.html` (`whyiq-autopilot-report.html` in `<Artifact Directory Path>`, `UserFacing: true`) to display before/after diffs, protected `keepAnswers`, dashboard transitions (`Waiting` vs. `Done`), and 1-click rollback actions.

## Progressive-Disclosure Tool Workflow

Always work from lightweight overview to targeted drill-down before editing files:

### Step 1: Executive Site Overview (`whyiq_get_site_overview`)
Call `whyiq_get_site_overview` with the user's `domain` (or `url`):
- Inspects composite metrics, **`CTA Pull`** (`{value} / 100`), predicted on-page AI recommendation readiness, measured weekly AI visibility, active 4-Mode Switchboard counts, `tier`, and `freeFixCreditsRemaining`.

### Step 2: 50-Visitor Simulation Drill-Down (`whyiq_inspect_visitor_simulation`)
Call `whyiq_inspect_visitor_simulation` with `url` and the matching `lens`:
- `synthesis`: Executive behavioral synthesis, top friction points, and highest-leverage conversion fixes.
- `emotional_and_trust`: V2 emotional affect breakdown and which trust signals visitors believed vs. dismissed.
- `scroll_and_visibility`: Scroll-depth reach and whether key proof or CTAs sit below the fold where visitors drop off.
- `archetype_voices`: Verbatim objections and quotes from the 50 simulated buyer personas (filterable via `filter_archetype` or `filter_exit_reason`).
- `technical_audits`: 8-signal predicted AI Recommendation readiness, 7-dimension WCAG AA accessibility, and Search Rank checks.

### Step 3: List Ranked Fixes (`whyiq_list_autopilot_fixes`)
Call `whyiq_list_autopilot_fixes` with:
- `domain`: Target domain.
- `product_filter`: `"scanner"`, `"radar"`, or `"all"`.
- `group_filter`: `"cro_ux"`, `"foundations"`, `"radar_answers"`, `"offsite"`, or `"all"`.
- `mode_filter`: `"auto"`, `"stage"`, `"flag"`, or `"all"`.

Each item returns `id`, `effectiveMode`, `unresolvedPlaceholders` (`[fill in: ...]` slots), and `keepAnswers` (phrases on the page that already earn AI citations and must not be deleted). Full governance details sit in [references/switchboard-and-ledger.md](references/switchboard-and-ledger.md).

### Step 4: Guarded Preparation (`whyiq_prepare_fix_bundle`)
Before touching any file in the workspace:
1. Check `unresolvedPlaceholders`. If non-empty, pause and ask the user for those exact customer metrics, case studies, or SLA facts first. Never guess or fabricate numbers.
2. Check if the item belongs to `offsite` (Reddit, Hacker News, G2, Trustpilot, directories): never automate off-site posts; direct the user to `https://www.whyiq.ai/radar/app/fixes`.
3. Call `whyiq_prepare_fix_bundle` with `domain`, `fix_ids`, `target_environment` (for example `"local_workspace"` or `"github_pr"`), and `resolved_placeholders`.
4. Note the returned `ledgerId` and preserve every phrase in `keepAnswers`.

### Step 5: Apply, Verify & Record (`whyiq_verify_and_record_fix`)
1. If `effectiveMode` is `"stage"`, present the exact diff to the user and wait for explicit approval. If `"auto"` (and zero placeholders remain), apply cleanly.
2. Call `whyiq_verify_and_record_fix` with `ledger_id`, `domain`, `status: "applied"` (or `"skipped"`), and `after_snapshot` so WhyIQ confirms zero remaining `[fill in: ...]` tokens and updates the Applied Fixes Ledger.

### Step 6: Instant Undo (`whyiq_rollback_fix`)
If the user asks to revert a change or a build check fails:
- Call `whyiq_rollback_fix` with `ledger_id` and `reason`, then restore the returned `before_snapshot` to the file.
