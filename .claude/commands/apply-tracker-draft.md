Review and apply the staged weekly tracker update. Run this on Monday morning after receiving the Saturday notification.

## What this does

Reads `tracker-update-draft.md`, presents every planned change in one compact review block, accepts corrections, applies approved changes to `initiative-tracker-2026.html`, and commits.

---

## STEP 1 — Read the draft

Read `tracker-update-draft.md` from the root of the repo.

If the file does not exist: say "No pending draft — nothing to review this week. If you expected one, the Saturday sweep may not have run yet." Then stop.

---

## STEP 2 — Present all items for review

Display ALL items in one compact block, exactly in this format:

```
📋 TRACKER DRAFT — Week of [date from draft] | [N] items

Reply "all good" to approve and publish everything.
To correct an item, call it out by number:
  "[n]: owner is [name]"        → fix who gets credit
  "[n]: move to card [card-id]" → change target card
  "[n]: skip"                   → exclude this item
  "[n]: update text — [text]"   → replace the log entry text
  "[n]: [anything else]"        → I'll interpret it

Multiple corrections in one reply are fine.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1 ✅  [card-id] | [Owner name]
     "[Update text — truncated to ~90 chars if longer]"
     → [Tracker destinations]

2 ⚠️  [card-id] | UNCLEAR: [who? — your one-line best guess]
     "[Update text]"
     → [Tracker destinations]

[continue for all items]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Formatting rules:
- ✅ = confident ownership | ⚠️ = ownership uncertain, needs Chris's call
- Tracker destinations shown inline as: `Card log · Last Week Wins · Key Updates · Upcoming · NEEDS · CLEAR · CHASE · CLEAR-CHASE` — only include what applies to that item
- Truncate update text at ~90 characters with "…" if longer — full text is in the draft file

---

## STEP 3 — Process corrections

Accept Chris's reply. Parse it for any combination of the correction formats above. Multiple corrections in one message are expected and fine.

After applying corrections, **summarise what will be applied before touching anything**:

> "Applying [N] of [total] items — [X] skipped. Item 3 updated to Cara as owner. Item 7 moved to card `lost-revive`. Ready to publish?"

Wait for confirmation ("yes", "go", "confirmed", "yep", "do it", etc.) before proceeding to Step 4.

---

## STEP 4 — Apply changes to initiative-tracker-2026.html

Read `initiative-tracker-2026.html`. Apply all approved items:

### Card log entries
For each approved item, prepend a new entry to the card's `log` array (newest first):
```json
{"date": "[Short date, e.g. '21 Jun']", "note": "[Update text]"}
```
Log entries **accumulate** — never overwrite prior entries, only prepend.

### Update card fields
For each card that received a log entry, also update these fields as appropriate based on the update content:
- `activity` — current status summary
- `next_steps` — what's coming next
- `blockers` — any blockers mentioned
- `metrics` — any numbers or results
- `progress` — percentage complete (0–100)
- `last_updated` — today's date (e.g. "23 Jun 2026")

### WEEKLY_WINS entries
For each item marked "Last Week Wins", add to the `WEEKLY_WINS` object:
```json
{"text": "[Update text]", "card_id": "[card-id]"}
```
Must be `{"text": "...", "card_id": "..."}` objects — not plain strings.

### KEY_UPDATES entries
For each item marked "Key Updates (leadership)", add to the appropriate section in `KEY_UPDATES`:
```json
{"text": "[Update text]", "card_id": "[card-id]"}
```

### UPCOMING_PRIORITIES entries
For each item marked "Upcoming Priorities", add to `UPCOMING_PRIORITIES`:
```json
{"text": "[Update text]", "card_id": "[card-id]"}
```

### Flag updates
- `NEEDS needs_response` → set `"needs_response": true` on that card
- `CLEAR needs_response` → remove `needs_response` (or set `false`) on that card
- `CHASE needs_chasing` → set `"needs_chasing": true` on that card
- `CLEAR-CHASE needs_chasing` → remove `needs_chasing` (or set `false`) on that card
- Cards not mentioned in any flag instruction retain their current state unchanged

### New cards
If an approved item references a card-id that doesn't exist in `ALL_CARDS`, create a new card with `"type": "additional"` and add it to `ALL_CARDS` before writing the log entry.

### Integrity check
Every entry added to `KEY_UPDATES`, `WEEKLY_WINS`, and `UPCOMING_PRIORITIES` must reference a `card_id` that exists in `ALL_CARDS`. Verify this before committing.

---

## STEP 5 — Commit and clean up

1. Commit `initiative-tracker-2026.html` with message:
   `Weekly tracker sweep — week of [date] | [N] cards updated`

2. Delete `tracker-update-draft.md` from the repo root

3. Commit the deletion with message:
   `Remove tracker draft — applied [date]`

---

## Card ID reference

Key active cards (partial list — see ALL_CARDS in the HTML for full list):
- `qualified-optimisation` — Qualified Experience Optimisation
- `heroforce-ai` — HeroForce AI Workforce
- `lost-revive` — Lost Revive AI Workforce
- `evals-self-healing` — Built-in Evals & Self-Healing
- `ae-outreach-expansion` — AE Outreach Expansion — 38 Seats
- `utm-standardisation` — UTM Standardisation for Marketo Measure
- `outreach-reporting-2` — Outreach Performance Reporting 2.0
- `relevance-sequence-framework` — Relevance AI Sequence Framework
- `relevance-reporting-framework` — Relevance AI Reporting Framework
- `ai-adoption-uk` — Increase AI Adoption — UK
- `ai-adoption-ca` — Increase AI Adoption — Canada
- `ai-sdr-webinars` — AI SDR — Webinars & Content Syndication
- `ai-research-brief` — AI Research Brief for Calls
- `long-term-nurture` — Long Term Nurture Programme
- `insights-reporting` — Insights-Driven Reporting
- `qualified-reporting` — Qualified Chatbot Reporting & Optimisation
- `optimised-relevance-workflow` — Optimised Relevance AI Workflow
- `outreach-system-maintenance` — Outreach Sequence Maintenance & Ops
- `anz-partnerships-ai-expansion` — ANZ Partnerships — Relevance AI Expansion
- `outreach-mcp-business-case` — Outreach MCP — Claude Connection Approval
- `concurrent-processing` — Concurrent Processing — Relevance AI Early Trigger
- `stakeholder-engagement` — Stakeholder & Leadership Engagement
- `outreach-overdue-task-agent` — Outreach Overdue Task Reporting Agent
