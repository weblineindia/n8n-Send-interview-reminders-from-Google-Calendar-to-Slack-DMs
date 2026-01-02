# Send Interview Reminders (10 Minutes) from Google Calendar to Slack DMs

### 📅 Automated Recruitment Reminders (n8n | Google Calendar | Slack)

This workflow ensures that interviewers never miss a candidate meeting. It monitors a specific Google Calendar and sends a direct Slack message to the interviewer exactly 10 minutes before the start time, including the candidate’s name, role, meeting link, and any preparation notes.

---

## ⚡ Quick Implementation Steps

- Import the workflow JSON into your n8n instance.
- Configure your **Google Calendar** and **Slack** credentials.
- Open the **Set: Config** node and update the variables (Calendar Name, Domain, etc.).
- Activate the workflow to start polling for upcoming interviews.

---

## 🎯 Who's It For

- **Interviewers** who prefer a timely Slack nudge over traditional calendar notifications.
- **Recruiting Coordinators** wanting to reduce "no-show" rates from internal teams.
- **Hiring Teams** that store candidate CVs and notes directly in the calendar event description.

---

## 🛠 Requirements

| Tool                | Purpose                                                             |
| :------------------ | :------------------------------------------------------------------ |
| **n8n Instance**    | To run and schedule the automation                                  |
| **Google Calendar** | The source of truth for interview schedules                         |
| **Slack App**       | To send DMs (requires `users:read.email`, `chat:write`, `im:write`) |
| **Company Email**   | Used to map Calendar attendees to Slack users                       |

---

## 🧠 How It Works

1. **Cron Trigger:** Runs every minute to check for near-term events.
2. **Google Calendar Node:** Fetches events from the specified "Interviews" calendar.
3. **Filter Logic:** Identifies events starting in exactly 10 minutes (configurable).
4. **User Mapping:** Matches the interviewer's email address to their Slack ID.
5. **Slack DM:** Sends a formatted message with the meeting link and description details.

---

## 🔧 How To Set Up – Step-by-Step

1. **Import Workflow:** Upload the `.json` file into your n8n workspace.
2. **Set Credentials:**
   - **Google Calendar:** Connect via OAuth2.
   - **Slack:** Create a Slack App and connect via OAuth2.
3. **Configure Settings:**
   - Open the **Set: Config** node.
   - `CALENDAR_NAME`: The exact name of your interview calendar (e.g., _Interviews_).
   - `COMPANY_DOMAIN`: Your email domain (e.g., _weblineindia.com_).
   - `LEAD_MINUTES`: Default is 10.
   - `FALLBACK_CHANNEL`: Where to post if a Slack DM fails (e.g., _#recruiting-alerts_).
4. **Calendar Format:**
   - Ensure the interviewer is an attendee of the event.
   - Add `CV: [URL]` and `Notes: [URL]` in the event description for them to be parsed.
5. **Activate:** Toggle the workflow to **Active**.

---

## ✨ How To Customize

- **Change Lead Time:** Adjust `LEAD_MINUTES` in the config to 5 or 15 minutes.
- **Business Hours:** Add a filter to only send reminders during 9 AM - 6 PM.
- **Different Channels:** Send the alert to a public "Hiring" channel instead of a DM.
- **Preparation Buffers:** Add a "Check-in" message 30 minutes prior for technical setup.

---

## ➕ Add-ons (Advanced)

- **Log to Sheets:** Record every reminder sent in a Google Sheet for audit purposes.
- **Feedback Link:** Automatically send a Slack message _after_ the interview with a link to the feedback form.
- **Holiday Checker:** Integrate a "Holiday Calendar" to pause reminders on non-working days.

---

## 📈 Use Case Examples

- **High-Volume Hiring:** An agency managing 20+ daily interviews keeps interviewers on track.
- **Remote Teams:** Ensures distributed team members are alerted regardless of their time zone.
- **Hiring Sprints:** Keeps teams focused during intense "Interview Day" events.

---

## 🧯 Troubleshooting Guide

| Issue                  | Possible Cause       | Solution                                                                         |
| :--------------------- | :------------------- | :------------------------------------------------------------------------------- |
| **No Slack DM sent**   | Email mismatch       | Ensure the Calendar attendee email matches the Slack email exactly.              |
| **Bot Error**          | Missing Slack scopes | Add `users:read.email` and `chat:write` to your Slack App.                       |
| **Duplicate Alerts**   | Polling overlap      | Ensure the "Check" logic avoids events already processed in the previous minute. |
| **Calendar not found** | Incorrect Name       | Verify the `CALENDAR_NAME` in the Config node matches your Google account.       |

---

## 📞 Need Assistance?

Need help integrating this into your specific HR stack or customizing the parsing logic?

👉 **Contact WeblineIndia** — We specialize in workflow automation for recruitment and enterprise teams.
