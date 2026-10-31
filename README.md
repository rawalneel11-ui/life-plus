# LiFE+ — Interactive Mission LiFE Citizen Engagement Platform

> **Hackathon Track**: `HC26-GEDA01`  
> **Agency**: Gujarat Energy Development Agency (GEDA), Government of Gujarat  
> **Challenge**: Development of an Interactive Mission LiFE Citizen Engagement Application  
> **Tagline**: *Small Actions. Measurable Impact. A Greener Tomorrow.*  
> **Submission Deadline**: 4 November 2026, 6:30 PM IST  

[![Live Production](https://img.shields.io/badge/Production-Live%20on%20Vercel-success?style=for-the-badge&logo=vercel)](https://life-plus-seven.vercel.app)
[![Pitch Deck PDF](https://img.shields.io/badge/Pitch%20Deck-10%20Slides%20(PDF)-15803d?style=for-the-badge&logo=adobeacrobatreader)](https://life-plus-seven.vercel.app/pitch-deck.pdf)
[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github)](https://github.com/rawalneel11-ui/life-plus)
[![Tests Passing](https://img.shields.io/badge/Tests-48%2F48%20Passed-059669?style=for-the-badge)](docs/TESTING.md)

---

## 📌 Executive Quick Links

| Resource | Direct Link | Description |
| :--- | :--- | :--- |
| 🌐 **Live Application** | [https://life-plus-seven.vercel.app](https://life-plus-seven.vercel.app) | Live production build running on Vercel Edge with zero-downtime serverless architecture |
| 📄 **Pitch Deck (PDF)** | [https://life-plus-seven.vercel.app/pitch-deck.pdf](https://life-plus-seven.vercel.app/pitch-deck.pdf) | Accessible 10-slide PDF covering Problem, Architecture, Schema, Stack, Scalability, and Roadmap |
| 🖥️ **Interactive Deck** | [https://life-plus-seven.vercel.app/pitch-deck](https://life-plus-seven.vercel.app/pitch-deck) | In-browser slide viewer with keyboard shortcuts, presentation mode, and `@media print` styles |
| 💻 **Source Code** | [https://github.com/rawalneel11-ui/life-plus](https://github.com/rawalneel11-ui/life-plus) | Full public repository with complete commit history throughout the hackathon window |
| 🎥 **Video Walkthrough** | *[Link to 2-3 min unlisted YouTube/Loom demonstration]* | Real, unmocked feature walkthrough across citizen journey |

---

## 1. Problem Statement & Mission LiFE Context

**Mission LiFE (Lifestyle for Environment)**, introduced by Prime Minister Narendra Modi and supported by the United Nations, aims to mobilize over 1 billion citizens globally to embrace circular, sustainable living.

Under **HC26-GEDA01**, the **Gujarat Energy Development Agency (GEDA)** identified critical citizen-level bottlenecks preventing residential households in Gujarat from translating state renewable energy momentum into personal action:

```mermaid
flowchart LR
    A["Abstract Utility Bills\n(kWh & Rupees only)"] --> B["Low Habit\nConsequence Visibility"]
    C["Solar Sizing & Subsidy\nHesitation / Jargon"] --> D["Delayed Rooftop\nAdoption"]
    E["One-Way Awareness\nBrochures / Fatigue"] --> F["Lack of Habit\nReinforcement"]
    
    B --> G["The Citizen Energy Paradox\nHigh State Capacity vs Grassroots Inaction"]
    D --> G
    F --> G
    
    G --> H["LiFE+ Digital Platform\nMeasurable · Contextual · Gamified"]
```

### The LiFE+ Solution
1. **Accurate Household Baseline**: 90-second onboarding capturing dwelling type, DISCOM, appliances, and monthly bills.
2. **Statutory Carbon Engine**: Translates electricity consumption into $\text{kg CO}_2\text{e}$ using Central Electricity Authority (CEA Baseline Database v19.0) grid baseline ($0.82\,\text{kg CO}_2/\text{kWh}$).
3. **Personalized AI Eco Coach**: Serverless Google Gemini 2.5 Flash advisor with real-time injection of the citizen's own appliance and billing records.
4. **Verified Anti-Duplication Gamification**: 6-level XP progression, daily & weekly green challenges, and regional leaderboards.
5. **District-Accurate Solar Calculator**: Irradiance modeling for all 33 Gujarat districts, shadow factor derating, PM Surya Ghar central subsidy tiers, and 25-year ROI forecasts.
6. **Government Resource Hub & Empaneled Vendors**: Verified DISCOM directory and official `.gov.in` sustainability policies.

---

## 2. System Architecture & Data Flow

LiFE+ is engineered on a modern, 4-tier cloud-native serverless architecture deployed on Vercel Global Edge and Google Cloud Firebase infrastructure:

```mermaid
flowchart TD
    subgraph Client ["Client Presentation Tier (Browser / PWA)"]
        UI["Next.js 16.4.3 App Router (Turbopack)"]
        Tailwind["Tailwind CSS v4 + Framer Motion"]
        Recharts["Recharts 3.10 (Energy Trends & Solar Payback)"]
        Zustand["Zustand Client Stores (Energy, User, Gamification)"]
    end

    subgraph Edge ["Edge Tier (Vercel Edge Runtime)"]
        Proxy["src/proxy.ts (Edge Middleware)"]
        OriginCheck["Tolerant Origin & CSRF Shield"]
        SessionCheck["Session Cookie Inspection ('life-plus-session')"]
    end

    subgraph Serverless ["Serverless API Tier (Next.js Route Handlers)"]
        AuthAPI["/api/auth/session\n(Google Identity Toolkit REST)"]
        EcoCoach["/api/eco-coach/chat\n(Gemini 2.5 Server Pipeline)"]
        SolarAPI["/api/solar/feasibility\n(Deterministic Calculation Engine)"]
        GamifyAPI["/api/challenges & /api/gamification\n(Atomic Transaction Verification)"]
    end

    subgraph Storage ["Cloud Persistence & External Services"]
        Firestore["Cloud Firestore (Multi-Tenant Document DB)"]
        GoogleAuth["Firebase Authentication (Client SDK)"]
        GeminiAPI["Google Gemini 2.5 Flash API"]
        LocalCache["Synthetic Baseline & District Irradiance Registry"]
    end

    UI --> Proxy
    Proxy -->|Protected Route Passes| Serverless
    Proxy -->|Unauthenticated| UI

    AuthAPI --> GoogleAuth
    EcoCoach --> GeminiAPI
    EcoCoach --> Firestore
    SolarAPI --> LocalCache
    GamifyAPI --> Firestore
```

---

## 3. Database Schema & Data Models

Cloud Firestore is structured as a privacy-isolated, multi-tenant document hierarchy:

```mermaid
erDiagram
    USERS ||--o{ RECORDS : logs
    USERS ||--o{ APPLIANCES : owns
    USERS ||--|| GAMIFICATION_STATUS : tracks
    USERS ||--o{ SOLAR_ASSESSMENTS : saves
    USERS ||--o{ REWARD_TRANSACTIONS : earns

    USERS {
        string uid PK
        string email
        string fullName
        string district
        string residentialType
        number monthlyKwh
        number monthlyBill
        boolean isOnboarded
        timestamp createdAt
    }

    RECORDS {
        string id PK
        string billingPeriod "YYYY-MM"
        number unitsConsumed
        number billAmount
        string notes
        timestamp loggedAt
    }

    APPLIANCES {
        string id PK
        string name
        string category
        number powerWatts
        number quantity
        number dailyHours
        number starRating
    }

    GAMIFICATION_STATUS {
        number totalXP
        number level
        string[] badges
        string[] activeChallenges
        string[] completedChallenges
        number streakDays
    }

    SOLAR_ASSESSMENTS {
        string id PK
        number capacityKw
        number roofAreaSqM
        number annualGenKwh
        number annualSavingsRs
        number netCostRs
        number paybackYears
        timestamp assessmentDate
    }
```

---

## 4. Complete Technology Stack & Rationale

| Layer | Technology | Version | Architectural Rationale |
| :--- | :--- | :--- | :--- |
| **Framework** | Next.js (App Router) | `16.4.3` | Turbopack sub-second compilation, Server Components, React 19 architecture. |
| **Frontend UI** | React | `19.3.0` | Latest concurrent features, seamless client state transitions. |
| **Styling** | Tailwind CSS v4 | `^4.0` | Zero-runtime CSS engine, lightning-fast rendering, WCAG AA compliance. |
| **Icons & Motion** | Lucide React + Framer Motion | `^1.64` / `^14.7` | High-fidelity micro-interactions and accessible SVG icons. |
| **Data Viz** | Recharts | `^3.10.1` | Native SVG rendering of seasonal consumption and solar ROI payback curves. |
| **Auth Engine** | Firebase Auth + Google Identity REST | `^13.1` | Direct REST verification avoids CommonJS/ESM dependency locks on Node 26. |
| **Database** | Cloud Firestore | `^13.1` | Real-time multi-tenant sync, sub-50ms reads, and offline cache persistence. |
| **AI Engine** | Google Gemini 2.5 Flash | `@google/genai` | Low-latency server-side inference, prompt assembly with citizen context. |
| **Validation** | Zod | `^4.6.7` | Strict runtime payload verification preventing malformed or synthetic data injection. |
| **Hosting** | Vercel Edge Network | Production | Global CDN, Mumbai edge routing (BOM1), automatic SSL, instant rollback capability. |

---

## 5. Scalability, Resilience & Security

### 🚀 Scalability
* **Zero-Provisioning Autoscaling**: Serverless Next.js Route Handlers autoscale on Vercel to handle burst loads during statewide GEDA awareness drives without server management.
* **Edge In-Memory Caching**: Static reference data (33 Gujarat district solar irradiance tables, BHK consumption baselines, and DISCOM tariffs) is cached at Edge points of presence for sub-10ms latency.
* **Firestore Offline Persistence**: Client-side IndexedDB caching allows citizens to simulate solar feasibility and log appliances even in rural areas with intermittent connectivity.

### 🛡️ Security Architecture
* **Strict Server-Only Secrets**: `GEMINI_API_KEY` and Firebase service account credentials are strictly server-bound. Zero private keys are present in client bundles.
* **Multi-Tenant Ownership Enforcement**: Firestore security rules restrict reads and writes via `request.auth.uid == userId`. Users cannot access or modify another citizen's records.
* **Anti-Duplication Atomic Minting**: Gamification rewards use time-bucketed transactional source IDs. Direct client writes to `rewardTransactions` are blocked (`allow write: if false;`), preventing replay attacks.
* **Resilient Authentication Pipeline**: Eliminates external Node.js CJS/ESM module loading conflicts by utilizing direct Google Identity Toolkit REST endpoints with cryptographic JWT payload fallback.

---

## 6. Current Limitations & Future Roadmap

### Current Limitations
1. **DISCOM Live API Integration**: Currently requires manual bill entry or smart defaults due to absence of open DISCOM webhook APIs.
2. **LiDAR Rooftop Satellite Ingestion**: Relies on user-entered terrace area and shading conditions; mitigated by a conservative $80\%$ usable area coefficient.
3. **Gemini API Upstream Throttling**: Guarded with in-memory rate limiting (15 req/min), 15-second server timeouts, and pre-compiled energy advice fallbacks.

### Strategic Roadmap
* **Phase A (Q1–Q2 2026)**: Integration with Gujarat Smart Meter AMI infrastructure for automated 15-minute interval consumption alerts.
* **Phase B (Q3 2026)**: WhatsApp/SMS OCR bot allowing citizens to photo-snap physical utility bills for zero-friction logging.
* **Phase C (Q4 2026)**: GEDA Green Credits marketplace for redeeming LiFE XP against municipal bus passes and solar equipment discounts.
* **Phase D (2027)**: Expansion across other state nodal agencies under national Mission LiFE guidelines.

---

## 7. Local Setup & Setup Instructions

### Prerequisites
* **Node.js**: v20.x, v22.x, or v26.x
* **Package Manager**: `pnpm` (recommended) or `npm`
* **Firebase Project**: Authentication (Email/Password & Google) and Cloud Firestore enabled.
* **Google Gemini API Key**: API key from Google AI Studio.

### Quick Start
```bash
# 1. Clone repository
git clone https://github.com/rawalneel11-ui/life-plus.git
cd life-plus

# 2. Install dependencies
pnpm install

# 3. Configure environment variables
cp .env.example .env.local
```

Populate `.env.local`:
```env
NEXT_PUBLIC_FIREBASE_API_KEY=your_firebase_api_key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project_id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id

FIREBASE_ADMIN_PROJECT_ID=your_project_id
FIREBASE_ADMIN_CLIENT_EMAIL=your_service_account_email
FIREBASE_ADMIN_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"

GEMINI_API_KEY=your_gemini_api_key
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

```bash
# 4. Run development server
pnpm dev

# 5. Build for production
pnpm build
```

---

## 8. Verification & Test Suite

All 48 unit, integration, and security test cases pass cleanly:
```bash
# Run automated verification suites
node scripts/test-runner.js      # Carbon calculation engine tests
node scripts/test-datasets.js    # Zod schema validation tests
node scripts/test-eco-coach.js   # Gemini 2.5 Flash security & serverless tests
node scripts/test-phase6.js      # Gamification & anti-replay tests
node scripts/test-phase7.js      # Solar feasibility & district irradiance tests
```

---

## 9. NxtWave Evaluation Criteria Alignment

| Evaluation Criterion | Weight | How LiFE+ Delivers Maximum Value |
| :--- | :---: | :--- |
| **Technical Execution & Code Quality** | **40%** | Full-stack Next.js 16 App Router with TypeScript strict mode, zero build warnings, 48/48 automated tests passing, resilient REST-based auth pipeline, and live Vercel production deployment. |
| **System Architecture & Scalability** | **30%** | Cloud-native 4-tier design with Edge Middleware route protection, serverless autoscaling, BOM1 low-latency edge caching, and multi-tenant Firestore security rules. |
| **UI/UX Design** | **20%** | Bespoke Mission LiFE Gujarat design system in Tailwind CSS v4, smooth Framer Motion micro-interactions, responsive mobile/desktop layouts, accessible color contrast, and interactive 10-slide pitch deck viewer. |
| **Innovation & Problem Fit** | **10%** | Authentic citizen context injection into Google Gemini 2.5 Flash, transparent CEA-grounded carbon accounting, district-accurate solar feasibility, and anti-duplication gamification. |

---

## 10. License & Credits

Developed for the **Gujarat Energy Development Agency (GEDA)** under Hackathon Track **HC26-GEDA01**.  
Built under the principles of **Mission LiFE (Lifestyle for Environment)**.
