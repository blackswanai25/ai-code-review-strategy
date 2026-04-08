# Dynamic Persona Engine: Lead-Specific QA Pipeline

> Pre-test your product for each incoming lead BEFORE they sign up

## The Problem

You have 15 static personas covering broad archetypes. But when a real person from "Bauunternehmen Schmidt" with the title "Leiter Kalkulation" signs up for an Auftragr trial, you don't know:
- Does our product handle their specific workflow?
- What will annoy THEM specifically (not a generic persona)?
- What's the first thing they'll try to do — and will it work?
- Are we ready for THIS person, or will they bounce in 5 minutes?

## The Solution: Lead-Triggered Persona Pipeline

```
┌─────────────────────────────────────────────────────────────┐
│  TRIGGER: Lead shows interest                                │
│  (trial signup, demo request, inquiry email, website visit)  │
│                                                              │
│  Input: Name, Title, Company, Email                          │
│  Optional: LinkedIn URL, Industry                            │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│  STAGE 1: LEAD INTELLIGENCE (~30 seconds)                    │
│                                                              │
│  ┌─────────────┐  ┌──────────────┐  ┌────────────────┐     │
│  │ LinkedIn     │  │ Company      │  │ Industry       │     │
│  │ Profile      │  │ Website      │  │ Context        │     │
│  │ (Proxycurl)  │  │ (Scraper)    │  │ (Claude)       │     │
│  └──────┬──────┘  └──────┬───────┘  └───────┬────────┘     │
│         │                │                   │               │
│         └────────────────┼───────────────────┘               │
│                          │                                   │
│                   Enriched Lead Profile                       │
│                   - Role & seniority                         │
│                   - Company size & type                      │
│                   - Industry & specialization                │
│                   - Skills & expertise                       │
│                   - Likely workflows                         │
│                   - Tech stack they probably use             │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│  STAGE 2: PERSONA GENERATION (~10 seconds)                   │
│                                                              │
│  Claude generates a full persona JSON matching our format:   │
│  - daily_reality (based on real role data)                   │
│  - psychology (inferred from seniority, industry, role)      │
│  - expectations (what THIS person expects from OUR product)  │
│  - deal_breakers (what would make THEM leave)                │
│                                                              │
│  Also: match against closest static persona to see what's    │
│  already covered vs. what's new/different                    │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│  STAGE 3: EXPECTATION MAPPING (~20 seconds)                  │
│                                                              │
│  Run Phase 1 expectations for this specific persona:         │
│  - First screen expectations                                 │
│  - "Within 2 minutes I should be able to..."                │
│  - Trust signals they need                                   │
│  - Dealbreakers that would make them leave                   │
│  - Their #1 job-to-be-done                                  │
│  - What "good enough" means for THEM                        │
│                                                              │
│  Output: Scored checklist of 15-20 specific expectations     │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│  STAGE 4: PRODUCT READINESS CHECK (~2-5 minutes)             │
│                                                              │
│  For each expectation, check against actual product:         │
│                                                              │
│  Option A (fast): Claude evaluates from product knowledge    │
│  Option B (thorough): Playwright walks the product           │
│                                                              │
│  Score each expectation:                                     │
│  ✅ Met (1.0)    — product does this well                    │
│  ⚠️ Partial (0.5) — product does this but with friction     │
│  ❌ Not met (0.0) — product doesn't do this                 │
│  🚫 Dealbreaker (-1.0) — not met AND persona flagged it     │
│                          as a dealbreaker (3x weight)        │
│                                                              │
│  READINESS SCORE = weighted average                          │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│  STAGE 5: ACTION PLAN                                        │
│                                                              │
│  Score ≥ 85%: GREEN — Ready. Send personalized welcome.     │
│    → Generate custom onboarding path highlighting features   │
│      that match their specific workflow                      │
│                                                              │
│  Score 60-84%: YELLOW — Mostly ready, known gaps.           │
│    → Fix critical gaps if possible before they start         │
│    → Prepare workarounds / documentation for gaps            │
│    → Route their onboarding away from weak areas             │
│                                                              │
│  Score < 60%: RED — Not ready for this user type.           │
│    → Prioritize gap fixes in sprint backlog                  │
│    → Delay their trial or set expectations                   │
│    → Consider: is this even our ICP?                         │
│                                                              │
│  Output:                                                     │
│  1. Readiness score with breakdown                           │
│  2. Gap list (prioritized by impact on this persona)         │
│  3. Personalized onboarding recommendations                  │
│  4. GitHub Issues auto-created for critical gaps             │
└─────────────────────────────────────────────────────────────┘
```

