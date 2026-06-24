# Deliverable 1 — WhatsApp Speed-to-Lead Automation Flow

**Goal:** Contact every new lead on WhatsApp in under 60 seconds, qualify them automatically, book them, and re-engage the ones who go cold — so the client's sales team only talks to warm, qualified people.

**Why it wins:** In India, leads respond on WhatsApp, not email/phone. Most agencies just hand over a lead sheet. You will own the first response, the qualification, and the follow-up — the part that actually decides whether ad spend turns into customers.

---

## 1. The tools you need (pick one)

| Tool | Approx. cost/month | Best for |
|------|-------------------|----------|
| AiSensy | ₹999–₹2,399 | Cheapest start, good automation, broadcast |
| WATI | ₹2,400+ | Clean UI, team inbox, popular with agencies |
| Interakt | ₹2,000+ | Shopify/D2C friendly |

All three run on the **official WhatsApp Business API** (so no ban risk) and connect to Meta Lead Ads + landing-page forms via a webhook or Zapier/Make/Pabbly.

**Connection path:**
`Meta Lead Form / Landing page form` → (webhook or Zapier/Pabbly) → `WhatsApp tool` → `CRM sheet (Deliverable 2)`

> Note: WhatsApp template messages for the *first* outbound message must be pre-approved by Meta. Submit the Message 1 template below for approval before going live.

---

## 2. The trigger logic

- **Trigger:** A new lead is created (form submit / Meta Lead Ad).
- **Action within 30–60 seconds:** Send Message 1 automatically.
- **Tag the lead** with source (campaign name) so you can track which ad produced which customer later.

---

## 3. The message sequence (exact copy)

> Replace `{{1}}` with lead's first name, `{Business}` with the client's brand, `{Offer}` with the campaign offer. Keep it conversational, not corporate.

### Message 1 — Instant (0–60 seconds) — *approved template*
```
Hi {{1}}, thanks for your interest in {Business}! 🙌
This is {AgentName} from {Business}. I'd love to help you with {Offer}.

Quick question so I can guide you properly:
What are you mainly looking for?

1️⃣ Pricing & details
2️⃣ Book a call / visit
3️⃣ Just exploring for now
```
*Reply with 1, 2, or 3.*

### Qualification branches (based on reply)

**If "1" (Pricing & details):**
```
Great! To share the most relevant pricing, can you tell me:

- Your city/location? 📍
- Your budget range?
- When are you looking to get started? (This week / This month / Later)
```
→ If budget + timeline are a fit → tag **HOT**, route to sales + offer to book (go to Message "Book").
→ If "Later" / low budget → tag **NURTURE** (go to nurture sequence).

**If "2" (Book a call/visit):**
```
Perfect! Here's the calendar — pick a slot that works for you 👇
{BookingLink}

Once you book, I'll send a confirmation + reminder. See you there! ✅
```
→ Tag **HOT / Appointment Booked**.

**If "3" (Just exploring):**
```
Totally fine, {{1}}! 😊 I'll send you a few things that usually help people decide.
No pressure at all — reply "STOP" anytime.
```
→ Tag **NURTURE**.

### Message "Book" (for HOT leads who haven't booked yet)
```
You're a great fit, {{1}}! 🎯
Let's lock a quick 10-min call so we can get you started.
Pick a slot 👉 {BookingLink}
```

---

## 4. No-response follow-up cadence (the part nobody does)

If the lead does NOT reply to Message 1, fire these automatically:

| Step | Timing | Message |
|------|--------|---------|
| Follow-up 1 | +20 minutes | `Hi {{1}}, just checking — did you get my message about {Offer}? Happy to answer any quick questions 😊` |
| Follow-up 2 | +1 day | `Hi {{1}}, still keen on {Offer}? We have limited slots this week. Want me to hold one for you?` |
| Follow-up 3 | +3 days | `Hey {{1}}, last check-in from my side 🙏 If now isn't right, no worries — should I check back next month?` |
| Mark status | +5 days | If still no reply → tag **COLD**, move to monthly re-engagement broadcast. |

---

## 5. Appointment reminders (cuts no-shows)

For every booked lead:
- **24 hours before:** `Hi {{1}}, reminder for your call/visit with {Business} tomorrow at {Time}. Reply "YES" to confirm or "RESCHEDULE" to change.`
- **2 hours before:** `See you soon, {{1}}! 🙌 Your appointment is at {Time}. Here's the link/location: {Detail}`

---

## 6. Status tags (these feed Deliverable 2)

`NEW → CONTACTED → QUALIFIED(HOT) → APPOINTMENT BOOKED → SHOWED UP → CUSTOMER (WON)`
Side tags: `NURTURE`, `COLD`, `LOST`.

Every status change should update the tracking sheet so you can report **cost per actual customer**, not cost per lead.

---

## 7. Cold-lead re-engagement (monthly)

Once a month, broadcast to all `NURTURE` + `COLD` leads:
```
Hi {{1}}! 👋 This month {Business} has {NewOffer/Discount}.
Want me to share the details? Reply "YES" 🙂
```
This squeezes extra customers out of leads you already paid for — pure margin, no extra ad spend. It's also a strong number to show clients ("we revived 4 dead leads into customers this month").

---

## 8. Setup checklist

- [ ] Create WhatsApp Business API account on chosen tool
- [ ] Submit Message 1 as an approved template
- [ ] Connect Meta Lead Ads + landing forms (webhook / Zapier / Pabbly)
- [ ] Build the branch logic above in the tool's flow builder
- [ ] Connect output to the tracking sheet (Deliverable 2)
- [ ] Test end-to-end with a dummy lead before going live
- [ ] Launch on ONE client first, measure for 2 weeks, then roll out
