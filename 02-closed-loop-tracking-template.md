# Deliverable 2 — Closed-Loop Cost-Per-Customer Tracking

**Goal:** Stop reporting "we got 200 leads." Start reporting **"we got you 14 paying customers at ₹X each, and ₹Y in revenue from ₹Z ad spend."** This is the number business owners pay premium money for.

You get two things here:
1. A **Lead Tracker** (row per lead) — import the included `lead-tracker-template.csv` into Google Sheets.
2. A **Monthly Client Report** (the dashboard you actually send the client).

---

## PART A — Lead Tracker (Sheet 1)

Import `lead-tracker-template.csv` into a new Google Sheet. One row = one lead. Columns:

| Column | Field | What goes in it |
|--------|-------|-----------------|
| A | Lead ID | Auto/sequential (1,2,3…) |
| B | Date Received | Date the lead came in |
| C | Name | Lead's name |
| D | Phone | WhatsApp number |
| E | Source / Campaign | e.g. "Meta - Lead Gen - Offer A" |
| F | Ad Spend Allocated | (optional per-lead; usually left blank — spend is totalled in report) |
| G | First Contact Time | When WhatsApp Message 1 fired |
| H | Response Time (mins) | Minutes from receipt to first contact |
| I | Status | NEW / CONTACTED / QUALIFIED / BOOKED / SHOWED / WON / NURTURE / COLD / LOST |
| J | Qualified? | YES / NO |
| K | Appointment Booked? | YES / NO |
| L | Customer (Won)? | YES / NO |
| M | Deal Value (₹) | Revenue from this customer (0 if not won) |
| N | Notes | Free text |

### Status flow
`NEW → CONTACTED → QUALIFIED → BOOKED → SHOWED → WON`
(side states: `NURTURE`, `COLD`, `LOST`)

---

## PART B — Monthly summary formulas

Put these in a "Summary" tab. Assume lead data is in `Tracker!A2:M1000`.

```
Total Leads          =COUNTA(Tracker!A2:A1000)
Qualified Leads      =COUNTIF(Tracker!J2:J1000,"YES")
Appointments Booked  =COUNTIF(Tracker!K2:K1000,"YES")
Customers Won        =COUNTIF(Tracker!L2:L1000,"YES")
Total Revenue (₹)    =SUM(Tracker!M2:M1000)
Avg Response Time    =AVERAGE(Tracker!H2:H1000)

# You enter these two manually each month:
Ad Spend (₹)         =  [from Meta Ads Manager]
Agency Fee (₹)       =  [your retainer]

# The numbers that matter:
Total Investment (₹)     = Ad Spend + Agency Fee
Cost Per Lead (₹)        = Ad Spend / Total Leads
Cost Per Qualified Lead  = Ad Spend / Qualified Leads
Cost Per Customer (CAC)  = Total Investment / Customers Won
Lead→Customer Rate (%)   = Customers Won / Total Leads * 100
Qualified→Customer (%)   = Customers Won / Qualified Leads * 100
ROAS                     = Total Revenue / Ad Spend
ROI (%)                  = (Total Revenue - Total Investment) / Total Investment * 100
```

> **Tip:** Cost Per Customer = (Ad Spend + Your Fee) ÷ Customers Won is your hero metric. When ROI is clearly positive, your retainer is no longer a "cost" in the client's mind — it's an investment with a known return. That's how you justify raising it.

---

## PART C — The Monthly Client Report (what you send)

Keep it one page. This is the layout:

```
────────────────────────────────────────────
   {CLIENT NAME} — Performance Report
   {Month, Year}
────────────────────────────────────────────

💰 THE BOTTOM LINE
   Ad Spend:            ₹ ______
   Agency Fee:          ₹ ______
   Total Investment:    ₹ ______
   Revenue Generated:   ₹ ______
   ➡️  ROI:              ____ %   (₹__ back for every ₹1 in)

🎯 RESULTS
   Leads Generated:      ____
   Qualified Leads:      ____
   Appointments Booked:  ____
   Customers Won:        ____
   Cost Per Customer:   ₹ ______

⚡ SPEED (our edge)
   Avg. first response:  ___ mins   (industry: hours/never)
   Cold leads revived:   ____ customers from old leads

📈 WHAT WORKED
   Top campaign:        __________
   Best creative/hook:  __________

🔜 NEXT MONTH'S PLAN
   - __________
   - __________
────────────────────────────────────────────
```

### Why this report changes everything
- It's written for the **owner**, not the marketing manager.
- It leads with **money in vs. money out**, not vanity metrics.
- "Avg response: 3 mins" and "revived 4 dead leads" are proof points competitors can't show.
- Once the client sees positive ROI in black and white, a fee increase becomes an easy conversation.

---

## Setup checklist
- [ ] Import `lead-tracker-template.csv` into Google Sheets
- [ ] Add the Summary tab with the formulas above
- [ ] Connect your WhatsApp tool so status changes update column I/L (or update manually daily at first)
- [ ] Build the one-page report as a Google Slides/Doc template
- [ ] Fill it for one client this month and use it as your repricing proof