## Why This Is Powerful

### For a solo founder:
- You can't manually test for every possible user type
- But you CAN test for the specific person who just showed interest
- First impressions determine everything — if their first 5 minutes have friction, they're gone
- This costs ~$0.50-1.00 per lead. For B2B SaaS where a customer is worth €hundreds/month, that's essentially free

### What makes this different from generic personas:
- Static personas = "a typical Kalkulator would expect X"
- Dynamic personas = "Hans Müller, Kalkulator at Tiefbau Schmidt GmbH, who specializes in Kanalbau and uses RIB iTWO, would expect X"
- The specificity matters because real users have specific tools, specific workflows, specific frustrations

### The compound effect:
- Every dynamic persona generated teaches you something about a user segment
- After 50 leads, you have 50 real-world persona profiles
- Patterns emerge: "All Kalkulatoren from companies >50 people expect GAEB P83 preview"
- Your static personas get more accurate over time
- Your product gets more ready for each new user type

---

## Lead Intelligence: LinkedIn Enrichment

### Option 1: Proxycurl API (Recommended)

**Pricing:** ~$0.01/credit (1 credit per profile lookup)
- Bulk: 1000 credits for $10
- Returns: headline, summary, experience history, skills, education, company info, certifications

**What you get for a construction industry lead:**
```json
{
  "full_name": "Hans Müller",
  "headline": "Leiter Kalkulation | Tiefbau Schmidt GmbH",
  "summary": "15 Jahre Erfahrung in der Kalkulation von Tiefbauprojekten...",
  "experiences": [
    {
      "title": "Leiter Kalkulation",
      "company": "Tiefbau Schmidt GmbH",
      "duration": "5 years",
      "description": "Verantwortlich für Angebotskalkulation im Kanalbau..."
    }
  ],
  "skills": ["Kalkulation", "VOB", "GAEB", "RIB iTWO", "Tiefbau"],
  "certifications": ["VOB-Sachkundiger"],
  "company": {
    "name": "Tiefbau Schmidt GmbH",
    "size": "51-200",
    "industry": "Civil Engineering",
    "location": "Nürnberg, Bayern"
  }
}
```

### Option 2: Apollo.io (Free tier available)
- 50 credits/month free
- Good for email + company data
- Less rich LinkedIn data than Proxycurl

### Option 3: Manual input (Zero cost)
- Add fields to your trial signup form:
  - Company name
  - Your role
  - Company size
  - Which features interest you most?
- This gives you 80% of what LinkedIn scraping provides
- No API cost, no legal risk

### Option 4: Hybrid (Recommended for start)
- Collect basic info at signup (name, title, company, email)
- If LinkedIn URL is provided or findable, enrich via Proxycurl
- If not, generate persona from title + company alone (Claude is surprisingly good at this)

---

## Persona Generation from Real Lead Data

### The Prompt

```
You are generating a user persona for product testing. 

LEAD DATA:
- Name: {name}
- Title: {title}
- Company: {company}
- Company size: {size}
- Industry: {industry}
- Location: {location}
- LinkedIn skills: {skills}
- LinkedIn summary: {summary}
- Current tools (from signup form or LinkedIn): {tools}

PRODUCT: {product_name} — {product_one_liner}

Generate a complete persona JSON with these sections:
1. daily_reality: What does this person's typical day look like? What tools 
   do they use? What's their biggest time waste? How many {relevant_actions} 
   do they do per week?
2. psychology: Tech savviness, risk tolerance, decision speed, trust signals,
   frustration triggers, delight triggers
3. expectations: First screen, must-haves, deal-breakers, nice-to-haves
4. current_pain_level: How much does their current approach hurt?

Base this on:
- Their actual role and seniority (from LinkedIn)
- Their company size (determines process formality, tool budget, decision authority)
- Their industry specialization (determines what features they'll look for first)
- Their skill set (determines tech savviness and which integrations they expect)

Be specific. Not "they use construction software" but "they likely use RIB iTWO 
based on their Kalkulation role at a mid-size Tiefbau firm in Bayern."
```

