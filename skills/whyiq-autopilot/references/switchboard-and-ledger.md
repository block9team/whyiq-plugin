# 4-Mode Switchboard, Honesty Gate & Undo Ledger Reference

## 1. The 4 Permission Modes
Every WhyIQ Autopilot action maps to one of 18 sub-elements controlled by the user's 4-Mode Switchboard (`off`, `flag`, `stage`, `auto`):

- **`off`**: Do not surface or apply items in this sub-element.
- **`flag`**: Read-only reporting. Diagnose and explain to the user without modifying code.
- **`stage`**: Build the proposed diff, present it cleanly (or via `staged-review.html`), and wait for explicit approval.
- **`auto`**: Direct execution permitted once `whyiq_prepare_fix_bundle` passes with zero unresolved `[fill in: ...]` slots.

Two hard limits overrides cannot bypass:
1. Off-site work (`offsite_community`, `offsite_authority`, `offsite_listings`) never runs on `auto` and never commits to Git. Review and send from `https://www.whyiq.ai/radar/app/fixes`.
2. Any fix containing an unresolved `[fill in: ...]` slot automatically drops to human review until the user supplies the real fact.

## 2. All 18 Switchboard Sub-Elements Across 4 Product Groups

1. **AI Radar: Win AI recommendations on buyer questions (`radar_answers`)**
   - `radar_answer`, `radar_extend`, `radar_new_page`, `radar_refresh`, `radar_google_serp`
2. **On-page AI recommendation readiness (`foundations`)**
   - `found_crawler`, `found_redirect`, `found_rendering`, `found_schema`, `found_pricing_stats`, `found_headings`
3. **Lift conversion and CTA Pull (`cro_ux`)**
   - `cro_hero_clarity`, `cro_cta_pull`, `cro_trust_proof`, `cro_a11y_lcp`
4. **Off-site recommendation co-pilot (`offsite`)**
   - `offsite_community`, `offsite_authority`, `offsite_listings`

## 3. Honesty Gate + `keepAnswers` + SHA-256 Rollback Protocol
- Never guess customer logos, revenue metrics, SLA uptime, SOC 2 badges, or review quotes.
- Before saving any edit to a page tracked by AI Radar, verify every phrase in `keepAnswers` stays intact so shipping a fix does not regress existing AI citations.
- Every prepared fix captures a cryptographic SHA-256 `before_snapshot`. Always record `after_snapshot` via `whyiq_verify_and_record_fix` immediately after applying so the dashboard stays synchronized (`To do -> Waiting (Next Weekly Scan)` for Radar moves, `To do -> Done` for Foundations/CRO) and 1-click rollback via `whyiq_rollback_fix` remains active.
