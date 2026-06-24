# Deliverable 6 — Webhook / Integration Setup (Meta Lead Ads → WhatsApp)

This connects the pieces so a new lead automatically triggers the WhatsApp flow from Deliverable 1 and logs into the tracker from Deliverable 2 — with zero manual work.

**The pipeline:**
```
Meta Lead Ad (or landing page form)
        │
        ▼
Automation connector  (Pabbly Connect  /  Zapier  /  Make)
        │
        ├──► WhatsApp tool (AiSensy / WATI)  → fires Message 1 in <60s
        └──► Google Sheet (Lead Tracker)      → logs lead as NEW
```

> **India tip:** Use **Pabbly Connect**. It has affordable one-time/annual pricing (vs. Zapier's per-task monthly cost), which matters when you run this across all 6 clients. Steps below use Pabbly; Zapier/Make are nearly identical conceptually.

---

## Prerequisites
- [ ] Meta Business account with a Lead Ad form live (or a landing page that posts form data)
- [ ] WhatsApp Business API account on AiSensy or WATI, with **Message 1 template approved**
- [ ] A Google account for the Lead Tracker sheet
- [ ] A Pabbly Connect account

---

## Part A — Meta Lead Ads → Pabbly

1. In Pabbly Connect, click **Create Workflow** → name it `{Client} - Lead to WhatsApp`.
2. **Trigger app:** choose **Facebook Lead Ads**.
3. **Trigger event:** `New Lead Instant`.
4. Click **Connect** → authorize your Facebook account.
5. Select the **Page** and the **Lead Form** for that client.
6. Click **Save & Send Test Request**, then submit a test lead in Meta's [Lead Ads Testing Tool](https://developers.facebook.com/tools/lead-ads-testing) so Pabbly captures sample fields (name, phone, email, campaign).

---

## Part B — Pabbly → WhatsApp (AiSensy example)

1. Add an **Action** step → search **AiSensy** (or **WATI**).
2. **Action event:** `Send Template Message`.
3. **Connect** using your AiSensy API key (AiSensy → Manage → API Key).
4. Map the fields:
   - **Phone number** → map from Meta lead's `phone_number` (prefix country code `91` if missing — see Part D).
   - **Template name** → your approved Message 1 template.
   - **Variable {{1}}** → map to lead's `full_name` / `first_name`.
5. Save & send a test → confirm the WhatsApp message arrives on the test number.

### WATI variant
- Action app: **WATI** → event `Send Template Message` → connect via WATI API endpoint + access token (WATI → Settings → API) → map number + template + params the same way.

---

## Part C — Pabbly → Google Sheet (log the lead)

1. Add another **Action** step → **Google Sheets** → event `Add New Row`.
2. Connect your Google account, pick the **Lead Tracker** spreadsheet + tab.
3. Map columns to match `lead-tracker-template.csv`:
   - Date Received → lead `created_time`
   - Name → `full_name`
   - Phone → `phone_number`
   - Source / Campaign → `campaign_name` (or `ad_name`)
   - Status → set a static value `NEW`
4. Save & test → confirm a new row appears.

---

## Part D — Common gotchas (fix these before launch)

| Problem | Fix |
|---------|-----|
| WhatsApp not sending | Message template not approved, or number lacks country code. Use a Pabbly **Text Formatter / Number Format** step to prepend `91`. |
| Duplicate leads | Add a Pabbly **filter** or use the Sheet's lead phone as a dedupe key. |
| Phone has spaces/`+` | Add a formatter step to strip non-digits before sending. |
| Test works, live doesn't | Re-check the form is **published** (not in draft) and the FB connection hasn't expired. |
| Leads delayed | Meta "Instant" trigger is near-real-time; if using polling, set the shortest interval your plan allows. |

---

## Part E — Status updates back to the sheet (for closed-loop reporting)

To report cost-per-customer, the sheet's **Status** and **Deal Value** columns must update as leads progress. Two options:

- **Manual (start here):** your team updates Status/Deal Value daily in the sheet. Simple, works from day one.
- **Automated (later):** in AiSensy/WATI, set up flow steps or webhooks that, on a tag change (e.g. `WON`), call Pabbly → `Update Row` in the sheet. Match the row by phone number.

Start manual, automate once the process is proven.

---

## Launch checklist
- [ ] Workflow built: Meta → WhatsApp → Sheet
- [ ] Message 1 template approved and tested end-to-end
- [ ] Country-code formatting verified
- [ ] Tested with a real form submission (not just Pabbly's test)
- [ ] Team trained to update Status + Deal Value daily
- [ ] Live on ONE client first; monitor for 48 hours before scaling
