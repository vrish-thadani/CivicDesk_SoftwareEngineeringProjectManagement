# CivicDesk – Municipal Grievance Redressal for a City of 4 Million

**Case Study 16**  
**Author:** Vrish Thadani  
**Course:** B.Tech CSE 2025-29 • Software Engineering & Project Management

---

## 1. Executive Summary & Core Idea
The CivicDesk project aims to solve the severe inefficiencies in how a city of 4 million residents handles civic complaints (like potholes, streetlights, and garbage overflow). Currently, complaints arrive through four unlinked channels, leading to duplicate reports (e.g., the same pothole reported 11 times but fixed zero times) and a loss of citizen trust due to "verbal closures" with no real action.

**The Core Idea:** The technical problems are easy to fix. The hard problem is political. A dashboard system that exposes ward officers' inefficiencies without their buy-in will be intentionally sabotaged. Therefore, every design choice in CivicDesk treats the ward officer as a stakeholder with a vested interest, rather than a target of the system.

---

## 2. Business Requirements Document (BRD)

### Business Objectives
- **BO1:** One record per real-world problem across all channels (Target: < 3% incorrect merges).
- **BO2:** Predictable service times enforced via SLAs (escalations at 80%).
- **BO3:** Honest, verifiable closure (no closure without evidence; citizen-rejected closures reopen).
- **BO4:** Accountability that officers actively support.
- **BO5:** Transparent communication with citizens.

### Scope
- **In Scope:** Intake from phone, web, counter, and social media; deduplication; routing by ward/department; SLA escalation engine; field closure with photo evidence; commissioner and ward dashboards; public tracking.
- **Out of Scope (Phase 1):** Payments, contractor billing, automated staff penalties, predictive maintenance.

---

## 3. Stakeholder Management & Strategy
Based on an Influence × Interest matrix, the stakeholders are managed as follows:

- **Manage Closely (High Influence / High Interest):** 
  - *Commissioner, Ward Officers, Department Heads.*
  - *Strategy:* Co-design the system. Ward officers see their data 48 hours before the commissioner and can dispute or annotate it. Department heads co-own the SLAs.
- **Keep Satisfied (High Influence / Lower Interest):**
  - *Councillors, Media, Social Media Influencers.*
  - *Strategy:* Provide a public status page and official reply templates to prevent surprises.
- **Keep Informed (Lower Influence / High Interest):**
  - *Citizens, Field Engineers.*
  - *Strategy:* Provide ticket IDs and WhatsApp tracking for citizens. Field engineers get a simple offline-capable app so they aren't blamed for upstream delays.
- **Monitor (Lower Influence / Lower Interest):**
  - *Operators, IT ops, Auditors.*

---

## 4. Software System Design

### Routing Engine
- **Logic:** GPS Geotag → Point-in-Polygon lookup against ward boundaries → Category → Department map → Assigned to the specific ward's engineer.
- **Edge cases:** Unclear locations go to a triage queue. Social posts use NLP assist with human confirmation.

### Deduplication Pipeline
- **Normalise:** Extract category, lat/long, accuracy radius, timestamp, and photo.
- **Candidate Search:** Geospatial index finds open tickets of the *same category* within **≤ 50 meters**, reported within the last **≤ 72 hours**.
- **Confidence Rule:** 
  - If exactly one candidate and GPS accuracy ≤ 20m: **Auto-merge**.
  - If several candidates or poor GPS (>50m): Send to human review.
- **Merge Strategy:** The report is attached to the master ticket as a "+1".
- **Design Philosophy:** *Prefer a false split over a false merge.* A false merge silently buries a real complaint, which is the exact failure CivicDesk is trying to solve. Incorrect merges target: < 3%.

### SLA & Escalation Rules
- **Streetlight:** 48 hours (Escalation at 38h 24m)
- **Water Leak:** 24 hours (Escalation at 19h 12m)
- **Pothole:** 7 days (Escalation at 5d 14h 24m)
- **Garbage:** 12 hours (Escalation at 9h 36m)
- **Rule:** Escalate when elapsed ≥ 80% of SLA. Breach when elapsed > 100%.

---

## 5. Project Management (PERT/CPM) & Risks

### Timeline Analysis
- **Critical Path:** A-B-D-F-G = 21 weeks.
- **Probability:** 93.6% chance of completion within 24 weeks.

### Buffer Strategy (Monsoon Overlap)
Instead of padding individual tasks, a **single 3-week shared project buffer** is placed immediately after activity F (Integration, Ward Pilot, and UAT). 
*Why?* Activity F is on the critical path, has zero float, and has the widest variance (2 to 12 weeks) because it depends on live field conditions and explicitly collides with the monsoon season. A pooled buffer protects the final delivery date from the highest-risk activity.

### Key Risks
1. **Organisational Resistance (Score: 20):** Mitigated by co-designing with officers, allowing them dispute rights, and using normalised metrics.
2. **Monsoon Delays (Score: 16):** Mitigated by the 3-week project buffer.
3. **Engineers Skip Updates (Score: 16):** Mitigated by a simple offline app requiring photo-only closure.

---

## 6. Testing & Quality Assurance (QA)

### Boundary Value Analysis (BVA) for SLAs
Testing focuses on the exact boundaries of the 80% escalation and 100% breach rules.
- *Example (Streetlight - 48h):* 
  - 38h 23m (No escalation) → 38h 24m (Escalate)
  - 48h 00m (No breach) → 48h 01m (Breach)

### Deduplication Accuracy Tests
Testing includes hard negative cases to ensure the auto-merge rule doesn't falsely group distinct problems:
- Same place, same hour, different category (water leak vs pothole) → **No merge.**
- Two distinct potholes 30m apart → **Operator review (No auto-merge).**
- Citizen replies "different problem" to a merge notice → **Automatic split.**

---

## 7. Metrics Dashboard (Goodhart's Law)
To prevent "Goodhart's Law" (where a measure becomes a target and ceases to be a good measure), the commissioner dashboard uses anti-gaming controls:
1. **Metrics are shown in pairs:** "SLA Compliance" is paired with "Reopen Rate". (Closing tickets early to game SLAs will cause the reopen rate to spike).
2. **Normalisation:** Wards are compared against their own history and similar wards (based on inflow and area), not put into a raw league table.
3. **Audited CSAT:** Citizen satisfaction is measured via random-sample callbacks by a central team, preventing wards from cherry-picking happy citizens.

---

## How to Run the Website Locally
The website acts as a digital brochure and presentation for this case study. It is built with raw HTML, CSS, and JS. 

To view it locally, open a terminal in the project directory and run:
```bash
python3 -m http.server 8000
```
Then navigate to: [http://localhost:8000](http://localhost:8000)
