# Implementation Plan: Deploying the Quality Pipeline Across 4 Products

> Created: 2026-04-08

## Current State Assessment

| Product | Repo | Stack | Tests | CI/CD | Review Pipeline | Biggest Gap |
|---------|------|-------|-------|-------|----------------|-------------|
| **Auftragr** | `auftragr` | Next.js 14, TS | Vitest (4 suites) | Netlify | None | No automated review |
| **Zuschlagr** | `zuschlagr` | React+Vite, TS | **ZERO** | Netlify | None | No tests at all |
| **Zeitplanr** | `bookmymeeting` | Next.js 14, TS | Vitest (multi) | Netlify | None | No automated review |
| **Free 5-Lens** | `free5lensanalysis` | Python 3.11 | Pytest (10+) | **None** | None | No CI/CD at all |

All 4 have CLAUDE.md. None have .coderabbit.yaml or GitHub Actions.

---

## Phase 1: Code Review Pipeline (Day 1-2)

### What We Can Do Right Now (no secrets needed)

For each of the 4 repos, add these files:

#### 1a. `.coderabbit.yaml` — Customized per product

**Auftragr:**
```yaml
language: de-DE
reviews:
  auto_review:
    enabled: true
    drafts: false
  path_instructions:
    - path: "src/app/api/**"
      instructions: "Check for input validation, auth (NextAuth), rate limiting, and Neon DB query safety"
    - path: "src/db/**"
      instructions: "Review Drizzle ORM queries for SQL injection, missing indexes, and migration safety"
    - path: "src/lib/matching/**"
      instructions: "Validate scoring algorithm correctness — weights must sum to 100%"
    - path: "netlify/functions/**"
      instructions: "Check for proper error handling, timeout management, and EU data residency compliance"
    - path: "src/lib/ai/**"
      instructions: "Verify prompt injection protection, token limits, and model fallback handling"
chat:
  auto_reply: true
```

**Zuschlagr:**
```yaml
language: de-DE
reviews:
  auto_review:
    enabled: true
    drafts: false
  path_instructions:
    - path: "netlify/functions/**"
      instructions: "Check for input validation, auth, rate limiting, and proper error responses"
    - path: "netlify/functions/_shared/ai/**"
      instructions: "Verify AI provider abstraction correctness, prompt injection protection, token limits"
    - path: "netlify/functions/_shared/rag/**"
      instructions: "Review embedding pipeline, retrieval logic, and pgvector query performance"
    - path: "netlify/functions/_shared/prompts/**"
      instructions: "Validate German language prompts for accuracy, completeness, and legal terminology"
    - path: "packages/shared/**"
      instructions: "Ensure Zod schemas are complete and match database schema"
    - path: "src/**"
      instructions: "Check React components for accessibility, error states, and loading states"
chat:
  auto_reply: true
```

**Zeitplanr (BookMyMeeting):**
```yaml
language: de-DE
reviews:
  auto_review:
    enabled: true
    drafts: false
  path_instructions:
    - path: "src/app/api/**"
      instructions: "Check for auth (NextAuth + Google OAuth), input validation, RLS compliance, and GDPR data handling"
    - path: "prisma/**"
      instructions: "Review migrations for data safety, RLS policies, and backwards compatibility"
    - path: "src/lib/**"
      instructions: "Verify Google Calendar API integration, timezone handling, and availability calculations"
    - path: "src/components/**"
      instructions: "Check for accessibility (a11y), loading states, error boundaries, and i18n"
    - path: "**/*.test.*"
      instructions: "Verify edge cases: timezone boundaries, DST transitions, concurrent bookings, holiday conflicts"
chat:
  auto_reply: true
```

**Free 5-Lens Analysis:**
```yaml
language: de-DE
reviews:
  auto_review:
    enabled: true
    drafts: false
  path_instructions:
    - path: "src/free5lens/agents/**"
      instructions: "Verify each lens agent's analysis logic, prompt quality, and German construction domain accuracy"
    - path: "src/free5lens/services/**"
      instructions: "Check API integration (Mistral), error handling, retry logic, and token management"
    - path: "src/free5lens/report/**"
      instructions: "Validate report generation accuracy, PDF formatting, and German language output"
    - path: "tests/**"
      instructions: "Verify test coverage of all 5 lenses, edge cases, and error scenarios"
chat:
  auto_reply: true
```

#### 1b. GitHub Actions Workflows

Create 3 workflow files per repo (Claude, Codex, Qodo). Template below — customize `paths:` per stack.