### Matching Against Static Personas

After generating the dynamic persona, compare it to the 5 static personas for that product:

```
COMPARISON: Dynamic persona "Hans Müller" vs. static persona library

Closest match: sabine-mueller-kalkulatorin (85% overlap)
  ✅ Same role type (Kalkulation)
  ✅ Same industry focus (Tiefbau)
  ✅ Same tool expectation (GAEB P83)
  ⚠️ Different company size (Hans: 120 people, Sabine: 80 people)
  ❌ Different specialization (Hans: Kanalbau, Sabine: general Tiefbau)
  
New expectations not in static persona:
  - Expects Kanalbau-specific LV positions
  - Company uses Nevaris, not iTWO
  - Needs Nachunternehmer management (larger company)
```

This tells you: "We've mostly tested for Hans's user type via Sabine, but we missed Kanalbau-specific needs and Nevaris integration."

---

## Readiness Scoring

### Score Calculation

```
For each expectation E[i]:
  weight[i] = 1.0 (normal) or 3.0 (if persona flagged as deal_breaker)
  score[i]  = 1.0 (met) or 0.5 (partial) or 0.0 (not met) or -1.0 (dealbreaker not met)

readiness = Σ(weight[i] × score[i]) / Σ(weight[i])
```

### Example: Hans Müller testing Auftragr

| # | Expectation | Weight | Score | Notes |
|---|------------|--------|-------|-------|
| 1 | Tiefbau/Kanalbau filter | 3.0 (DB) | 0.5 | Has Tiefbau but no Kanalbau sub-filter |
| 2 | GAEB P83 preview | 3.0 (DB) | 1.0 | ✅ Supported |
| 3 | Geographic radius filter | 1.0 | 1.0 | ✅ Works well |
| 4 | Submissionsfrist countdown | 1.0 | 1.0 | ✅ Present |
| 5 | German interface | 3.0 (DB) | 1.0 | ✅ Bilingual |
| 6 | Email alerts for matches | 1.0 | 1.0 | ✅ Daily digest |
| 7 | Nevaris ERP integration | 1.0 | 0.0 | ❌ Not available |
| 8 | Nachunternehmer sharing | 1.0 | 0.0 | ❌ Not available |
| 9 | Mobile-friendly | 1.0 | 0.5 | ⚠️ Works but not optimized |
| 10 | Price <€100/month | 1.0 | 1.0 | ✅ Within range |

**Readiness: (1.5 + 3.0 + 1.0 + 1.0 + 3.0 + 1.0 + 0 + 0 + 0.5 + 1.0) / (3+3+1+1+3+1+1+1+1+1) = 12.0/16.0 = 75%**

**Verdict: YELLOW** — Mostly ready. The Kanalbau sub-filter is a partial dealbreaker, but GAEB and German interface are solid. Nevaris and Nachunternehmer are missing but not dealbreakers for trial. Recommend: highlight GAEB and matching features in onboarding, acknowledge Kanalbau limitation.

---

## Implementation Architecture

### For Immediate Use (CLI Tool)

```
auftragr-readiness-check \
  --name "Hans Müller" \
  --title "Leiter Kalkulation" \
  --company "Tiefbau Schmidt GmbH" \
  --industry "Tiefbau" \
  --linkedin "https://linkedin.com/in/hansmueller" \
  --product auftragr

Output:
  → personas/dynamic/hans-mueller-tiefbau-schmidt.json
  → expectations/dynamic/hans-mueller-expectations.md
  → readiness/hans-mueller-readiness-report.md (score: 75%, YELLOW)
  → github-issues/hans-mueller-gaps.md (2 issues created)
```

