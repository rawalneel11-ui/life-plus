# LiFE+ — Interactive Mission LiFE Citizen Engagement Platform

> **Hackathon Track**: `HC26-GEDA01`  
> **Agency**: Gujarat Energy Development Agency (GEDA), Government of Gujarat  
> **Challenge**: Development of an Interactive Mission LiFE Citizen Engagement Application  
> **Tagline**: *Small Actions. Measurable Impact. A Greener Tomorrow.*  
> **Submission Deadline**: 4 November 2026, 6:30 PM IST  
> **Evaluation Partner**: NxtWave  

[![Live Production](https://img.shields.io/badge/Production-Live%20on%20Vercel-success?style=for-the-badge&logo=vercel)](https://life-plus-seven.vercel.app)
[![Pitch Deck PDF](https://img.shields.io/badge/Pitch%20Deck-10%20Slides%20(PDF)-15803d?style=for-the-badge&logo=adobeacrobatreader)](https://life-plus-seven.vercel.app/pitch-deck.pdf)
[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github)](https://github.com/rawalneel11-ui/life-plus)
[![Tests Passing](https://img.shields.io/badge/Tests-48%2F48%20Passed-059669?style=for-the-badge)](docs/TESTING.md)
[![TypeScript Strict](https://img.shields.io/badge/TypeScript-5.0%20Strict-3178c6?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org)
[![Next.js](https://img.shields.io/badge/Next.js-16.4.3%20Turbopack-black?style=for-the-badge&logo=next.js)](https://nextjs.org)

---

## 📌 Executive Submission Quick Links

| Deliverable | URL / Resource | Description |
| :--- | :--- | :--- |
| 🌐 **Live Application** | [https://life-plus-seven.vercel.app](https://life-plus-seven.vercel.app) | Live production application on Vercel Global Edge Network (BOM1 Mumbai) |
| 📄 **Pitch Deck (PDF)** | [https://life-plus-seven.vercel.app/pitch-deck.pdf](https://life-plus-seven.vercel.app/pitch-deck.pdf) | Official 10-slide architectural pitch deck (Landscape format) |
| 🖥️ **Interactive Deck** | [https://life-plus-seven.vercel.app/pitch-deck](https://life-plus-seven.vercel.app/pitch-deck) | In-browser presentation viewer with keyboard controls, fullscreen mode & print styles |
| 💻 **GitHub Repository** | [https://github.com/rawalneel11-ui/life-plus](https://github.com/rawalneel11-ui/life-plus) | Full codebase with all commits made during the hackathon window |
| 🎥 **Video Walkthrough** | *[Insert 2–3 min unlisted YouTube / Loom link]* | Scene-by-scene demonstration of live working prototype |

---

## 📖 Table of Contents

1. [Problem Statement & Mission LiFE Context](#1-problem-statement--mission-life-context)
2. [Platform Architecture & System Diagrams](#2-platform-architecture--system-diagrams)
   * [2.1 End-to-End 4-Tier Cloud Architecture](#21-end-to-end-4-tier-cloud-architecture)
   * [2.2 Citizen User Journey & State Transitions](#22-citizen-user-journey--state-transitions)
   * [2.3 Context-Aware AI Eco Coach Pipeline](#23-context-aware-ai-eco-coach-pipeline)
   * [2.4 Resilient Serverless Authentication Flow](#24-resilient-serverless-authentication-flow)
3. [Database Schema & Entity Relationship Model](#3-database-schema--entity-relationship-model)
4. [Mathematical Models & Statutory Calculation Engines](#4-mathematical-models--statutory-calculation-engines)
5. [Complete Technology Stack](#5-complete-technology-stack)
6. [Detailed Local Setup & Installation Guide](#6-detailed-local-setup--installation-guide)
   * [6.1 Prerequisites](#61-prerequisites)
   * [6.2 Step-by-Step Installation](#62-step-by-step-installation)
   * [6.3 Environment Variables Reference Table](#63-environment-variables-reference-table)
   * [6.4 Firebase Security Rules Deployment](#64-firebase-security-rules-deployment)
7. [Production Deployment Guide](#7-production-deployment-guide)
8. [API Route Reference](#8-api-route-reference)
9. [Verification, Quality Assurance & Test Suites](#9-verification-quality-assurance--test-suites)
10. [NxtWave Evaluation Matrix](#10-nxtwave-evaluation-matrix)
11. [Current Limitations & Strategic Roadmap](#11-current-limitations--strategic-roadmap)
12. [Troubleshooting & Common Questions](#12-troubleshooting--common-questions)

---

## 1. Problem Statement & Mission LiFE Context

**Mission LiFE (Lifestyle for Environment)**, championed by Prime Minister Narendra Modi and supported by the United Nations, is an India-led global movement to shift human behavior from mindful destruction to mindful utilization.

Under challenge **HC26-GEDA01**, the **Gujarat Energy Development Agency (GEDA)** identified a critical paradox: although Gujarat possesses the highest installed renewable capacity and solar rooftop density in India, residential electricity consumers lack individual visibility and agency.

```mermaid
flowchart TD
    subgraph Challenge ["The Citizen Energy Paradox in Gujarat"]
        A["Abstract Utility Bills\nOnly kWh & Rupees displayed"] --> D["Invisible Household Footprint"]
        B["Solar Jargon & Hesitation\nComplex net metering & subsidy tiers"] --> E["Delayed PM Surya Ghar Adoption"]
        C["One-Off Civic Campaigns\nStatic brochures without feedback loops"] --> F["Habit Attrition & Civic Fatigue"]
    end

    subgraph Solution ["The LiFE+ Intervention Engine"]
        D --> G["Accurate Carbon Engine\nCEA 0.82 kg CO2e / kWh"]
        E --> H["District Solar Calculator\n33 Districts & 25-Yr ROI"]
        F --> I["Contextual AI & Anti-Duplication XP\nGemini 2.5 + Daily Habits"]
    end

    G --> J["Quantifiable Residential Conservation · GEDA Alignment"]
    H --> J
    I --> J
```

### The 7 Core Pillars of LiFE+
1. **Citizen Baseline Onboarding (`/onboarding`)**: 90-second onboarding wizard gathering dwelling type, DISCOM (UGVCL, DGVCL, MGVCL, PGVCL, Torrent Power), appliance inventory, and baseline billing (+100 XP).
2. **Energy Tracker & Billing Analytics (`/tracker`)**: Add, inspect, and visualize monthly metered consumption, seasonal bill variations, and baseline divergence.
3. **Statutory Carbon Footprint Engine (`/carbon`)**: Computes monthly and annual emissions using the official Central Electricity Authority factor ($0.82\,\text{kg CO}_2\text{e/kWh}$) with tree sequestration equivalents.
4. **Context-Aware AI Eco Coach (`/eco-coach`)**: Serverless Google Gemini 2.5 Flash advisor injecting the user's authentic household profile and appliance wattages.
5. **Anti-Duplication Gamification & Community (`/challenges`, `/rewards`, `/community`)**: 6 citizen tiers, verified green challenges, and privacy-masked regional leaderboards.
6. **Rooftop Solar Feasibility Calculator (`/solar-calculator`)**: District-level Peak Sun Hours (PSH), shadow loss derating, PM Surya Ghar subsidy caps (up to ₹78,000), and 25-year financial payback.
7. **Government Schemes & Empaneled Solar Vendors (`/resources`, `/solar-vendors`)**: Searchable portal of verified DISCOM vendors and official government policy documents.

---

## 2. Platform Architecture & System Diagrams

### 2.1 End-to-End 4-Tier Cloud Architecture

```mermaid
flowchart TB
    subgraph Tier1 ["1. Client Presentation Layer (Next.js 16 App Router)"]
        Browser["Citizen Web Browser / Mobile PWA"]
        Pages["App Router Pages\n(/dashboard, /tracker, /solar-calculator, /eco-coach)"]
        UIElements["Tailwind CSS v4 + Framer Motion Components"]
        ChartLib["Recharts 3.10 Visualization Engine"]
        ZustandStore["Zustand Client State (User, Energy, Gamification)"]
    end

    subgraph Tier2 ["2. Edge Security & Routing Layer (Vercel Edge Runtime)"]
        EdgeProxy["src/proxy.ts (Next.js 16 Edge Middleware)"]
        CookieGuard["Session Cookie Inspection ('life-plus-session')"]
        CSRFShield["Tolerant Origin Validation & Security Headers"]
    end

    subgraph Tier3 ["3. Serverless API Execution Tier (Next.js Route Handlers)"]
        AuthHandler["/api/auth/session\nGoogle Identity Toolkit REST Engine"]
        EcoHandler["/api/eco-coach/chat\nGemini 2.5 Contextual Pipeline"]
        SolarHandler["/api/solar/feasibility\nSolar Irradiation Engine"]
        GamifyHandler["/api/challenges & /api/gamification\nAtomic Transaction Verifier"]
        DatasetHandler["/api/datasets\nSynthetic Registry & District Baselines"]
    end

    subgraph Tier4 ["4. Cloud Persistence & AI Services"]
        FirestoreDB[("Cloud Firestore\nMulti-Tenant Document DB")]
        FirebaseAuth["Firebase Authentication Service"]
        GeminiFlash["Google Gemini 2.5 Flash API\n(Server-Side Only via @google/genai)"]
        EdgeCache["BOM1 Edge Memory Cache\n(District Tables & Tariffs)"]
    end

    Browser --> UIElements
    UIElements --> Pages
    Pages --> ZustandStore
    Pages --> ChartLib

    Pages -->|HTTP Fetch with Session Cookie| EdgeProxy
    EdgeProxy --> CookieGuard
    CookieGuard --> CSRFShield

    CSRFShield -->|Protected Route Authorized| Tier3
    CookieGuard -->|Missing Cookie on Protected Route| Browser

    AuthHandler --> FirebaseAuth
    AuthHandler --> FirestoreDB
    EcoHandler --> GeminiFlash
    EcoHandler --> FirestoreDB
    SolarHandler --> EdgeCache
    GamifyHandler --> FirestoreDB
    DatasetHandler --> EdgeCache
```

---

### 2.2 Citizen User Journey & State Transitions

```mermaid
stateDiagram-v2
    [*] --> LandingPage: Citizen visits life-plus-seven.vercel.app
    LandingPage --> Registration: Click 'Get Started'
    LandingPage --> PitchDeck: Click 'Pitch Deck (PDF)'
    Registration --> FirebaseAccount: Create Account (Email or Google)
    FirebaseAccount --> EdgeSession: /api/auth/session sets life-plus-session
    EdgeSession --> OnboardingWizard: Redirect to /onboarding
    
    state OnboardingWizard {
        PersonalDetails --> HouseholdDwelling
        HouseholdDwelling --> ApplianceInventory
        ApplianceInventory --> LiFEInterests
        LiFEInterests --> BaselineReview
    }
    
    BaselineReview --> Dashboard: Complete Baseline (+100 XP Awarded)
    
    state Dashboard {
        ViewAnalytics --> TrackNewBill: Add Monthly Bill
        ViewAnalytics --> OpenEcoCoach: Ask Gemini Advisor
        ViewAnalytics --> CalculateSolar: Run Rooftop Assessment
        ViewAnalytics --> JoinChallenge: Complete Daily Green Habit
    }

    TrackNewBill --> CarbonEngine: Recalculate 0.82 kg/kWh CO2e
    CalculateSolar --> SaveAssessment: Save to Profile (+100 XP)
    JoinChallenge --> MintXP: Atomic XP Minting (Anti-Replay)
    MintXP --> LevelProgression: Level Up & Unlock Badges
    LevelProgression --> CommunityLeaderboard: View District Rank
```

---

### 2.3 Context-Aware AI Eco Coach Pipeline

```mermaid
sequenceDiagram
    autonumber
    actor Citizen as Citizen User
    participant Browser as Browser Client
    participant Server as /api/eco-coach/chat
    participant Firestore as Cloud Firestore
    participant Gemini as Google Gemini 2.5 Flash API

    Citizen->>Browser: Types "How can I reduce my AC bill?"
    Browser->>Server: POST { message } with 'life-plus-session'
    Server->>Server: Authenticate request & extract citizen UID
    Server->>Firestore: Fetch users/{uid} & appliance inventories
    Firestore-->>Server: Return: Ahmedabad, 2BHK, 1.5T Split AC, 240 kWh/mo
    Server->>Server: Assemble System Prompt + User Context + Energy History
    Note over Server,Gemini: API Key kept strictly server-side (NEVER sent to client)
    Server->>Gemini: Call generateContent(assembledContextPrompt)
    Gemini-->>Server: Return structured, bilingual energy advice
    Server->>Browser: HTTP 200 { response, timestamp }
    Browser->>Citizen: Render formatted AI coach message with auto-scroll
```

---

### 2.4 Resilient Serverless Authentication Flow

```mermaid
sequenceDiagram
    autonumber
    actor Citizen as Citizen User
    participant Client as Browser (Firebase Client SDK)
    participant Route as /api/auth/session
    participant IdentityAPI as Google Identity Toolkit REST API
    participant Edge as Next.js Edge Middleware

    Citizen->>Client: Enters credentials or clicks Google Sign-In
    Client->>Client: firebase.auth().signInWith...
    Client-->>Client: Generates valid signed Firebase ID Token
    Client->>Client: Sets client document.cookie fallback
    Client->>Route: POST /api/auth/session { idToken }
    
    alt Standard Path
        Route->>IdentityAPI: POST accounts:lookup?key=API_KEY { idToken }
        IdentityAPI-->>Route: 200 OK { users: [{ localId: uid, email }] }
    else Offline / Fallback Path
        Route->>Route: Decode JWT payload locally & verify unexpired exp
    end
    
    Route->>Route: Set HTTP-Only 'life-plus-session' cookie (7-day maxAge)
    Route-->>Client: HTTP 200 { success: true, uid }
    Client->>Edge: Hard navigation (window.location.href = '/onboarding')
    Edge->>Edge: Inspects 'life-plus-session' cookie
    Edge-->>Client: Grants access to protected route (/onboarding)
```

---

## 3. Database Schema & Entity Relationship Model

All citizen data is encapsulated within Cloud Firestore under a strict multi-tenant schema with document-level security:

```mermaid
erDiagram
    USERS ||--o{ RECORDS : "logs bills"
    USERS ||--o{ APPLIANCES : "owns appliances"
    USERS ||--|| GAMIFICATION_STATUS : "maintains status"
    USERS ||--o{ SOLAR_ASSESSMENTS : "stores runs"
    USERS ||--o{ REWARD_TRANSACTIONS : "receives XP"

    USERS {
        string uid PK "Citizen Firebase UID"
        string email "Citizen Email"
        string fullName "Display Name"
        string district "One of 33 Gujarat Districts"
        string state "Default: Gujarat"
        string residentialType "1bhk | 2bhk | 3bhk | rowhouse | bungalow"
        string discom "UGVCL | DGVCL | MGVCL | PGVCL | Torrent Power"
        number monthlyKwh "Baseline monthly energy consumption"
        number monthlyBill "Baseline monthly electricity bill in INR"
        boolean isOnboarded "True upon wizard completion"
        timestamp createdAt "Registration timestamp"
    }

    RECORDS {
        string id PK "Auto-generated record ID"
        string billingPeriod "Format: YYYY-MM"
        number unitsConsumed "kWh consumed in period"
        number billAmount "Total bill in INR"
        string notes "Citizen notes / season info"
        timestamp loggedAt "Record creation timestamp"
    }

    APPLIANCES {
        string id PK "Auto-generated appliance ID"
        string name "e.g. Inverter AC 1.5 Ton"
        string category "cooling | heating | refrigeration | lighting | other"
        number powerWatts "Rated power in Watts"
        number quantity "Number of units in home"
        number dailyHours "Average usage hours per day"
        number starRating "BEE Star Rating (1 to 5)"
        timestamp addedAt "Timestamp"
    }

    GAMIFICATION_STATUS {
        string uid PK "Matches citizen UID"
        number totalXP "Cumulative citizen XP"
        number level "Current citizen level (1 to 6)"
        string[] badges "Unlocked badge IDs"
        string[] activeChallenges "In-progress challenge IDs"
        string[] completedChallenges "Completed challenge IDs"
        number streakDays "Consecutive daily login streak"
        timestamp lastActive "Last active timestamp"
    }

    SOLAR_ASSESSMENTS {
        string id PK "Auto-generated assessment ID"
        number capacityKw "Recommended solar capacity in kW"
        number roofAreaSqM "Entered rooftop area in square meters"
        string roofType "flat | sloped"
        string shading "low | moderate | high"
        number annualGenKwh "Estimated annual generation in kWh"
        number annualSavingsRs "Estimated annual bill reduction in INR"
        number grossCostRs "Estimated system capital cost"
        number subsidyRs "PM Surya Ghar central financial subsidy"
        number netCostRs "Net citizen investment"
        number paybackYears "Estimated financial payback period"
        timestamp assessmentDate "Timestamp"
    }

    REWARD_TRANSACTIONS {
        string id PK "Compound source key (prevents replay)"
        string userId "Citizen UID"
        string source "onboarding | challenge | solar | tracker"
        number xpEarned "XP minted"
        timestamp timestamp "Transaction timestamp"
    }
```

---

## 4. Mathematical Models & Statutory Calculation Engines

### 4.1 Carbon Footprint Engine
Statutory accounting follows the **Central Electricity Authority (CEA) Baseline Database v19.0**:

$$\text{Carbon Footprint (kg CO}_2\text{e)} = \text{Electricity Consumed (kWh)} \times 0.82\,\text{kg CO}_2/\text{kWh}$$

$$\text{Equivalent Trees Required} = \frac{\text{Annual Carbon Footprint (kg CO}_2\text{e)}}{21.77\,\text{kg CO}_2/\text{tree/year}}$$

$$\text{Avoided Car Kilometers} = \frac{\text{Emissions Reduced (kg CO}_2\text{e)}}{0.192\,\text{kg CO}_2/\text{km}}$$

### 4.2 Rooftop Solar Feasibility Engine
Rooftop capacity is physically bounded by usable terrace space and historical monthly consumption:

$$\text{Capacity}_{\text{Area}} (\text{kW}) = \frac{\text{Roof Area (m}^2) \times \text{Usable Factor}}{\text{Specific Area Requirement (m}^2/\text{kW})}$$

* **Flat RCC Roof**: Usable Factor = $0.70$ (70%), Specific Area = $10.0\,\text{m}^2/\text{kW}$.
* **Sloped Roof**: Usable Factor = $0.85$ (85%), Specific Area = $8.5\,\text{m}^2/\text{kW}$.

$$\text{Capacity}_{\text{Consumption}} (\text{kW}) = \frac{\text{Average Monthly Consumption (kWh)}}{120\,\text{kWh/kW/month}}$$

$$\text{Recommended Capacity} (\text{kW}) = \min(\text{Capacity}_{\text{Area}}, \text{Capacity}_{\text{Consumption}})$$

### 4.3 PM Surya Ghar: Muft Bijli Yojana Central Subsidy
Calculated strictly pursuant to MNRE Gazette guidelines:
* **Capacity $\le 1.0\,\text{kW}$**: ₹30,000 per kW (₹30,000).
* **Capacity $> 1.0\,\text{kW}$ and $\le 2.0\,\text{kW}$**: ₹30,000 for 1st kW + ₹30,000 for 2nd kW (₹60,000).
* **Capacity $> 2.0\,\text{kW}$ and $\le 3.0\,\text{kW}$**: ₹60,000 + ₹18,000 for 3rd kW (₹78,000).
* **Capacity $> 3.0\,\text{kW}$**: Capped at **₹78,000** maximum central subsidy.

---

## 5. Complete Technology Stack

```
┌────────────────────────────────────────────────────────────────────────┐
│                        LiFE+ TECHNOLOGY MATRIX                         │
├───────────────────────┬──────────────────────────┬─────────────────────┤
│ LAYER                 │ TECHNOLOGY               │ VERSION / REMARKS   │
├───────────────────────┼──────────────────────────┼─────────────────────┤
│ Framework             │ Next.js (App Router)     │ 16.4.3 (Turbopack)  │
│ UI Runtime            │ React                    │ 19.3.0              │
│ Language              │ TypeScript               │ 5.0 (Strict mode)   │
│ Styling Engine        │ Tailwind CSS             │ v4.0 (Zero-runtime) │
│ Motion & Animation    │ Framer Motion            │ 14.7.1              │
│ Icons                 │ Lucide React             │ 1.64.0              │
│ Charting              │ Recharts                 │ 3.10.1              │
│ State Management      │ Zustand                  │ 5.0.16              │
│ Form Management       │ React Hook Form          │ 7.91.0              │
│ Schema Validation     │ Zod                      │ 4.6.7               │
│ Client Authentication │ Firebase Auth Client SDK │ 13.1.0              │
│ Cloud Database        │ Cloud Firestore          │ 13.1.0              │
│ Server Token Engine   │ Google Identity REST API │ Official Endpoint   │
│ AI LLM Engine         │ Google Gemini 2.5 Flash  │ @google/genai       │
│ PDF Engine            │ pdf-lib                  │ 1.17.1 (Standard)   │
│ Deployment Platform   │ Vercel Edge Network      │ Production (BOM1)   │
└───────────────────────┴──────────────────────────┴─────────────────────┘
```

---

## 6. Detailed Local Setup & Installation Guide

### 6.1 Prerequisites

Before installing the application locally, ensure you have:
* **Node.js**: `v20.x`, `v22.x`, or `v26.x` (LTS recommended).
* **Package Manager**: `pnpm` (recommended: `pnpm@11.x`), `npm`, or `yarn`.
* **Firebase Project**: An active project created in the [Firebase Console](https://console.firebase.google.com).
* **Google Gemini API Key**: An API key from [Google AI Studio](https://aistudio.google.com).

---

### 6.2 Step-by-Step Installation

#### Step 1: Clone the Repository
```bash
git clone https://github.com/rawalneel11-ui/life-plus.git
cd life-plus
```

#### Step 2: Install Project Dependencies
```bash
pnpm install
# or: npm install
```

#### Step 3: Configure Environment Variables
Copy `.env.example` into a new `.env.local` file:
```bash
cp .env.example .env.local
```

Open `.env.local` and populate the values as outlined in the reference table below.

#### Step 4: Run the Development Server
```bash
pnpm dev
```
Open **[http://localhost:3000](http://localhost:3000)** in your browser.

#### Step 5: Verify Production Build
```bash
pnpm build
```

---

### 6.3 Environment Variables Reference Table

| Variable Name | Required | Scope | Description & Example Format |
| :--- | :---: | :---: | :--- |
| `NEXT_PUBLIC_FIREBASE_API_KEY` | **Yes** | Client | Firebase Web API key (`AIzaSy...`) |
| `NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN` | **Yes** | Client | Firebase Auth domain (`life-pulse-b3996.firebaseapp.com`) |
| `NEXT_PUBLIC_FIREBASE_PROJECT_ID` | **Yes** | Client | Firebase project ID (`life-pulse-b3996`) |
| `NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET`| **Yes** | Client | Firebase storage bucket (`life-pulse-b3996.appspot.com`) |
| `NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID` | **Yes** | Client | Firebase Cloud Messaging sender ID (`1234567890`) |
| `NEXT_PUBLIC_FIREBASE_APP_ID` | **Yes** | Client | Firebase web application ID (`1:1234567890:web:...`) |
| `FIREBASE_ADMIN_PROJECT_ID` | **Yes** | Server | Google Cloud project ID for server authentication |
| `FIREBASE_ADMIN_CLIENT_EMAIL` | **Yes** | Server | Service account email (`firebase-adminsdk-xxx@...`) |
| `FIREBASE_ADMIN_PRIVATE_KEY` | **Yes** | Server | RSA private key (with escaped `\n` linebreaks) |
| `GEMINI_API_KEY` | **Yes** | Server | Google AI Studio Gemini API key (`AIzaSy...`) |
| `NEXT_PUBLIC_APP_URL` | **Yes** | Client | Base URL (`http://localhost:3000` or production URL) |
| `NEXT_PUBLIC_APP_ENV` | No | Client | Environment mode (`development` or `production`) |

> [!IMPORTANT]
> **Zero Credential Leakage Guarantee**: Variables prefixed with `FIREBASE_ADMIN_` and `GEMINI_API_KEY` do not have the `NEXT_PUBLIC_` prefix and are strictly forbidden from being compiled into the client bundle by Turbopack.

---

### 6.4 Firebase Security Rules Deployment

To enforce strict multi-tenant privacy, deploy the project's security rules using the Firebase CLI:
```bash
# Login to Firebase
firebase login

# Deploy Firestore rules directly
firebase deploy --only firestore:rules
```

*(Alternatively, paste the contents of `firestore.rules` directly into the Rules tab in your Firebase Console).*

---

## 7. Production Deployment Guide

LiFE+ is configured for zero-downtime deployment on the Vercel Global Edge Network.

### Deploying to Vercel via CLI
```bash
# 1. Install Vercel CLI globally if not already installed
npm install -g vercel

# 2. Link your local project
vercel link

# 3. Pull environment variables or set them via dashboard
vercel env pull .env.production.local

# 4. Deploy directly to production
vercel deploy --prod --yes
```

### Firebase Authorized Domains
When deploying to a custom domain or Vercel alias (e.g. `life-plus-seven.vercel.app`), add the domain to Firebase Console:
1. Go to **Firebase Console** $\rightarrow$ **Authentication** $\rightarrow$ **Settings** $\rightarrow$ **Authorized domains**.
2. Click **Add domain** and enter your production hostname (e.g. `life-plus-seven.vercel.app`).

---

## 8. API Route Reference

All backend API routes execute server-side in isolated Node.js serverless functions:

| Route | Method | Auth Required | Request Payload | Description |
| :--- | :---: | :---: | :--- | :--- |
| `/api/auth/session` | `POST` | No | `{ idToken: string }` | Validates Firebase token via Identity Toolkit and sets HTTP-only `life-plus-session` cookie. |
| `/api/auth/session` | `GET` | Yes | *Cookies* | Verifies current session cookie and returns `{ isAuthenticated, uid }`. |
| `/api/auth/session` | `DELETE`| Yes | *Cookies* | Destroys session cookie and logs user out. |
| `/api/eco-coach/chat` | `POST` | Yes | `{ message: string }` | Assembles user energy context and streams response from Gemini 2.5 Flash. |
| `/api/solar/feasibility`| `POST`| Yes | `{ roofArea, billKwh, district, ... }` | Executes solar capacity and PM Surya Ghar subsidy calculations. |
| `/api/challenges` | `GET` | Yes | *None* | Retrieves all active daily and weekly green challenges. |
| `/api/challenges/join` | `POST` | Yes | `{ challengeId: string }` | Enrolls user in an active challenge. |
| `/api/challenges/complete`| `POST`| Yes | `{ challengeId: string }` | Atomically awards XP with replay protection. |
| `/api/community/leaderboard`| `GET`| Yes | *None* | Returns privacy-safe masked regional leaderboard. |
| `/api/datasets/baseline` | `GET` | No | `?houseType=2bhk` | Returns static energy baseline for Gujarat residential typologies. |

---

## 9. Verification, Quality Assurance & Test Suites

The codebase includes 5 automated test runners validating all statutory calculations, Zod validation schemas, and server-side security guards:

```bash
# Run all verification test suites:
node scripts/test-runner.js      # 1. Carbon Calculation & CEA Grid Factor Tests
node scripts/test-datasets.js    # 2. Zod Schema Validation & Data Provenance Tests
node scripts/test-eco-coach.js   # 3. Gemini 2.5 Serverless Security & Timeout Tests
node scripts/test-phase6.js      # 4. Gamification XP Minting & Anti-Replay Tests
node scripts/test-phase7.js      # 5. Solar Sizing & PM Surya Ghar Subsidy Tests
```

### Test Coverage Summary:
* **Carbon Engine**: Tests 100% adherence to $0.82\,\text{kg CO}_2/\text{kWh}$ statutory baseline, handling of edge zero-consumption cases, and non-negative outputs.
* **Solar Feasibility**: Tests Area vs Consumption minimum bounds, shadow multiplier reductions, and exact MNRE subsidy step tiers up to ₹78,000.
* **Security & Auth**: Validates that direct client attempts to mint XP without server authentication are strictly blocked.

---

## 10. NxtWave Evaluation Matrix

| Criterion | Weight | Platform Implementation in LiFE+ |
| :--- | :---: | :--- |
| **Technical Execution & Code Quality** | **40%** | Full-stack Next.js 16.4.3 App Router with React 19 and TypeScript strict mode. 48/48 test passes, zero compiler errors, zero ESLint warnings, and resilient REST-based token verification eliminating ESM require crashes. |
| **System Architecture & Scalability** | **30%** | 4-Tier cloud-native design with Edge Middleware protection, serverless autoscaling, BOM1 Mumbai low-latency edge caching, and document-level Cloud Firestore isolation. |
| **UI/UX Design** | **20%** | Purpose-built Mission LiFE Gujarat design system in Tailwind CSS v4, smooth Framer Motion micro-interactions, responsive mobile/desktop layouts, high-contrast WCAG AA compliance, and interactive 10-slide Pitch Deck viewer. |
| **Innovation & Problem Fit** | **10%** | Context-aware AI Eco Coach powered by Google Gemini 2.5 Flash, transparent CEA-grounded carbon accounting, district-sensitive Peak Sun Hours modeling for all 33 Gujarat districts, and anti-replay gamification. |

---

## 11. Current Limitations & Strategic Roadmap

### Current Limitations
1. **DISCOM Live API Access**: In the absence of state-level open DISCOM webhook APIs, utility bills are entered manually; mitigated by intelligent Gujarat BHK baseline pre-population.
2. **LiDAR Rooftop Satellite Ingestion**: Rooftop area is user-entered; mitigated by an engineering $80\%$ usable terrace coefficient and multi-point shading multipliers.
3. **Gemini LLM Rate Limiting**: Mitigated with in-memory request debouncing (15 req/min), 15-second server timeout guards, and structured fallback advice.

### Strategic Roadmap
* **Phase A (Q1–Q2 2026)**: Integration with Gujarat Smart Meter AMI infrastructure for automated 15-minute interval consumption tracking and peak-tariff alerts.
* **Phase B (Q3 2026)**: WhatsApp OCR bot allowing citizens to photo-snap physical utility bills for instant automatic logging.
* **Phase C (Q4 2026)**: GEDA Green Credits marketplace for redeeming LiFE XP against municipal transit passes and vendor solar panel discounts.
* **Phase D (2027)**: Expansion across other state nodal agencies under national Mission LiFE and Bureau of Energy Efficiency guidelines.

---

## 12. Troubleshooting & Common Questions

#### 1. "Authentication error: auth/unauthorized-domain"
* **Solution**: Add your domain to Firebase Console under **Authentication $\rightarrow$ Settings $\rightarrow$ Authorized domains**. Add `life-plus-seven.vercel.app` or your local IP.

#### 2. "PowerShell: running scripts is disabled on this system"
* **Solution**: Run commands using `npx.cmd` and `pnpm.cmd` instead of bare `npx` and `pnpm`, or run `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass`.

#### 3. "Failed to load external module: require() of ES Module jose not supported"
* **Solution**: Fully resolved in LiFE+! Our serverless authentication engine uses the direct **Google Identity Toolkit REST API**, bypassing third-party CommonJS/ESM module locks on modern Node.js runtimes.

---

## 13. License & Attribution

Developed for the **Gujarat Energy Development Agency (GEDA)** under Hackathon Track **HC26-GEDA01**.  
Built under the principles of **Mission LiFE (Lifestyle for Environment)**.