**TypeScript repos (Auftragr, Zuschlagr, Zeitplanr):**
```yaml
# paths filter:
paths:
  - '**/*.ts'
  - '**/*.tsx'
  - '**/*.js'
  - '**/*.jsx'
  - '**/*.css'
```

**Python repo (Free 5-Lens):**
```yaml
# paths filter:
paths:
  - '**/*.py'
  - '**/*.toml'
  - '**/*.yaml'
```

### What YOU Need To Do (manual steps)

1. **Install CodeRabbit GitHub App** on all 4 repos:
   - Go to https://www.coderabbit.ai → Sign in with GitHub → Install App → Select all 4 repos
   - Takes 2 minutes

2. **Add GitHub Secrets** to each repo (or once at org level):
   - `ANTHROPIC_API_KEY` — from console.anthropic.com
   - `OPENAI_API_KEY` — from platform.openai.com
   - Settings → Secrets and variables → Actions → New repository secret

3. **Start using branches + PRs** (if not already):
   - Never commit directly to main
   - Create feature branches, push PRs
   - The review pipeline only triggers on PRs

---

## Phase 2: Persona Library (Day 2-3)

### Product-Specific Personas

All products target the German market (DACH region). Personas must reflect German business culture, procurement regulations (VOB/VgV/GWB), and professional norms.

#### Auftragr Personas (Tender Discovery)

| # | Name | Title | Company | Industry Focus |
|---|------|-------|---------|---------------|
| 1 | Thomas Berger | Einkaufsleiter | Mid-size Bauunternehmen (150 employees) | Hochbau (building construction) |
| 2 | Lisa Hartmann | BIM-Managerin | Large GU/Generalunternehmer (500+) | Infrastructure |
| 3 | Klaus Weber | Geschäftsführer | Small Handwerksbetrieb (15 employees) | Elektrotechnik |
| 4 | Sabine Müller | Kalkulatorin | Civil engineering firm (80 employees) | Tiefbau (civil works) |
| 5 | Michael Schneider | Vertriebsleiter | Specialty subcontractor (40 employees) | Fassadenbau (facades) |

#### Zuschlagr Personas (Bid Evaluation)

| # | Name | Title | Company | Context |
|---|------|-------|---------|---------|
| 1 | Dr. Andrea Fischer | Leiterin Vergabestelle | Municipal authority (Stadtverwaltung) | Manages 50+ procurements/year |
| 2 | Markus Hoffmann | Sachbearbeiter Vergabe | State ministry (Landesministerium) | Processes bids for large infrastructure |
| 3 | Claudia Braun | Vergaberechtsexpertin | Public entity (Eigenbetrieb) | Legal compliance focus |
| 4 | Stefan Koch | Technischer Prüfer | Federal agency | Technical bid evaluation |
| 5 | Ingrid Neumann | Rechnungsprüferin | Court of Auditors (Rechnungshof) | Post-award compliance audit |

#### Zeitplanr Personas (Meeting Scheduling)

| # | Name | Title | Company | Context |
|---|------|-------|---------|---------|
| 1 | Jan Richter | Teamleiter Engineering | Tech startup (30 employees) | Schedules daily standups, client calls |
| 2 | Petra Becker | Projektleiterin | Mittelstand manufacturing (200 employees) | Coordinates cross-department meetings |
| 3 | Anna Schmidt | Executive Assistant | Corporate HQ (DAX company) | Manages C-suite calendars |
| 4 | David Kim | Freelance Consultant | Solo (international clients) | Multi-timezone, minimal friction needed |
| 5 | Lena Wagner | HR Recruiterin | Growing SaaS company (80 employees) | 20+ interview slots per week |

#### Free 5-Lens Personas (Tender Analysis)

| # | Name | Title | Company | Context |
|---|------|-------|---------|---------|
| 1 | Frank Zimmermann | Kalkulator | Mid-size Bauunternehmen (100 emp) | Bid/no-bid decisions daily |
| 2 | Heike Vogel | Bauleiterin | General contractor (200 emp) | Feasibility and execution planning |
| 3 | Dr. Martin Schäfer | Risikomanager | Large construction group (1000+ emp) | Contract risk assessment |
| 4 | Ursula Klein | Geschäftsführerin | Small specialty firm (25 emp) | Strategic decisions on which markets to enter |
| 5 | Jörg Lehmann | Externer Berater | Independent consultant | Advises SMEs on tender strategy |

---

## Phase 3: First Expectation Mapping Run (Day 3-4)

For each product, run Phase 1 of the UX strategy:
1. Load each persona
2. Tell them about the product (one-liner description)
3. Ask: "What do you expect to see? What would make you trust/leave? What must it do better than your current approach?"
4. Store results as baseline expectations