### For Automated Use (Webhook Pipeline)

```
Trial Signup Form (Netlify/website)
        │
        ▼
Netlify Function: /api/lead-persona-trigger
        │
        ├── Call Proxycurl API (enrich LinkedIn)
        ├── Call Claude API (generate persona + expectations)
        ├── Call Claude API (readiness check against product knowledge)
        │
        ▼
Store results:
        ├── Persona JSON → database or git repo
        ├── Readiness report → Notion/Airtable or email to you
        ├── GitHub Issues → auto-created for critical gaps
        └── CRM tag → "Ready: GREEN/YELLOW/RED"
```

### For Full Automation (Browser-Based Testing)

```
After persona + expectations generated:
        │
        ▼
Playwright + Claude:
        ├── Login as test account matching persona's role
        ├── Navigate key flows this persona would try
        ├── Compare each screen against expectations
        ├── Screenshot every step
        │
        ▼
Generate visual readiness report:
        ├── Screenshots with persona commentary
        ├── Expectation vs. reality per screen
        ├── Overall readiness score
        └── Prioritized fix list
```

---

## Cost Per Lead

| Stage | Tool | Cost |
|-------|------|------|
| LinkedIn enrichment | Proxycurl | $0.01-0.10 |
| Persona generation | Claude Sonnet | ~$0.03 |
| Expectation mapping | Claude Sonnet | ~$0.05 |
| Readiness check (knowledge-based) | Claude Sonnet | ~$0.05 |
| Readiness check (browser-based) | Playwright + Claude | ~$0.30-0.50 |
| GitHub issue creation | gh CLI | $0.00 |
| **Total (fast mode)** | | **~$0.15-0.25** |
| **Total (thorough mode)** | | **~$0.50-0.75** |

**At $0.25-0.75 per lead, testing 100 leads/month = $25-75.** For B2B SaaS in procurement where a single customer might be worth €200-500/month, this is a no-brainer investment.

---

## The Feedback Loop

### From Leads to Product Improvement

```
Lead 1: Hans (Kalkulator, Tiefbau) → Score: 75% → Gap: Kanalbau filter
Lead 2: Maria (Einkäuferin, Hochbau) → Score: 90% → Minor: mobile UX
Lead 3: Peter (GF, Elektro) → Score: 60% → Gap: too complex for SME
Lead 4: Sabine (Kalkulator, Straßenbau) → Score: 70% → Gap: sub-trade filter
Lead 5: Jan (Vertrieb, Fassade) → Score: 65% → Gap: private pipeline

PATTERN DETECTED:
- 3/5 leads are Kalkulatoren → they all want sub-Gewerk filtering
- 2/5 are non-technical → onboarding is too complex for SME GFs
- Kanalbau + Straßenbau + Fassade = need better sub-trade taxonomy

SPRINT PRIORITY:
1. Sub-Gewerk filter (impacts 60% of leads)
2. Simplified SME onboarding (impacts 40% of leads)
3. Mobile UX improvements (impacts 20% of leads)
```

Your product roadmap becomes DATA-DRIVEN by actual incoming leads, not guesswork.

### From Dynamic Personas to Static Persona Updates

After 20+ dynamic personas for a product:
- Cluster them by role/industry
- Identify patterns not covered by your 5 static personas
- Add new static personas for underserved segments
- Update existing personas with real-world data

---

## Integration with Existing Pipeline

This slots into the quality pipeline as Eyes 7-8:

| Eye | Tool | What It Validates |
|-----|------|-------------------|
| 1-2 | Claude Code + Codex | Code correctness |
| 3 | CodeRabbit | Bugs, patterns, style |
| 4 | Claude Code Action | Logic, security |
| 5 | Qodo PR-Agent | Test coverage |
| 6 | One Horizon | Product intent |
| 7 | Static Personas (15) | Generic user experience across archetypes |
| **8** | **Dynamic Personas (per lead)** | **Specific user readiness per real prospect** |

---

---

## Codex Critical Review: GDPR & Legal Risks

