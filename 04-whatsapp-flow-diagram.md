# Deliverable 4 — WhatsApp Flow Diagram (Visual)

Hand this to whoever sets up your automation tool. It maps the entire lead journey from ad click to customer.

```mermaid
flowchart TD
    A[New Lead<br/>Meta Lead Ad / Landing Form] --> B{{Webhook / Zapier / Pabbly}}
    B --> C[/Log lead in Tracker Sheet<br/>Status: NEW/]
    B --> D[[Send Message 1<br/>within 60 seconds]]

    D --> E{Lead replies?}

    E -->|No reply| F[Follow-up 1<br/>+20 min]
    F --> G{Reply?}
    G -->|No| H[Follow-up 2<br/>+1 day]
    H --> I{Reply?}
    I -->|No| J[Follow-up 3<br/>+3 days]
    J --> K{Reply?}
    K -->|No| L[Tag COLD<br/>+5 days]
    L --> M[(Monthly cold-lead<br/>re-engagement broadcast)]

    E -->|Replies 1<br/>Pricing| N[Ask: city + budget + timeline]
    E -->|Replies 2<br/>Book| O[Send booking link]
    E -->|Replies 3<br/>Exploring| P[Tag NURTURE<br/>send helpful content]

    G -->|Yes| Q{Route by intent}
    I -->|Yes| Q
    K -->|Yes| Q
    N --> Q
    P --> M

    Q -->|Fit: budget + timeline OK| R[Tag HOT / QUALIFIED]
    Q -->|Not ready / low budget| P

    R --> O
    O --> S[Tag APPOINTMENT BOOKED]
    S --> T[[24h + 2h reminders]]
    T --> U{Showed up?}
    U -->|Yes| V[Sales conversation]
    U -->|No| W[Reschedule sequence]
    W --> T

    V --> X{Closed?}
    X -->|Yes| Y([Tag WON / CUSTOMER<br/>log Deal Value in Tracker])
    X -->|No| Z[Tag NURTURE / LOST<br/>add to follow-up]
    Z --> M

    Y --> AA[/Feeds Monthly Report:<br/>Cost per Customer + ROI/]

    style A fill:#4285f4,color:#fff
    style D fill:#25d366,color:#fff
    style T fill:#25d366,color:#fff
    style Y fill:#0f9d58,color:#fff
    style L fill:#db4437,color:#fff
    style AA fill:#f4b400,color:#000
```

### How to read it
- **Blue** = entry point (the ad/form).
- **Green** = automated WhatsApp actions (the part that runs without you).
- **Red** = cold lead (recycled monthly, never thrown away).
- **Green oval (WON)** = a paying customer — this is what feeds your ROI report.
- **Yellow** = the closed-loop reporting that justifies your premium pricing.

> If your tool doesn't render Mermaid, paste this into the live editor at https://mermaid.live to view/export it as an image.
