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
```

The CARD UPDATES section populates the "Running Commentary" log on each initiative card.

The NEEDS MY RESPONSE section controls the ⚡ Needs Response filter in the tracker's Work Overview:
- `NEEDS: [card-id]` sets `needs_response: true` on that card — it will appear when the filter is active
- `CLEAR: [card-id]` removes the flag — it will no longer appear in the Needs Response filter
- Any card NOT mentioned keeps its current `needs_response` state unchanged

---

**STEP 5 — Review and post**

Show the draft to the user and say:

*"Here's your draft based on your Asana and Slack activity this week. Please review and edit anything that looks wrong or incomplete — especially the NEXT WEEK section which is hard to infer automatically, and the CARD UPDATES section which needs to capture the specific granular detail (named people, explicit actions, stated next steps).*

*When you're happy with it, I can post it directly to #sales-automation-weekly-input, or you can copy and post it yourself. What would you like to do?"*

If they confirm posting: use `slack_send_message` to post to channel `C0B6GBDR9C7` (#sales-automation-weekly-input).

**Important:** Only post once confirmed by the user. Never auto-post without review.

---

## Saturday sweep — updating the tracker

When updating `initiative-tracker-2026.html` from the weekly inputs, the sweep should:

1. **Read all posts** from #sales-automation-weekly-input for the current week
2. **Extract CARD UPDATES sections** from each post — these are the authoritative source for log entries
3. **For each card referenced** in a CARD UPDATES entry:
   - Add a new entry to the card's `log` array: `{"date": "[Short date]", "note": "[Specific sentence]"}`
   - Log entries **accumulate** — never overwrite prior log entries, only append new ones
   - The `log` array should remain in reverse chronological order (newest first)
4. **Also update** the card's `activity`, `next_steps`, `blockers`, `metrics`, and `progress` fields as usual
5. **Extract NEEDS MY RESPONSE sections** and update `needs_response` on affected cards:
   - `NEEDS: [card-id]` → set `"needs_response": true` on that card
   - `CLEAR: [card-id]` → remove `needs_response` field (or set to `false`) on that card
   - Cards not mentioned retain their current `needs_response` state
6. **For any win, highlight, or callout** that doesn't yet have a card — create a new `additional` type card and add the card to ALL_CARDS before referencing it
7. **Every entry** in KEY_UPDATES, HIGHLIGHTS, WEEKLY_WINS, and UPCOMING_PRIORITIES must have a `card_id` that maps to a real card in ALL_CARDS
   - WEEKLY_WINS and UPCOMING_PRIORITIES items must be `{"text": "...", "card_id": "..."}` objects, not plain strings

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
- `stakeholder-engagement` — Stakeholder & Leadership Engagement

---

## Notes for the team

- This skill needs Slack and Asana MCPs connected in your Claude environment
- Run it any time before Friday 4pm AWST
- The Saturday automated agent reads your post as its primary source — the more specific your CARD UPDATES section, the richer the commentary in the tracker
- The CARD UPDATES section is what populates the "Running Commentary" log visible when leadership expand a card — treat it as the narrative record of the work
- If something in the draft is wrong, edit it before posting — accuracy matters more than speed