> Reviewed by OpenAI Codex (o4-mini). Critical findings that reshape the approach.

### GDPR Risk: LinkedIn Scraping

**Problem:** LinkedIn ToS prohibit automated scraping. Proxycurl claims "licensed data" but YOU still need a lawful basis under GDPR (Art. 6) to process it. German data protection (BDSG) is even stricter.

**Mitigation — The Consent-First Approach:**
- **Do NOT scrape LinkedIn without the lead's knowledge**
- Instead: ask leads to provide their LinkedIn URL voluntarily during signup ("Help us personalize your experience")
- If they provide it, you have implied consent for business-relevant data
- If they don't, fall back to title + company + signup form answers
- Document a Legitimate Interest Assessment (LIA) regardless

### GDPR Risk: Profiling Government Procurement Officers

**Problem:** Public procurement officers are public officials. Profiling them personally may trigger BDSG § 3 concerns. GDPR Art. 22 prohibits purely automated decisions affecting data subjects.

**Mitigation:**
- The persona engine is an ADVISOR, not a GATEKEEPER
- Never auto-reject or deprioritize leads based on scores
- Always have human review of readiness scores before action
- Strip any non-business data (politics, personal interests, education details)

### Risk: Cookie-Cutter Personas

**Problem:** LLMs regress to the mean — two similar job titles produce nearly identical personas.

**Mitigation:**
- Feed high-signal context: company specialization, signup form answers ("What's your biggest challenge?"), company size
- Validate: if two personas for similar leads look identical, the engine isn't adding value — flag this
- Over time, calibrate against real conversion data

### Risk: False Confidence in Scores

**Problem:** Readiness scores based on AI-predicted expectations ≠ real user behavior. People say they want X, then ignore it.

**Mitigation:**
- Treat scores as FORECASTS with confidence bands, not ground truth
- After leads start using the product, compare predicted vs actual behavior
- Calibrate the model: if high-readiness leads churn, the model is wrong
- Plan for 10-20 real user interviews to validate the first batch of dynamic personas

### Risk: The "Creepy" Factor

**Problem:** Referencing personal LinkedIn history in outreach feels surveillance-like.

**Mitigation:**
- Never reference personal details in outreach
- Only use enrichment data internally for product testing
- Be transparent in privacy policy about data collection
- Limit stored data to business-relevant fields only

### Revised Approach: Consent-Based Dynamic Personas

```
ORIGINAL (risky):
  Lead signs up → Auto-scrape LinkedIn → Generate persona silently

REVISED (GDPR-safe):
  Lead signs up → Ask: "Help us personalize your trial"
    → Optional: LinkedIn URL, company size, biggest challenge
    → Optional: "What tools do you currently use?"
  → Generate persona from VOLUNTARILY PROVIDED data
  → If no extra data: use title + company + industry defaults
```

This is safer AND more accurate — self-reported data beats scraped data because the lead tells you their actual workflow, not what LinkedIn says.

### Leads Without LinkedIn (German Handwerk)

Very common in construction. Fallbacks:
- Signup form with role-specific questions
- Company lookup via Unternehmensregister.de or IHK listings (public data, no GDPR issue)
- Default to closest static persona from the library
- Over time, build Handwerk-specific persona archetypes

---

## Implementation Priority

### Week 1: Manual CLI Version
- Build a simple script that takes name/title/company/industry
- Generates persona + expectations using Claude API
- Runs readiness check against product knowledge (no browser yet)
- Outputs markdown report

### Week 2: LinkedIn Enrichment
- Add Proxycurl integration for automatic profile enrichment
- Compare dynamic personas against static persona library

### Week 3: Automated Webhook
- Trigger on trial signup
- Auto-generate persona + readiness report
- Email you the report before the lead starts their trial

### Month 2: Browser-Based Testing
- Add Playwright walkthrough for thorough testing
- Screenshot-based readiness reports
- Automated GitHub issue creation for gaps

### Month 3: Pattern Analysis
- Dashboard showing lead readiness trends
- Automatic sprint priority suggestions based on lead patterns
- Static persona library auto-updates from dynamic persona clusters
