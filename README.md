# Swasthya-Queue
Teleconsultation Queue &amp; Triage Management System for Rural Clinics

DEPLOYMENT LINK : https://swasthya-queue.netlify.app/

## Doctor Dashboard Login Credentials

| Field      | Details     |
|------------|-------------|
| **Portal** | Doctor Dashboard (Secure Login) |
| **Username** | `Doctor` |
| **Password** | `Doctor123` |

# स्वास्थ्य Queue — Swasthya Queue

> **AI-powered teleconsultation & emergency triage platform for rural Primary Health Centres**

Swasthya Queue is a multi-channel patient triage, queue management, and emergency referral system designed for rural PHCs (Primary Health Centres) in India. It enables instant patient assessment via Web, SMS, or USSD — requiring no smartphone or internet connection.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Access Channels](#access-channels)
- [Triage Scoring Algorithm](#triage-scoring-algorithm)
- [Portals & Roles](#portals--roles)
- [Referral & Dispatch System](#referral--dispatch-system)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Demo Credentials](#demo-credentials)
- [Project Structure](#project-structure)

---

## Overview

Rural PHCs in India often face challenges with patient overflow, lack of structured triage, and delayed referrals for critical cases. Swasthya Queue solves this by:

- Triaging patients automatically in under 1 second using a START-inspired scoring algorithm
- Supporting registration via web kiosk, USSD `*599#`, or WhatsApp/SMS chatbot
- Giving doctors a pre-built clinical brief before every teleconsultation
- Enabling one-tap emergency referrals — bed booking, ambulance dispatch, and referral notice all sent simultaneously

---

## Features

### Patient Registration
- Multi-step web form with language selection (English, Hindi, Tamil, Telugu, Kannada)
- Symptom selector with visual icons
- Severity scale (1–5, Mild to Critical)
- Duration of symptoms input
- Generates a colour-coded queue token with estimated wait time

### Automated Triage
- Scores patients based on symptom criticality, severity rating, and age
- Applies 1.5× multiplier for patients above 60 or below 5 years
- Assigns priority: 🔴 RED (Critical), 🟠 ORANGE (Moderate), 🟢 GREEN (Routine)
- Queue auto-reorders in real time whenever a new patient registers

### Doctor Dashboard (Secured)
- Live patient queue sorted by triage score
- Expandable patient cards with vitals, symptom list, and AI-generated 3-sentence clinical brief
- One-click teleconsultation via secure video call
- In-app messaging to communicate directly with the patient
- One-button referral escalation to Command Center

### Command Center (Referral & Dispatch)
- Live alert bar for critical patients requiring immediate referral
- Nearest hospitals ranked by distance, bed availability, and specialist match
- Real-time ICU and general bed count display
- 108 ambulance network integration with live unit locations and ETAs
- OpenStreetMap live route map with animated ambulance marker
- Auto-generated referral notice (editable) sent via SMS + NIC eReferral portal
- Referral status timeline — both doctor and hospital see the same state

### Access Channels
| Channel | Requirements | Best For |
|---|---|---|
| Web / App | Smartphone or shared clinic tablet | Clinic kiosk, ASHA/ANM workers |
| USSD `*599#` | Any 2G keypad phone, no internet | Remote villages, no-data zones |
| WhatsApp / SMS | Basic phone with SMS capability | Async, literate patients |

---

## Triage Scoring Algorithm

Inspired by the START (Simple Triage and Rapid Treatment) protocol:

| Factor | Score |
|---|---|
| Chest pain / Breathlessness / Seizure | +4 each |
| High fever / Severe headache / Injury | +2 each |
| Vomiting / Abdominal pain / Cold | +1 each |
| Patient-reported severity | +1 to +5 |
| Age > 60 or < 5 years | × 1.5 multiplier |

**Priority bands:**

| Score | Priority | Action |
|---|---|---|
| ≥ 8 | 🔴 RED — Critical | See immediately |
| 4–7 | 🟠 ORANGE — Moderate | Within 30 minutes |
| 1–3 | 🟢 GREEN — Mild | Normal queue |

---

## Portals & Roles

### Clinic Operations (Public)
No login required. Provides access to:
- Patient Registration (Web, USSD, SMS flows)
- Command Center / Referral Dashboard

### Doctor Dashboard (Secured)
Login required. Provides access to:
- Live priority queue with expandable patient briefs
- Video teleconsultation
- In-app patient messaging
- Referral escalation

---

## Referral & Dispatch System

When a critical patient needs transfer, the Command Center enables:

1. **Hospital selection** — Nearest hospitals ranked by distance + bed availability + specialist presence
2. **Bed reservation** — One-click ICU or general bed booking with real-time confirmation
3. **Ambulance dispatch** — 108 network integration; nearest available unit auto-suggested with live ETA
4. **Referral notice** — Auto-generated clinical summary sent via SMS + NIC eReferral portal
5. **Live timeline** — Status progression visible to both referring PHC and receiving hospital

The entire referral chain — bed + ambulance + notice — can be triggered in under 10 seconds.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript |
| Maps | Leaflet.js + OpenStreetMap tiles |
| Translations | Google Translate Widget API |
| USSD simulation | Custom multi-step state machine |
| SMS/WhatsApp sim | Scripted conversational flow (Dialogflow/Gemini in production) |
| Backend (mock) | In-browser `APIService` object simulating network latency and ML inference |
| Fonts | Inter (Google Fonts) |

**Production integrations planned:**
- Telephony: Plivo / Twilio USSD Bridge
- NLP: Dialogflow / Google Gemini
- Referral: NIC eReferral portal
- Ambulance: 108 Ambulance Network API (State Health Dept.)
- Video: eSanjeevani / WebRTC E2E

---

## Getting Started

Swasthya Queue is a single-file HTML application. No build step or server required.

```bash
# Clone or download the project
git clone https://github.com/your-org/swasthya-queue.git

# Open in browser
open index.html
```

Or simply open `index.html` directly in any modern browser.

> **Note:** The map panel (`#panel-dispatch`) requires an internet connection to load OpenStreetMap tiles. All other panels work fully offline.

---

## Demo Credentials

| Role | Username | Password |
|---|---|---|
| Doctor | `doctor` | `doctor123` |

Use these to access the secured **Doctor Dashboard** portal.

---

## Project Structure

```
swasthya-queue/
│
├── index.html              # Entire application (single-file)
│
│   Inline sections:
│   ├── Hero & Navigation
│   ├── #panel-landing      — Portal selector (Clinic / Doctor)
│   ├── #panel-patient      — Patient registration (Web / USSD / SMS flows)
│   ├── #panel-doctor       — Doctor dashboard with live queue
│   ├── #panel-dispatch     — Command Center: referral, ambulance, hospital
│   └── #panel-about        — How it works: flow steps, algorithm, channels
│
│   Modals:
│   ├── #auth-modal         — Doctor login
│   ├── #video-call-modal   — Teleconsultation overlay
│   ├── #message-modal      — In-app patient messaging
│   └── #sys-modal          — Dispatch confirmation notification
│
└── (no external dependencies beyond CDN links)
```

---

## Roadmap / Planned Enhancements

- [ ] Integration with real 108 ambulance dispatch API
- [ ] eSanjeevani teleconsultation deep-link for video calls
- [ ] Offline PWA support with service workers for low-connectivity zones
- [ ] ABHA (Ayushman Bharat Health Account) ID lookup at registration
- [ ] Aadhaar-based patient record linking
- [ ] Push notifications via Firebase for queue status updates
- [ ] Analytics dashboard with daily/weekly patient trends
- [ ] Admin panel for PHC management and doctor scheduling

---

## License

This project is intended for public health use. Contact the maintainers for licensing terms before commercial deployment.

---

*Built to bridge the last mile in rural healthcare access.*