**Execution:** Run this directly in Claude Code using the persona JSON files. No browser automation needed yet.

**Output:** `expectations/` directory per product with one JSON per persona.

---

## Phase 4: First Product Walkthrough (Day 4-7)

### Approach: Screenshots + Claude Evaluation (Option A)

For each product:
1. Take 5-8 screenshots of key screens/flows
2. Load each persona + their expectations
3. Ask Claude to evaluate each screen as that persona
4. Run jury deliberation to synthesize findings

### Key Flows Per Product

**Auftragr:**
1. Landing page → Sign up → Onboarding
2. Dashboard → New tenders today → Filter by trade/location
3. Tender detail → AI analysis → Scoring breakdown
4. Saved searches → Email digest settings
5. Premium features → Pricing → Upgrade flow

**Zuschlagr:**
1. Landing page → Create evaluation → Upload tender criteria
2. Invite bidders → Receive bids → Bid overview
3. Evaluation matrix → Score bids → Compare side-by-side
4. Award decision → Generate protocol → Export audit trail
5. Bidder debrief → Feedback generation

**Zeitplanr:**
1. Landing → Sign up → Connect Google Calendar
2. Create event type → Set availability → Share link
3. Booking page (guest view) → Select slot → Confirm
4. Dashboard → Upcoming bookings → Reschedule/cancel
5. Widget embed → Integration in external website

**Free 5-Lens:**
1. CLI: Upload tender document
2. AI analysis running (5 lenses)
3. Report: Commercial lens findings
4. Report: Risk lens findings
5. Final recommendation + PDF export

---

## Phase 5: Zuschlagr Test Suite (Day 5-7) — CRITICAL

Zuschlagr has ZERO tests. This is the highest-risk product from a quality perspective. Before the review pipeline can be effective, we need baseline tests.

**Priority test areas:**
1. Zod schema validation (packages/shared)
2. API endpoint input validation (netlify/functions)
3. AI provider abstraction (model switching, error handling)
4. RAG pipeline (embedding, retrieval, scoring)
5. Evaluation scoring algorithm correctness
6. German procurement compliance rules

**Approach:** Use Qodo + Claude Code to generate an initial test suite.

---

## Phase 6: Template and Scale (Week 2)

Once Product 1 is fully working:
1. Copy CI configs to remaining 3 repos (customized per stack)
2. Run persona expectation mapping for remaining 3 products
3. Run walkthroughs for remaining 3 products
4. Generate jury reports for all 4

---

## Execution Order (Prioritized)

| Day | Action | Products | Who |
|-----|--------|----------|-----|
| **Day 1** | Add .coderabbit.yaml to all repos | All 4 | Claude Code |
| **Day 1** | Add GitHub Actions workflows to all repos | All 4 | Claude Code |
| **Day 1** | YOU: Install CodeRabbit App + add secrets | All 4 | Manual |
| **Day 2** | Build persona JSON files | All 4 | Claude Code |
| **Day 2** | Run expectation mapping | Start with Auftragr | Claude Code |
| **Day 3** | Run expectation mapping | Remaining 3 | Claude Code |
| **Day 3** | Screenshots + persona walkthrough | Auftragr | Claude Code |
| **Day 4** | Screenshots + persona walkthrough | Zuschlagr, Zeitplanr | Claude Code |
| **Day 5** | Generate Zuschlagr test suite | Zuschlagr | Claude Code + Qodo |
| **Day 6** | Jury deliberation for all 4 products | All 4 | Claude Code |
| **Day 7** | Compile findings, create GitHub issues | All 4 | Claude Code |
| **Week 2** | First real PR with full review pipeline | Pilot: Auftragr | You |
| **Week 2** | Validate: did the pipeline catch real issues? | All 4 | Review |

---

## What I'll Build Right Now

With your go-ahead, I'll:

1. **Create `.coderabbit.yaml`** for all 4 repos (pushed directly)
2. **Create GitHub Actions workflows** (claude-review.yml, codex-review.yml, qodo-review.yml) for all 4 repos
3. **Create persona JSON files** in the strategy repo under `personas/`
4. **Run the first expectation mapping** for your most critical product

This sets up the entire infrastructure. Once you install CodeRabbit and add secrets, the pipeline goes live on the next PR.

### What I Need From You

1. **Which product is highest priority?** (I'd guess Auftragr or Zuschlagr based on activity)
2. **Are these products deployed and accessible?** (I need URLs for screenshot walkthroughs)
3. **Confirm: should I push .coderabbit.yaml and workflow files directly to main on all 4 repos?** Or create PRs?
