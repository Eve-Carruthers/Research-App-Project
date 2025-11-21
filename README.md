# Kinetic
## The Systematic Research Engagement Platform

> Transform passive reading into measurable progress. Track your research journey, engage with your lab, and discover what matters—without the noise.

---

### The Problem

Reading research papers is **invisible work**. You spend hours, but have nothing to show for it. There's no professional way to track your engagement, no scalable forum for paper-level discussion, and no system for labs to share their academic pulse. Journal clubs are fragmented. Discovery is overwhelming. And your reading streak? It only exists in your head.

---

### The Solution

PaperTrail is **personal research infrastructure that becomes social through use**:

- **For You**: A private Research-Log (GitHub-style heatmap) that tracks every paper you touch, rewarding discipline with Research Points (RP).
- **For Your Lab**: A private annotation layer and reading room scheduler that makes journal clubs 10x more efficient.
- **For Your Field**: Lab Streams—public activity feeds where verified labs share what they're reading and discussing, creating ambient social proof.

**Built for researchers, refined for PIs, and accessible to all.**

---

###  Core Features

#### **1. Research-Log** (Your Academic Streak)
Your visual anchor. A 52-week heatmap showing the depth of your daily engagement:
-  **Mint**: Read abstract, saved paper (1-9 RP)
-  **Emerald**: Added private annotation (10-24 RP)  
-  **Forest**: Public comment, summary, or author Q&A (25+ RP)

*Private by default. Public, if you choose. Streaks are for you, not performance.*

#### **2. Lab Streams** (Public Research Activity)
Every verified lab gets an X-style activity feed—auto-generated from real research actions:
- "MIT Vision Lab commented on *Diffusion Models for Medical Imaging*"
- "Weekly Digest: 12 papers saved this week"
- "Live Q&A with Dr. Chen tomorrow → RSVP"

*Free viewers can follow 3 streams. Upgrade to join the conversation.*

#### **3. Discovery Engine** (Spotify for Papers)
Hybrid algorithm blending content signals, network velocity, and collaborative filtering:
-  **Active Debates**: Papers with accelerating comment velocity
-  **Lab Picks**: What your network is reading
-  **ELIA Suggests**: Based on where you spend time (methods vs. intro)

*Serendipity slider lets you control how much randomness you want.*

#### **4. Intelligent Reader** (Evidence Broker AI)
A RAG-based system that surfaces evidence, not truth:
- **Evidence Map**: Side panel showing supporting/contextual papers from Semantic Scholar
- **Ask the Paper**: Grounded Q&A citing line numbers (Pro)
- **Synthesise My Library**: Debate map across your saved papers (Pro)

*Every citation is one-click to the source. You decide what's valid.*

#### **5. Digital Journal Clubs** (Lab Tier)
- **Pre-Meeting**: Private annotation overlay for lab members
- **Live**: Host Reading Rooms via partner platform (integrated)
- **Post-Meeting**: Auto-generated key questions list

---

### 🎯 Who is PaperTrail For?

| Personla | Goal | Entry Tier | Core Value |
| :--- | :--- | :--- | :--- |
| **Public** | Stay current, feel productive | **Free** | Private Research-Log, follow 3 labs |
| **Postdoc/ECR** | Build expertise, visibility | **Pro ($5/mo)** | Ask the Paper, unlimited streams |
| **PI** | Manage lab's literature intake | **Lab ($150/mo)** | Lab dashboard, host Reading Rooms |
| **Department Head** | Workforce analytics, recruiting | **Institutional ($15k+/yr)** | SSO, API, white-label, custom RAG |

---


#### **For Developers (Self-Host)**
```bash
# Clone the monorepo
git clone https://github.com/papertrail/papertrail.git
cd papertrail

# Set up environment
cp .env.example .env
# Add your API keys: NCBI_EUTILS_KEY, SEMANTIC_SCHOLAR_KEY

# Run with Docker Compose (includes Neo4j, Qdrant)
docker-compose up -d

# Frontend
cd apps/web && npm install && npm run dev

# Backend
cd apps/api && poetry install && uvicorn main:app --reload
```

**Requirements**: Node.js 20+, Python 3.12+, Docker

---

### Technical Architecture

#### **High-Level Design**
```
┌─────────────────────────────────────────────────────────────┐
│                    Frontend (Next.js 14)                    │
│  • WCAG AAA Accessible UI (Radix + Tailwind)               │
│  • React Query for state management                          │
└───────────────────────────┬─────────────────────────────────┘
                            │
┌───────────────────────────▼─────────────────────────────────┐
│                    API Gateway (FastAPI)                    │
│  • GraphQL (queries) + REST (mutations)                    │
│  • JWT auth, rate limiting (3 req/s for free)              │
└───────────────────────────┬─────────────────────────────────┘
                            │
┌───────────────────────────▼─────────────────────────────────┐
│              Core Services (Modular Monolith)               │
│  • Engagement Graph (Neo4j) - user-paper relationships     │
│  • RAG Pipeline (Python) - Qdrant vector DB, LLM calls    │
│  • Stream Service (Node) - Lab Stream generation           │
└───────────────────────────┬─────────────────────────────────┘
                            │
┌───────────────────────────▼─────────────────────────────────┐
│              External APIs (Polite Crawling)                │
│  • NCBI E-utilities, Semantic Scholar, arXiv, OpenAlex     │
└─────────────────────────────────────────────────────────────┘
```

#### **Key Technical Decisions**
- **Never host PDFs**: Load client-side from arXiv/DOI sources (legal safe harbour).
- **Cache metadata**: Redis for 7 days; PostgreSQL for persistent data.
- **AI is a service**: RAG runs async; results stream to UI via WebSockets.
- **Accessibility**: axe-core in CI, Lighthouse score ≥95 required to merge.

---

### 📈 Roadmap

#### **Phase 1 **
- [x] Research-Log heatmap MVP
- [x] NCBI E-utilities integration
- [ ] Community Catalyst hiring (5 postdocs)
- [ ] Public launch in "Diffusion Models" field

#### **Phase 2**
- [ ] Lab Streams (Catalyst activity only)
- [ ] Public comments & Following features
- [ ] Basic Evidence Map (Semantic Scholar data)
- [ ] Lab Tier ($150/mo) launch

#### **Phase 3**
- [ ] "Ask the Paper" RAG feature
- [ ] Human-in-the-Loop voting system
- [ ] Pro Tier ($5/mo) launch
- [ ] Expand to "Computational Biology"

#### **Phase 4 **
- [ ] SSO, analytics dashboard
- [ ] Custom RAG models for labs
- [ ] Institutional Tier ($15k+/yr) sales

---

###  Contributing

We believe research infrastructure should be open. PaperTrail is **AGPL-3.0 licensed**; commercial features are closed-source plugins.

#### **How to Contribute**
1. **Issues**: Tag with `accessibility`, `api`, `ui`, or `ai`
2. **PRs**: Must pass axe-core, Lighthouse ≥95, and Promptfoo evals

---

###  License

[AGPL-3.0](LICENSE) - Core platform is open. Commercial features (Lab/Institutional tiers) are proprietary extensions.

---
