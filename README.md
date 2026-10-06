# CivicDesk Case Study Presentation

This repository contains the presentation website for **Case Study 16: CivicDesk - Municipal Grievance Redressal for a City of 4 Million**.

## About the Project

The CivicDesk case study explores the challenges of municipal grievance redressal in a large city. Currently, citizen complaints arrive through multiple unlinked channels (phone, web, counter, social media). This leads to severe inefficiencies, such as duplicate reports (e.g., the same pothole reported 11 times), unresolved issues due to verbal closures, and a complete lack of accountability and trust. 

This project presents the CivicDesk solution, which focuses not just on the technical fixes (like a centralized ticket store and deduplication), but heavily on the political realities of implementation. 

**Key areas covered in this case study include:**
- **Business Requirements & Scope:** Defining in-scope features like deduplication, SLA tracking, and verifiable closures, while purposefully keeping complex features (like automated penalties) out of phase 1.
- **Stakeholder Strategy:** Recognizing that ward officers will sabotage a system that merely exposes them. The strategy treats them as partners (Manage Closely) who co-design the system and view their data before it goes public.
- **System Design:** An architecture flow featuring a robust Deduplication Pipeline (based on 50m radius and 72h windows) that explicitly prefers false splits over false merges to ensure no real complaint is silently buried.
- **Project Plan (PERT/CPM):** A critical path analysis resulting in a 21-week timeline, featuring a strategic 3-week shared buffer to protect against monsoon delays during field pilots.
- **Metrics Dashboard:** A design based on Goodhart's Law. Metrics are paired (e.g., SLA Compliance paired with Reopen Rate) and normalized to prevent gaming the system.

## How to View Locally

You can view the presentation website by running a simple local HTTP server. 

If you have Python installed, run the following command in the project directory:

```bash
python3 -m http.server 8000
```

Then, open your web browser and navigate to: [http://localhost:8000](http://localhost:8000)

## Author
Prepared by **Vrish Thadani**
Course: B.Tech CSE 2024-28 • Software Engineering & Project Management
<img width="456" height="606" alt="Screenshot 2026-10-06 at 1 21 33 PM" src="https://github.com/user-attachments/assets/354ebe24-ca3f-4ec0-b29c-579e3e08fa67" />
<img width="444" height="606" alt="Screenshot 2026-10-06 at 1 21 41 PM" src="https://github.com/user-attachments/assets/91f60126-3a58-4d05-85ba-065e7ec76421" />
<img width="460" height="610" alt="Screenshot 2026-10-06 at 1 21 26 PM" src="https://github.com/user-attachments/assets/335d6baf-8cdd-479c-95c6-286a78fde200" />
<img width="458" height="618" alt="Screenshot 2026-10-06 at 1 21 19 PM" src="https://github.com/user-attachments/assets/79b50dee-d515-4db4-9f84-4a03b540e11d" />

