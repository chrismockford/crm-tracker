# Weekly Slack Summary — Setup Guide for Cara & Claire

## What this does

Every Friday at 3pm AWST, a scheduled Claude agent runs under **your own Slack account** and:

1. Scans your Slack messages and DMs from the past 7 days
2. Filters for **work-related content only** — anything personal is ignored
3. Packages your activity into the team's structured weekly template
4. Posts the summary to `#sales-automation-weekly-input`

This feeds directly into the Saturday automated sweep that updates the initiative tracker and Tuesday's OKR canvas update that goes to leadership.

**Your DMs are read only by you** — the agent runs under your own Slack credentials, not Chris's or anyone else's.

---

## What you need before starting

1. **A claude.ai account** — go to claude.ai and sign up or log in (your Employment Hero email is fine)
2. **Slack connected as an MCP** — instructions in Step 1 below
3. The whole setup takes about 10 minutes

---

## Setup steps

### Step 1 — Connect Slack to Claude

1. Go to **claude.ai/customize/connectors**
2. Find **Slack** and click **Connect**
3. When prompted, log in with your **Employment Hero Slack account**
4. Approve the permissions — Claude needs read access to your messages

That's it. Your Slack is now connected under your own credentials.

---

### Step 2 — Create the scheduled routine

1. Go to **claude.ai/code/routines**
2. Click **New routine**
3. Set the **schedule** to: every Friday at 3pm AWST

   > Friday 3pm AWST = Friday 5am UTC
   > Cron expression: `0 5 * * 5`

4. Set the **name**: `Weekly Slack Summary — [Your Name]`

5. In the **prompt field**, paste the script from Step 3 below (Cara uses the Cara version, Claire uses the Claire version)

6. Under **MCP connections**, add **Slack** (the one you connected in Step 1)

7. Save and enable the routine

---

### Step 3 — The skill script

**For Cara — paste this as your routine prompt:**

```
You are generating Cara Ng's weekly work summary for the Employment Hero Sales Automation team. Run every Friday at 3pm AWST.

YOUR SLACK USER ID: U058T88F6MU
TARGET CHANNEL: #sales-automation-weekly-input (ID: C0B6GBDR9C7)

STEP 1 — Search your Slack activity (last 7 days)
Search for messages FROM you (from:<@U058T88F6MU>) across:
- All channels you are a member of
- Your direct messages and group DMs

Collect everything you find. You will filter in Step 2.

STEP 2 — Filter for work content ONLY
Keep a message only if it relates to your work responsibilities at Employment Hero, specifically:
- Outreach sequences, Relevance AI workforces, AI SDR agents, HeroForce, Lost Revive
- Qualified chatbot, Salesforce, Marketo, Asana, CRM
- SDR teams, BAD/MQL/SAO, pipeline, leads, sequences, automation
- Any project, initiative, or tool you work on professionally

DISCARD any message that:
- Appears personal in nature (social plans, family, health, personal purchases, weekend activities)
- Is clearly unrelated to Sales Automation or Employment Hero work
- If you are uncertain whether a message is work-related, DISCARD IT

STEP 3 — Generate the weekly summary
Using only the work-related messages from Step 2, fill in this template. Be specific and factual — only include things you actually said or did. Do not invent or embellish. If a section has nothing to report, write "None this week."

---
📊 *CRM Weekly Input — Cara Ng — [today's date in DD Mon YYYY]*

✅ *SHIPPED THIS WEEK*
• [Specific things you completed or launched — sequences, workforces, fixes, builds]

🔵 *KEY UPDATES*
• [Initiative name]: [one-line current status]
• [Repeat for each area you're actively working on]

⚠️ *BLOCKERS / RISKS*
• [Any specific blockers, errors, or risks you mentioned — or "None"]

📊 *METRICS / RESULTS*
• [Any numbers you shared: reply rates, conversion rates, task counts, etc.]

📋 *NEXT WEEK FOCUS*
• [Top 2–3 things you plan to work on next week based on your conversations]
---

STEP 4 — Post to the channel
Use slack_send_message to post the completed summary to channel C0B6GBDR9C7.

Add this line at the bottom of the message:
_✅ Auto-generated from Cara's Slack activity — reviewed and confirmed._

STEP 5 — Confirm
Print: how many messages you scanned, how many were kept as work-related, and confirm the post was sent.
```

---

**For Claire — paste this as your routine prompt:**

```
You are generating Claire Lee's weekly work summary for the Employment Hero Sales Automation team. Run every Friday at 3pm AWST.

YOUR SLACK USER ID: U087QGVMUN5
TARGET CHANNEL: #sales-automation-weekly-input (ID: C0B6GBDR9C7)

STEP 1 — Search your Slack activity (last 7 days)
Search for messages FROM you (from:<@U087QGVMUN5>) across:
- All channels you are a member of
- Your direct messages and group DMs

Collect everything you find. You will filter in Step 2.

STEP 2 — Filter for work content ONLY
Keep a message only if it relates to your work responsibilities at Employment Hero, specifically:
- Outreach sequences, usage reporting, weekly metrics, trigger management
- Qualified chatbot (partner routing, SDR onboarding, gated content assets)
- Salesforce, Asana, Marketo, CRM, SDR teams
- Partnerships SDR routing, partner leads, sequence naming, content cataloguing
- Any project, initiative, or tool you work on professionally

DISCARD any message that:
- Appears personal in nature (social plans, family, health, personal purchases, weekend activities)
- Is clearly unrelated to Sales Automation or Employment Hero work
- If you are uncertain whether a message is work-related, DISCARD IT

STEP 3 — Generate the weekly summary
Using only the work-related messages from Step 2, fill in this template. Be specific and factual — only include things you actually said or did. Do not invent or embellish. If a section has nothing to report, write "None this week."

---
📊 *CRM Weekly Input — Claire Lee — [today's date in DD Mon YYYY]*

✅ *SHIPPED THIS WEEK*
• [Specific things you completed — sequences, routing updates, reports, fixes]

🔵 *KEY UPDATES*
• [Initiative name]: [one-line current status]
• [Repeat for each area you're actively working on]

⚠️ *BLOCKERS / RISKS*
• [Any specific blockers, errors, or risks you mentioned — or "None"]

📊 *METRICS / RESULTS*
• [Any numbers from your Outreach metrics report or other data you shared]

📋 *NEXT WEEK FOCUS*
• [Top 2–3 things you plan to work on next week based on your conversations]
---

STEP 4 — Post to the channel
Use slack_send_message to post the completed summary to channel C0B6GBDR9C7.

Add this line at the bottom of the message:
_✅ Auto-generated from Claire's Slack activity — reviewed and confirmed._

STEP 5 — Confirm
Print: how many messages you scanned, how many were kept as work-related, and confirm the post was sent.
```

---

## Testing it before Friday

Once you've set it up, you can run it immediately to test:
1. Go to **claude.ai/code/routines**
2. Find your routine
3. Click **Run now**

Check `#sales-automation-weekly-input` — your summary should appear within a few minutes.

---

## How the filter works (privacy)

The agent reads your Slack messages and DMs under your own credentials. The prompt explicitly instructs it to:
- Only keep messages that relate to your Employment Hero work responsibilities
- Discard anything that looks personal
- If uncertain, discard it

The agent never stores your messages — it processes them in the moment and generates the summary. Nothing is retained.

If you ever want to review what it's doing, run it manually and check the output before it posts. You can also add a review step by asking Chris to modify your routine to show you the draft first.

---

## Questions?

Reach out to Chris (Mocks) in Slack.
