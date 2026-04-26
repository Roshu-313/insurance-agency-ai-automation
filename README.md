# 🏥 Insurance Agency AI Lead Follow-Up Automation

A fully automated lead follow-up system for insurance agencies built with n8n, Groq AI, Twilio, Gmail, Google Sheets and Slack.

## 🎯 What This Does

Insurance agencies lose 20-30% of potential clients every year simply because no one followed up. This automation fixes that completely — zero manual follow-up, agents only make the call that converts.

## ⚡ How It Works

1. **Trigger** — A new lead is added to Google Sheets
2. **AI SMS** — Groq AI (Llama 3.3 70B) writes a personalized SMS for that specific lead and insurance type (Medicare / ACA / Auto)
3. **SMS Sent** — Twilio sends the SMS instantly to the lead
4. **CRM Updated** — Google Sheets updates automatically — lead marked as "Contacted"
5. **Day 2** — A personalized follow-up email sends via Gmail
6. **Day 5** — An urgency SMS fires with a message tailored to their insurance type
7. **Day 10** — A soft close email sends automatically
8. **Slack Alerts** — Agent gets notified at every step

**Result: Zero manual follow-up. Agents only make the call that converts.**

---

## 🛠️ Tools Used

| Tool | Purpose | Cost |
|------|---------|------|
| n8n | Workflow automation | Free (self-hosted) |
| Groq AI (Llama 3.3 70B) | Writes personalized SMS messages | Free tier |
| Twilio | Sends SMS to leads | ~$0.0075/SMS |
| Gmail | Sends follow-up emails | Free |
| Google Sheets | CRM / lead database | Free |
| Slack | Agent notifications | Free tier |

---

## 📋 Workflow Structure
Google Sheets Trigger
↓
Filter (New leads only)
↓
Groq AI — Writes personalized SMS
↓
Code Node — Extracts SMS text
↓
Twilio — Sends SMS #1
↓
Google Sheets — Updates status to "Contacted"
↓
Wait 2 Days
↓
Gmail — Sends follow-up email
↓
Wait 3 Days
↓
Code Node — Writes urgency SMS by insurance type
↓
Twilio — Sends urgency SMS #2
↓
Wait 5 Days
↓
Gmail — Sends soft close email
↓
Slack — Notifies agent

---

## 🚀 Setup Instructions

### 1. Prerequisites
- n8n instance (self-hosted or cloud)
- Groq API key — [console.groq.com](https://console.groq.com)
- Twilio account — [twilio.com](https://twilio.com)
- Google account (Sheets + Gmail)
- Slack workspace

### 2. Google Sheets Setup
Create a spreadsheet named **"Summit Insurance AI Automation"** with a tab called **"Leads"** and these columns:
Name | Phone | Email | Insurance Line | Lead Source | Date Added | Last Contact | Follow-up Status | Agent Name | Notes | SMS 1 Sent | Email 1 Sent | SMS 2 Sent | Email 2 Sent | Replied | Reply Date | Outcome

Phone numbers must be in format: `+1XXXXXXXXXX`

### 3. Import the Workflow
1. Download `lead-followup-sequence.json` from this repo
2. Open n8n → click **"Import"**
3. Upload the JSON file
4. Connect your credentials (Google Sheets, Gmail, Twilio, Slack, Groq)

### 4. Configure Credentials in n8n
- **Google Sheets** — OAuth2 or Service Account
- **Gmail** — OAuth2
- **Twilio** — Account SID + Auth Token
- **Slack** — OAuth2
- **Groq** — HTTP Header Auth (`Bearer gsk_yourkey`)

### 5. Update the Workflow
Replace these placeholders in the workflow:
- `[your number]` → your actual phone number
- `[your Twilio number]` → your Twilio number
- `#general` → your Slack channel name

### 6. Activate
- Toggle the workflow to **Active**
- Add a new lead row to Google Sheets with `Follow-up Status = New`
- Watch it run!

---

## 📊 Google Sheets Lead Status Values

| Status | Meaning |
|--------|---------|
| New | Just added, no contact yet |
| Contacted | First SMS sent |
| Responded | Lead replied |
| Booked | Call scheduled |
| Quoted | Quote provided |
| Enrolled | Converted! |
| Not Interested | Removed from flow |

---

## 💡 Insurance Line Logic

The urgency SMS (Day 5) automatically sends a different message based on insurance type:

- **Medicare** → AEP deadline urgency message
- **ACA** → Open enrollment deadline message  
- **Auto** → Rate savings message

---

## 📁 Files in This Repo
├── lead-followup-sequence.json   # n8n workflow — import this
├── README.md                     # This file
└── screenshots/                  # Workflow screenshots
└── workflow-overview.png

---

## 🔧 Customization

- Change wait times in the Wait nodes (currently 2, 3, 5 days)
- Edit the Groq prompt to match your agency's voice
- Add more insurance lines in the urgency SMS code node
- Change the Slack channel in the Slack node

---

## 📞 Contact

Built by Roshan — [roshan@callsmax.com](mailto:roshan@callsmax.com)

Free 2-week pilot available for independent insurance agencies.

---

## ⭐ If this helped you, give it a star!
