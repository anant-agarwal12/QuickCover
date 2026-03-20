# 🛡️ GigShield — AI-Powered Parametric Income Insurance for India's Gig Economy

> **Guidewire DEVTrails 2026 | University Hackathon**
> **Persona:** Food Delivery Partners (Zomato / Swiggy)
> **Platform:** Android (Native — Kotlin)
> **Phase 1 Submission | March 20, 2026**

---

## 📌 Table of Contents

1. [The Problem We're Solving](#the-problem-were-solving)
2. [Our Solution — GigShield](#our-solution--gigshield)
3. [Persona & Scenario Walkthroughs](#persona--scenario-walkthroughs)
4. [Weekly Premium Model](#weekly-premium-model)
5. [Parametric Trigger Design](#parametric-trigger-design)
6. [Platform Justification — Why Android?](#platform-justification--why-android)
7. [AI/ML Integration Plan](#aiml-integration-plan)
8. [🔴 Phase 1 Market Crash — Adversarial Defense & Anti-Spoofing Strategy](#-phase-1-market-crash--adversarial-defense--anti-spoofing-strategy)
9. [Tech Stack & Architecture](#tech-stack--architecture)
10. [Development Roadmap](#development-roadmap)

---

## The Problem We're Solving

India has over **12 million food delivery partners** working for platforms like Zomato and Swiggy. These workers operate entirely on a per-delivery commission model — no fixed salary, no sick leave, no safety net. A single week of heavy monsoon rain, an area-wide AQI spike, or a sudden local curfew can erase 20–40% of their monthly income overnight.

**Current reality for a delivery partner on a bad week:**

| Event | Avg. Income Lost | Insurance Available? |
|---|---|---|
| Monsoon flooding (Mumbai, 3 days) | ₹1,200 – ₹1,800 | ❌ None |
| AQI > 400 (Delhi, 5 days) | ₹2,000 – ₹2,500 | ❌ None |
| Unplanned curfew / local bandh | ₹800 – ₹1,500 | ❌ None |
| Platform app outage (>4 hours) | ₹400 – ₹700 | ❌ None |

These are not rare edge cases. In cities like Mumbai, Delhi, Chennai, and Bengaluru, such disruptions occur **6–10 times per year on average**, and often cluster during monsoon season.

GigShield exists to close this gap with a zero-friction, AI-automated parametric insurance product built specifically for the delivery worker's lifestyle.

---

## Our Solution — GigShield

GigShield is an **Android-first, AI-native parametric income insurance platform** that:

- Enrolls a delivery partner in under **3 minutes** using their platform ID (Zomato/Swiggy worker ID)
- Issues a **weekly policy** priced dynamically based on real-time local risk
- **Automatically detects** qualifying disruptions via weather, AQI, traffic, and platform signals
- **Triggers and processes claims without the worker filing anything** — zero-touch payout
- Pays directly to the worker's **UPI/bank account within 2 hours** of a disruption event closing
- Employs a **multi-layer AI fraud detection engine** to ensure platform integrity

No paperwork. No claim forms. No waiting. Just protection.

---

## Persona & Scenario Walkthroughs

### Persona: Ravi, 28 — Swiggy Partner, Bengaluru

Ravi delivers food in the Koramangala–HSR Layout–BTM corridor. He works 10–12 hours a day, 6 days a week. His average weekly take-home is ₹4,500–₹5,500. He has no savings buffer and supports his parents.

**Scenario A — Monsoon Flood Day**

> It's July. The IMD forecast says 80mm of rainfall. By 11 AM, water is knee-deep on 80th Feet Road. Zomato suspends orders in Ravi's zone at 11:30 AM.

1. GigShield's weather trigger detects rainfall > 65mm threshold in Ravi's zone polygon.
2. The platform detects reduced order volume in Ravi's area as a corroborating signal.
3. Ravi's active weekly policy is queried. He's covered.
4. Disruption window is logged: 11:00 AM to 5:00 PM (6 hours).
5. Pro-rated payout of ₹330 is initiated to his UPI automatically at 5:30 PM.
6. Ravi receives a notification: *"We've got your back today. ₹330 credited."*

He never opened the app once.

---

**Scenario B — Delhi AQI Spike**

> It's November. Delhi's AQI hits 423 (Severe). Swiggy issues an optional safety advisory. Ravi's Delhi counterpart, Arjun, chooses not to ride.

1. AQI crosses the 400 threshold at 9 AM. Trigger fires.
2. Arjun's GPS confirms he's inactive (did not leave home zone for 4+ hours).
3. His inactivity is cross-validated against platform API signals (zero orders accepted).
4. Payout is calculated for the hours he was inactive due to the AQI event.
5. ₹280 credited by evening.

---

**Scenario C — Local Bandh (Social Disruption)**

> A sudden protest closes major arterial roads in a zone. No weather event. Pure social disruption.

1. GigShield ingests traffic API data — major roads in the zone show 0 km/h velocity for 3+ hours.
2. News API corroborates a declared bandh in that district.
3. Workers in the affected zone polygon are flagged as disruption-eligible.
4. Claims are batched and processed after a 2-hour cool-down confirmation window.

---

## Weekly Premium Model

We intentionally designed the financial model around the delivery worker's **weekly payout cycle**, not monthly.

### Why Weekly?

Most delivery platforms pay out earnings every 5–7 days. A monthly premium feels like a large, lump deduction. A weekly premium of ₹25–₹60 feels like buying a cup of chai — affordable and mentally frictionless.

### Dynamic Weekly Pricing Formula

```
Weekly Premium = Base Rate × Zone Risk Multiplier × Tenure Discount × Season Multiplier
```

| Variable | Description | Range |
|---|---|---|
| **Base Rate** | Platform average daily earnings × 7% | ₹25 – ₹55 |
| **Zone Risk Multiplier** | Historical disruption frequency in worker's home zone | 0.8x – 1.4x |
| **Tenure Discount** | Loyalty reduction for long-standing policyholders | 0.85x – 1.0x |
| **Season Multiplier** | Monsoon/Winter smog season surcharge | 1.0x – 1.25x |

### Tier Structure

| Tier | Weekly Premium | Max Weekly Payout | Trigger Hours Before Payout |
|---|---|---|---|
| **Basic Shield** | ₹29 | ₹500 | 4 hours |
| **Smart Shield** | ₹49 | ₹900 | 3 hours |
| **Full Shield** | ₹69 | ₹1,400 | 2 hours |

Workers on Smart Shield or above get access to the predictive weather alert 12 hours before a likely trigger event, giving them a chance to plan shifts.

### Payout Calculation

```
Payout = (Worker Avg Hourly Earnings) × (Confirmed Disruption Hours) × Coverage Multiplier
```

Capped at the tier's weekly payout limit. Pro-rated daily across a multi-day event.

---

## Parametric Trigger Design

Triggers are fully automated. No manual claim submission required.

| Trigger ID | Event | Threshold | Validation Source |
|---|---|---|---|
| `ENV-01` | Extreme Rainfall | > 65mm/day in zone | IMD / OpenWeatherMap API |
| `ENV-02` | Flood Zone Alert | Official flood advisory for PIN/zone | NDMA API + Google Crisis Map |
| `ENV-03` | AQI Severe | AQI > 400 in city zone | CPCB API / AQICNapi |
| `ENV-04` | Extreme Heat | > 44°C + Heat wave alert | IMD API |
| `SOC-01` | Local Curfew/Bandh | Road velocity < 5 km/h for 3+ hrs + news confirm | MapmyIndia Traffic API + News API |
| `SOC-02` | Platform Outage | Zomato/Swiggy API non-responsive for 4+ hrs | Synthetic monitoring via StatusPage mock |
| `SOC-03` | Night Curfew Zone | Official government order in PIN code area | Government alert API / mock |

**All triggers require corroboration from at least 2 independent data sources** before a claim window opens. This is the single most important fraud-resistance design decision in the system.

---

## Platform Justification — Why Android?

This was a deliberate, research-backed choice.

1. **Device Reality:** Over 96% of gig delivery workers in India use Android smartphones. The ₹8,000–₹15,000 price segment (Redmi, Realme, Samsung M-series) dominates this cohort. iOS is not relevant for this persona.

2. **UPI Deep Integration:** Android allows deep UPI intent-based payment flows natively. Payout confirmation UX is seamless on Android.

3. **Background Location & Sensor Access:** Parametric insurance requires reliable background GPS to validate presence in disruption zones. Android's WorkManager and FusedLocationProvider give us the tools to do this responsibly, with battery optimization in mind, in ways that aren't possible on iOS without major restrictions.

4. **Platform Worker ID Integration:** Zomato and Swiggy's worker-facing apps are Android-first. Our onboarding flow can deep-link to platform credential verification.

5. **Regional Language Support:** Android makes it straightforward to support Hindi, Tamil, Kannada, and Bengali UI — essential for delivery worker trust and comprehension.

---

## AI/ML Integration Plan

### 1. Dynamic Premium Engine (XGBoost + Real-time Feature Pipeline)

A gradient-boosted model trained on:
- Historical hyper-local weather patterns (zone-level, not city-level)
- Seasonal disruption calendars (monsoon months, festival curfews)
- Worker tenure, zone assignment, hours worked per week
- Historical claims density by zone

Output: Personalized weekly premium per worker, recalculated every Sunday night before the new policy week begins.

### 2. Fraud Detection AI (Multi-layer Ensemble)

See the full [Anti-Spoofing section below](#-phase-1-market-crash--adversarial-defense--anti-spoofing-strategy) — this is Phase 1's dedicated deep-dive.

### 3. Anomaly Detection on Payouts (Isolation Forest)

An Isolation Forest model runs on every payout batch to flag statistically anomalous claim patterns — sudden spikes in claims from a single zone, unusual correlated inactivity across many workers at non-disruption times, and outlier payout amounts relative to a worker's historical earnings profile.

### 4. Predictive Disruption Forecasting (LSTM Weather Model)

A lightweight LSTM trained on historical IMD rainfall and AQI data predicts the probability of a trigger-level event in the next 24–72 hours, per zone. Used to:
- Send proactive alerts to covered workers
- Dynamically adjust next week's premium offer in real time
- Pre-position liquidity reserves for likely payout events

### 5. Worker Risk Profiling (Clustering — K-Means)

Workers are silently clustered into risk profiles based on operating zone, shift hours, and historical income patterns. This is used to calibrate payout calculations and detect behavioral anomalies (e.g., a worker suddenly "moving" to a high-payout zone just before a trigger event fires).

---

## 🔴 Phase 1 Market Crash — Adversarial Defense & Anti-Spoofing Strategy

> *500 delivery partners. Fake GPS. Real payouts. A coordinated fraud ring just drained a platform's liquidity pool.*
> *Simple GPS verification is dead. How do you spot the faker from the genuinely stranded worker?*

This section is our response to the **Market Crash challenge** — a coordinated, large-scale GPS spoofing + fraud ring attack on a parametric insurance platform. This is the hardest problem in our domain and we've designed for it from Day 1.

---

### The Threat Model

A sophisticated fraud ring operating at scale has three attack vectors:

| Attack Type | Description | Scale Potential |
|---|---|---|
| **GPS Spoofing** | Workers use mock location apps to appear in a disrupted zone while physically elsewhere | High — apps like "Fake GPS Go" work on unrooted Android |
| **Coordinated Inactivity** | A ring of workers agrees to be "inactive" during a manufactured "trigger event" to claim payouts | Very High — social/WhatsApp coordination |
| **Synthetic Identity Clusters** | Multiple fake worker accounts registered under different names but linked by device fingerprint, network, or payment details | Medium — requires real Zomato/Swiggy IDs |
| **Trigger Manipulation** | Attempting to flood news/social signals to trigger `SOC-01` (bandh detection) artificially | Low — but must be defended against |

---

### Layer 1 — Mock Location Detection (Device-Level)

This is our first and hardest line of defense. Like Pokémon GO and Uber, **GigShield refuses to operate if a mock location provider is active on the device.**

**How we detect it:**

```kotlin
// Check if any mock location provider is active
fun isMockLocationEnabled(context: Context): Boolean {
    val locationManager = context.getSystemService(Context.LOCATION_SERVICE) as LocationManager
    val providers = locationManager.getProviders(false)
    for (provider in providers) {
        if (locationManager.isProviderEnabled(provider)) {
            val location = locationManager.getLastKnownLocation(provider)
            if (location != null && location.isFromMockProvider) {
                return true
            }
        }
    }
    // Additional check: Developer Options mock location app setting
    return Settings.Secure.getString(
        context.contentResolver,
        Settings.Secure.ALLOW_MOCK_LOCATION
    ) != "0"
}
```

**Additional device integrity checks:**
- **Google Play Integrity API** — replaces SafetyNet. Verifies the device hasn't been tampered with and is running genuine Android. Workers on rooted devices or emulators are flagged.
- **Developer Options Detection** — if Developer Options are enabled, the app prompts workers to disable them and logs the flag for risk scoring.
- **Location Provider Consistency Check** — GPS, Wi-Fi, and Cell Tower triangulation are cross-validated. If a worker's GPS says Koramangala but their cell tower says Whitefield, that's a red flag.

**What happens when spoofing is detected:**
1. The app displays a clear, non-alarming message: *"We couldn't verify your location. Please check your location settings."*
2. The session is logged as a spoofing attempt flag on the worker's risk profile.
3. Two consecutive spoofing flags within 30 days triggers a manual review hold on all future claims — not a ban, because the worker may genuinely have had a misconfigured app.
4. Five or more spoofing flags → automatic account suspension pending human review.

---

### Layer 2 — Behavioral GPS Trajectory Analysis (The Smart Layer)

A fraudster can spoof their location to a disrupted zone. But **they can't easily fake natural human movement patterns.**

We analyze GPS trajectory data with the following heuristics:

**Teleportation Detection:**
If a worker's GPS jumps from Point A to Point B — a distance that would take 20+ minutes to travel — in under 2 minutes, that's a teleportation event. Real workers don't teleport.

**Movement Entropy Scoring:**
A genuine delivery worker who is unable to work due to rain will show low-entropy movement — sitting at home, perhaps moving 50–200m occasionally. A fraudster using a static fake GPS coordinate will show *zero* entropy — a perfectly stationary dot that never wavers. Real GPS, even when stationary, drifts slightly. We score this.

**Historical Route Fingerprinting:**
Each worker has a historical delivery route fingerprint — the zones they typically operate in. If during a disruption event a worker's GPS suddenly places them in a zone they have *never* operated in over the past 8 weeks (but that zone happens to be in a payout-eligible disruption area), that's a high-risk flag.

---

### Layer 3 — Coordinated Ring Detection (Graph-Based Fraud Analysis)

A single bad actor is easy. **500 coordinated bad actors is a graph problem.**

We build a **Worker Activity Graph** where nodes are workers and edges represent:
- Shared device fingerprints or IMEI
- Same UPI/bank account destination
- Geographically co-located inactivity (all went "inactive" within minutes of each other in the same zone)
- Common registration metadata (same IP range, same device model batch, similar sign-up timestamps)

An anomaly score is computed on every payout batch using **graph centrality metrics**. A cluster of 15+ workers all going inactive simultaneously in the same zone, registered within the same 2-week window, with payouts routing to the same payment graph cluster — that's not a coincidence. That's a ring.

**Action:** Entire cluster is flagged. Payouts are held pending **human review** (see Layer 5). The specific trigger event is re-evaluated for legitimacy.

---

### Layer 4 — Payout Spike Anomaly Detection

**The rule is simple: sudden spikes in payout volume initiate mandatory human review — always, no exceptions.**

We define a spike as:
> Total claims in any 6-hour window exceeding **2.5× the rolling 4-week average** for that zone and trigger type.

When a spike is detected:
1. All claims above the spike threshold are automatically **held in a "Pending Review" queue**
2. A human adjudicator is notified within 15 minutes (target SLA)
3. The adjudicator reviews the top 20 highest-value claims in the spike for anomalies
4. If the spike is legitimate (e.g., an unusually severe monsoon event), claims are batch-approved
5. If anomalies are found, the entire spike batch is quarantined pending deeper investigation

**Why human review, not just AI?**

Because in catastrophic, large-scale fraud — the kind that drains a liquidity pool — the cost of an AI false negative is platform failure. Human review is our circuit breaker. The AI handles volume; humans handle edge cases and exceptions at scale.

---

### Layer 5 — Cross-Signal Truth Table

The most powerful fraud resistance mechanism: **no single signal ever authorizes a payout alone.**

Every claim must satisfy the following truth table before any payout is released:

| Signal | Required for Payout? | Data Source |
|---|---|---|
| Parametric trigger confirmed | ✅ Mandatory | Weather/AQI/Traffic API |
| Worker GPS in disruption zone | ✅ Mandatory | FusedLocationProvider |
| Worker inactivity confirmed | ✅ Mandatory | Platform API + motion sensors |
| No mock location flag | ✅ Mandatory | Device Integrity check |
| No spoofing flags in last 30 days | ✅ Mandatory | Internal risk score |
| No ring-detection cluster flag | ✅ Mandatory | Graph anomaly model |
| Payout within normal range | ✅ Mandatory | Isolation Forest score |
| Trigger corroborated by 2+ sources | ✅ Mandatory | Multi-API validation |

**All eight conditions must be true.** Fail any one → hold for human review, not auto-reject. We never automatically punish workers. We hold and review.

---

### Layer 6 — Gradual Trust Building (Tenure-Based Payout Velocity)

New accounts are the highest risk. We implement a **trust ramp**:

| Account Age | Max Payout Per Claim | Claims Per Week |
|---|---|---|
| 0–4 weeks | ₹250 | 1 |
| 5–12 weeks | ₹600 | 2 |
| 13–26 weeks | Full tier limit | 3 |
| 26+ weeks | Full tier limit | Unlimited |

This makes it economically unattractive to spin up fake accounts — the payoff from new accounts is too small to justify the operational cost of running a fraud ring.

---

### How We Distinguish the Genuine Stranded Worker from the Faker

This is the core philosophical question of the Market Crash challenge.

| Signal | Genuine Stranded Worker | Fraud Actor |
|---|---|---|
| GPS location | In historical operating zone | Teleported to disruption zone |
| GPS movement entropy | Low but non-zero (natural drift) | Zero (static fake pin) |
| Platform API activity | Zero orders received/accepted | Zero orders (but suspicious timing) |
| Device integrity | Clean | Developer options on / mock provider active |
| Historical pattern match | Consistent with their profile | Sudden zone migration |
| Network metadata | Home/local cell tower match | Mismatch with claimed location |
| Ring graph score | Isolated node | High-centrality cluster node |

A genuine worker will pass all eight cross-signal checks naturally. A fraudster will fail at least 2–3, which triggers a review — not an automatic denial. **We are designed to protect honest workers first, and catch fraud second.**

---

## Tech Stack & Architecture

```
┌──────────────────────────────────────────────────────┐
│              ANDROID APP (Kotlin + Jetpack Compose)  │
│  • FusedLocationProvider (background GPS tracking)   │
│  • Play Integrity API (device attestation)           │
│  • Retrofit (API calls) + Room (local cache)         │
│  • WorkManager (background sync jobs)                │
│  • Firebase Push (disruption alerts + payout notifs) │
└─────────────────────┬────────────────────────────────┘
                      │ HTTPS / REST
┌─────────────────────▼────────────────────────────────┐
│           BACKEND (FastAPI — Python)                  │
│  • Worker API, Policy API, Claims API, Payout API    │
│  • Trigger Engine (cron + webhook listeners)         │
│  • Fraud Scoring Engine                              │
│  • ML Model Serving (XGBoost, Isolation Forest)      │
└──────────────┬───────────────────┬───────────────────┘
               │                   │
┌──────────────▼──────┐  ┌─────────▼──────────────────┐
│  PostgreSQL          │  │  Redis (session + queue)    │
│  (core data store)   │  │  + Celery (async jobs)      │
└─────────────────────┘  └────────────────────────────┘
               │
┌──────────────▼──────────────────────────────────────┐
│          EXTERNAL INTEGRATIONS                       │
│  • OpenWeatherMap API (rainfall, temp)               │
│  • CPCB AQI API (air quality)                        │
│  • MapmyIndia Traffic API (road velocity)            │
│  • NDMA Flood Alerts API                             │
│  • News API (bandh/curfew corroboration)             │
│  • Razorpay (payout sandbox — UPI/bank transfer)     │
└─────────────────────────────────────────────────────┘
```

### AI/ML Stack

| Component | Model / Tool | Hosting |
|---|---|---|
| Premium calculation | XGBoost | FastAPI + joblib |
| Fraud / anomaly detection | Isolation Forest | FastAPI + scikit-learn |
| Ring detection | NetworkX graph analysis | Celery background task |
| Disruption forecasting | LSTM (TensorFlow Lite on-device) | Android edge inference |
| Worker clustering | K-Means | Offline batch, weekly retrain |

---

## Development Roadmap

### ✅ Phase 1 (March 4–20) — Ideation & Foundation
- [x] Product concept finalized (Food delivery persona, Android, weekly pricing)
- [x] Adversarial defense & anti-spoofing architecture designed
- [x] System architecture and API contract defined
- [x] README with full strategy documentation (this document)
- [ ] 2-minute strategy video (uploading separately)
- [ ] Repository scaffolding — Android project + FastAPI skeleton

### 🔄 Phase 2 (March 21–April 4) — Automation & Protection
- [ ] Worker onboarding flow (Android — Zomato/Swiggy ID verification)
- [ ] Policy creation UI + weekly pricing engine
- [ ] 3–5 automated parametric triggers (weather + AQI + traffic)
- [ ] Zero-touch claim processing pipeline
- [ ] Mock UPI payout integration (Razorpay sandbox)
- [ ] GPS anti-spoofing implementation (Play Integrity API)

### 🔄 Phase 3 (April 5–17) — Scale & Optimise
- [ ] Full fraud detection AI pipeline (graph ring detection + isolation forest)
- [ ] Worker dashboard (earnings protected, active coverage, payout history)
- [ ] Admin/insurer dashboard (loss ratios, predictive disruption analytics)
- [ ] Final 5-minute demo video with simulated disruption + auto-claim
- [ ] Final pitch deck

---

## Team

> Sannjusmita Das        
> Krish Sharma        
> Anant Agarwal            

---

## License

This project is submitted as part of the Guidewire DEVTrails 2026 University Hackathon.

---

*Built with care for the 12 million delivery partners who keep India running, rain or shine.*
