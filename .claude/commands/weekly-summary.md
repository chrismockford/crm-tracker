Generate my weekly Sales Automation team summary and post it to #sales-automation-weekly-input.

## What this does
Searches your Asana task completions and Slack messages from the last 7 days, generates a pre-filled weekly summary in the team template, lets you review it, then posts it to the channel.

---

## Instructions

**STEP 1 — Who is running this?**

Ask: "Hi! Which team member are you? (Cara / Claire / Chris)"

Use the corresponding IDs:
- **Chris Mockford**: Slack `U07UQSRLHA4`, Asana GID `1208704347237862`
- **Cara Ng**: Slack `U058T88F6MU`, Asana GID `1204718627911793`
- **Claire Lee**: Slack `U087QGVMUN5`, Asana GID `1209086855361095`

---

**STEP 2 — Pull Asana data (last 7 days)**

Query CRM project (GID: `1204665224125904`), workspace (GID: `149498577369773`).

For this person, find:
- Tasks **completed** in the last 7 days
- Tasks **in progress** modified in the last 7 days

Skip: tasks named "MEETING ACTION", "Daily Relevance AI check", or any task under 5 words with no description. Focus on BIG ROCK tasks, sequence builds, workforce launches, and initiative work.

---

**STEP 3 — Pull Slack data (last 7 days)**

Search these channels using `from:<@SLACK_ID>` filter (replace with their Slack ID):
- `#employment-hero-qualified` (C09BTHC9XMM)
- `#anz-ai-sdr-co-pilot` (C09ETFZH0GL)
- `#sdr-leaders-gtm-alliance` (C080L16MV46)
- `#crm-crew-leaders` (C0A2Z6H0B33)

Capture **granular specifics**: named people, exact actions taken, dates, external parties involved, stated next steps. Examples of the level of detail needed:
- "Mocks reached out to Greg Beazley for an update on UTM standardisation progress"
- "Cara triaged a live Salesforce verification issue for Rohit in the Qualified vendor channel"
- "Claire identified Upsell triggers still referencing Paris Holloway and updated BAD + MQL triggers to Charlene"

These specifics feed directly into the running commentary on initiative cards — the more precise, the better.

---

**STEP 4 — Generate the draft summary**

Fill in the template using ONLY what you found in Steps 2 and 3. Do not invent, assume, or embellish. If a section has nothing to report, write "None this week."

Use today's date for [Date].

```
📊 CRM Weekly Input — [Name] — [Date]

✅ SHIPPED THIS WEEK
• [Specific completed items — Asana BIG ROCKs + meaningful Slack announcements]
• [If nothing: "Nothing major shipped — ongoing work only"]

🔵 KEY UPDATES
• [Initiative name]: [one-line status from Asana notes or Slack]
• [Repeat for each active initiative with movement]

⚠️ BLOCKERS / RISKS
• [Any blockers or risks mentioned in Slack or Asana — be specific]
• [Or: "None"]

📊 METRICS / RESULTS
• [Any numbers: reply rates, conversion, task counts, sequence performance]
• [Or: "No new metrics this week"]

📋 NEXT WEEK FOCUS
• [Asana tasks due in next 7 days + any stated priorities from Slack]
• [Top 3 things you plan to work on]

🗂️ CARD UPDATES (for tracker sweep)
[For each initiative card that had movement this week, include an entry in this format:]
CARD: [card-id] | [Short date e.g. "12 Jun"] | [One specific sentence: who did what, any named people, outcome or next step]

Example entries:
CARD: qualified-optimisation | 12 Jun | Mocks reached out to Greg Beazley for a status update on partner routing delivery from Usman — no response yet, escalation planned for next week.
CARD: utm-standardisation | 12 Jun | Cara completed static sequence UTM tagging — all 500 sequences done, confirmed to Greg Beazley.
CARD: lost-revive | 12 Jun | Claire reported EOFY campaign results to Haroon and Clare B — Tuesday batch sent, total engagement report pending.

⚡ NEEDS MY RESPONSE (for tracker sweep)
[List any cards where progress has stalled because our team needs to act — a response is pending, a decision is ours to make, or the next step sits with us. These will be flagged in the tracker's "Needs Response" filter.]
NEEDS: [card-id] | [One sentence — what specifically is waiting on us and why it's blocking progress]
CLEAR: [card-id] | [One sentence — confirm the ball is no longer in our court and why]

Example entries:
NEEDS: outreach-mcp-business-case | Mocks needs to write and submit business case to infosec — no action taken yet, blocking connector approval.
NEEDS: long-term-nurture | Cara needs to confirm UTM additions and sequence variant count before Claire can build Outreach sequences.
CLEAR: utm-standardisation | Cara completed all tagging and Greg Beazley confirmed live — no further action required from us.

📣 CHASING (for tracker sweep)
[List any cards where the ball is technically in an external party's court but we need to actively push them — not passive waiting, but assertive chasing. Distinct from PENDING/WAITING ON (which is passive) — this section is for cases where you know it's stalled and you need to go after it.]
CHASE: [card-id] | [Who you need to chase] | [What you're waiting on and why it needs active follow-up, not passive waiting]
CLEAR-CHASE: [card-id] | [Confirm they've responded or delivered — no longer needs chasing]

Example entries:
CHASE: qualified-optimisation | Usman (Qualified vendor) | Partner routing branching logic overdue since 30 Apr — needs direct escalation, not another nudge.
CHASE: ae-outreach-expansion | Doc | Specific AE pain points needed before platform recommendation — hasn't responded to initial ask.
CLEAR-CHASE: utm-standardisation | Greg Beazley confirmed touchpoints live in Salesforce — no further follow-up needed.
```

