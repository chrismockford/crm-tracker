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

Look for: things they shipped or announced, problems they solved, status updates they posted, metrics or results they shared.

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
```

---

**STEP 5 — Review and post**

Show the draft to the user and say:

*"Here's your draft based on your Asana and Slack activity this week. Please review and edit anything that looks wrong or incomplete — especially the NEXT WEEK section which is hard to infer automatically.*

*When you're happy with it, I can post it directly to #sales-automation-weekly-input, or you can copy and post it yourself. What would you like to do?"*

If they confirm posting: use `slack_send_message` to post to channel `C0B6GBDR9C7` (#sales-automation-weekly-input).

**Important:** Only post once confirmed by the user. Never auto-post without review.

---

## Notes for the team

- This skill needs Slack and Asana MCPs connected in your Claude environment
- Run it any time before Friday 4pm AWST
- The Saturday automated agent reads your post as its primary source — the more specific your update, the better the tracker output will be
- If something in the draft is wrong, edit it before posting — accuracy matters more than speed