The CARD UPDATES section populates the "Running Commentary" log on each initiative card.

The NEEDS MY RESPONSE section controls the ⚡ Needs Response filter in the tracker's Work Overview:
- `NEEDS: [card-id]` sets `needs_response: true` on that card — it will appear when the filter is active
- `CLEAR: [card-id]` removes the flag — it will no longer appear in the Needs Response filter
- Any card NOT mentioned keeps its current `needs_response` state unchanged

The CHASING section controls the 📣 Chasing filter in the tracker's Work Overview:
- `CHASE: [card-id]` sets `needs_chasing: true` on that card — it will appear when the Chasing filter is active
- `CLEAR-CHASE: [card-id]` removes the flag — card drops out of the Chasing filter
- **The key distinction**: Needs Response = next action is ours. Chasing = next action is theirs, but we must actively push, not wait.

---

**STEP 5 — Review and post**

Show the draft to the user and say:

*"Here's your draft based on your Asana and Slack activity this week. Please review and edit anything that looks wrong or incomplete — especially the NEXT WEEK section which is hard to infer automatically, and the CARD UPDATES section which needs to capture the specific granular detail (named people, explicit actions, stated next steps).*

*When you're happy with it, I can post it directly to #sales-automation-weekly-input, or you can copy and post it yourself. What would you like to do?"*

If they confirm posting: use `slack_send_message` to post to channel `C0B6GBDR9C7` (#sales-automation-weekly-input).

**Important:** Only post once confirmed by the user. Never auto-post without review.

---

## Saturday sweep — building the tracker draft

This phase reads all team posts, deduplicates, and stages changes for Chris to review on Monday. **It does NOT write to `initiative-tracker-2026.html` directly.** Changes are written to a draft file first.

### Step 1 — Read all posts

Read all posts from `#sales-automation-weekly-input` (channel ID: `C0B6GBDR9C7`) for the current week — anything posted since Monday 00:00 AWST.

### Step 2 — Deduplication pass

The same piece of work often appears across multiple team members' posts. Before building the draft, resolve duplicates:

1. Group all CARD UPDATE entries by `card-id` across all posts
2. For each card that appears in more than one post:
   - **Same action, different reporters**: Keep one entry. Identify who performed the action — look for first-person voice ("I completed", "I reached out") or a named subject in the entry text ("Cara completed", "Mocks chased"). Credit the doer.
   - **Different actions on the same card**: Merge into one log entry, e.g. "Cara completed UTM tagging; Mocks chased Greg Beazley for confirmation."
   - **Ownership genuinely unclear** (both people claim the same action, or no clear signal): Keep the most specific entry, mark as ⚠️ UNCLEAR with your best guess and the reason
3. For NEEDS/CLEAR and CHASE/CLEAR-CHASE: if conflicting instructions appear across posts, use the most recent post's signal

### Step 3 — Classify each update

For each deduplicated item, decide which tracker sections it should populate in addition to the card log (which always gets an entry):

- **Last Week Wins** (`WEEKLY_WINS`): items that completed, shipped, or were confirmed — keywords: "completed", "launched", "live", "done", "shipped", "confirmed", "delivered", "finished"
- **Key Updates** (`KEY_UPDATES`, leadership-visible): significant progress on active initiatives — meaningful movement, cleared blockers, stakeholder decisions. Not every update qualifies — only those with strategic relevance.
- **Upcoming Priorities** (`UPCOMING_PRIORITIES`): things starting or being planned next — "next week", "planning to", "scoping", "starting", "will begin"
- **Card log only**: routine progress notes, minor updates, operational detail

### Step 4 — Write tracker-update-draft.md

Write the following file to the root of the repo. Do not touch `initiative-tracker-2026.html`.

Each item should contain exactly the fields shown — nothing more, nothing less:

```
# Tracker Update Draft — Week of [Monday date of this week, e.g. "23 Jun 2026"]
Generated: [Today's date] | Source: #sales-automation-weekly-input
Total items: [N] | Status: PENDING REVIEW

---

## Item 1 of [N]

**Initiative**: [Full initiative name]
**Card ID**: `[card-id]`
**Owner**: [Name] — OR — ⚠️ UNCLEAR — mentioned by [X] and [Y]; best guess: [Z] because [one-line reason]
**Confidence**: ✅ High — OR — ⚠️ Low — ownership uncertain
**Update text**: "[Exact sentence that will be written to the card log]"
**Tracker writes**:
- Card log entry
- Last Week Wins [include only if applicable]
- Key Updates (leadership) [include only if applicable]
- Upcoming Priorities [include only if applicable]
- Flag: NEEDS needs_response [include only if applicable]
- Flag: CLEAR needs_response [include only if applicable]
- Flag: CHASE needs_chasing [include only if applicable]
- Flag: CLEAR-CHASE needs_chasing [include only if applicable]

**Decision**: PENDING

---

[Repeat for each item]
```

### Step 5 — Notify Chris

Send a Slack direct message to Chris Mockford (user ID: `U07UQSRLHA4`):

> 📋 Tracker draft is ready — [N] items staged for review. Open Claude Code and run `/apply-tracker-draft` to review and publish.

Then stop. Do not write any further changes to `initiative-tracker-2026.html`.

### Card ID reference

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

---

## Notes for the team

- This skill needs Slack and Asana MCPs connected in your Claude environment
- Run it any time before Friday 4pm AWST
- The Saturday automated agent reads your post as its primary source — the more specific your CARD UPDATES section, the richer the commentary in the tracker
- The CARD UPDATES section is what populates the "Running Commentary" log visible when leadership expand a card — treat it as the narrative record of the work
- If something in the draft is wrong, edit it before posting — accuracy matters more than speed
