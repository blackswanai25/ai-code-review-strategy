---
product: zeitplanr
date: 2026-04-08
phase: product-walkthrough
screens_evaluated: landing-page, registration
personas_count: 5
---

# Zeitplanr — Phase 2: Product Walkthrough

Evaluating the live product (https://zeitplanr.de/) against Phase 1 expectations.

---

## Screen 1: Landing Page (https://zeitplanr.de/)

### What the page shows:
- **Hero:** "Die Calendly-Alternative aus Deutschland" — Professionelle Terminplanung, 100% kostenlos, Open Source, DSGVO-konform
- **Features:** 12 feature cards including Google Calendar sync, team bookings with round-robin, embeddable widget, webhooks, recurring bookings, holiday detection
- **Calendar support mentioned:** Google Calendar, CalDAV & Outlook, Google Meet & Jitsi, Nextcloud Talk
- **Pricing:** Free (Open Source). Comparison table vs Calendly showing all features included at €0
- **Legal:** Impressum, Datenschutz, AGB, AVV, DSE-Hinweis, Trust Center all present
- **DSGVO:** Heavily emphasized — EU Frankfurt hosting, no US data transfer, AES-256, audit logging, data export/deletion
- **Team features:** "Team-Buchungen mit Round-Robin-Zuweisung" mentioned
- **Language:** German primary, English toggle available
- **Design:** Clean, professional, modern UI with gradient accents
- **Footer:** "Made in Erlangen, Germany" — "Ein Community-Projekt"

---

### Jan Richter — Teamleiter Engineering, CloudNova GmbH (Berlin startup)

**First Impression (0-30 seconds):**
Score: 🟢 POSITIVE

| Expectation | Status | Notes |
|------------|--------|-------|
| Google Calendar sync prominently shown | ✅ Met | Featured prominently in feature cards |
| Multiple event types on free tier | ✅ Met | "100% kostenlos" — all features included |
| Professional booking page | ⚠️ Partial | Claimed but no live demo visible without signup |
| Fast setup (<2 min) | ⚠️ Partial | "3 Schritte" setup process shown, looks simple |
| Google Meet integration | ✅ Met | "Google Meet & Jitsi" explicitly listed |
| DSGVO compliant | ✅ Met | Heavily emphasized, Frankfurt hosting |
| Buffer time between meetings | ❓ Unknown | Not visible on landing page |
| Dark mode | ❓ Unknown | Not mentioned |

**Jan's reaction:** "Free, open source, Google Calendar + Meet, DSGVO — this checks my main boxes. Clean design. I'll sign up and test it in 5 minutes. Only concern: no live demo booking page to preview before committing."

**Expectation gaps found:** 1 (no demo booking page preview)
**Dealbreakers triggered:** 0

---

### Petra Becker — Projektleiterin, Maschinenbau Becker & Sohn (Stuttgart Mittelstand)

**First Impression (0-30 seconds):**
Score: 🟡 MIXED — Critical risk identified

| Expectation | Status | Notes |
|------------|--------|-------|
| Outlook/Exchange support | ⚠️ Partial | "CalDAV & Outlook" listed in features but NOT prominent — buried in feature grid |
| German interface | ✅ Met | Fully German, professional copy |
| DSGVO documentation for IT dept | ✅ Met | AVV, DSE-Hinweis, Trust Center — excellent |
| Impressum exists | ✅ Met | Present in footer |
| Professional appearance | ✅ Met | Clean, modern design |
| Phone/email support | ⚠️ Partial | "Community Support" mentioned, no phone number visible |
| Other Mittelstand companies use it | ❌ Not met | No customer logos, testimonials, or case studies |
| Pricing in Euros, transparent | ✅ Met | Free, clearly stated |
| Guest booking without account | ❓ Unknown | Not explicitly stated on landing page |
| MS Teams integration | ❌ Not met | Only Google Meet & Jitsi mentioned |

**Petra's reaction:** "German, DSGVO-konform, AVV vorhanden — meine IT-Abteilung wäre zufrieden. ABER: Outlook-Support steht zwar in der Feature-Liste, aber die Hauptbotschaft ist 'Google Calendar.' Wo sind die Referenzen? Kein einziges Unternehmen als Referenz? 'Community-Projekt' klingt nach Hobby, nicht nach Enterprise-Software. Und wo ist MS Teams? Wir nutzen kein Google Meet. Ich bin skeptisch, aber der Preis (kostenlos) senkt die Einstiegshürde genug, dass ich es trotzdem probiere."

**Expectation gaps found:** 4 (Outlook buried, no testimonials, no MS Teams, "Community-Projekt" branding)
**Dealbreakers triggered:** 0 (Outlook IS mentioned, just not prominent — she'd proceed cautiously)

**CRITICAL FINDING:** The hero says "Calendly-Alternative" and the entire positioning screams Google ecosystem. Petra uses Outlook/Exchange. She's not gone in 30 seconds (Outlook IS in the features), but she's skeptical. The "Community-Projekt" label and zero customer references will make her hesitate to propose this to her IT department.

---

### Anna Schmidt — Assistentin der Geschäftsführung, Müller Consulting AG (Frankfurt)

**First Impression (0-30 seconds):**
Score: 🟡 MIXED — Major uncertainty

| Expectation | Status | Notes |
|------------|--------|-------|
| Multi-calendar management (3 Partners) | ❓ Unknown | "Team-Buchungen" mentioned but unclear if one user can manage multiple people's calendars |
| Booking approval workflow | ❓ Unknown | Not mentioned on landing page |
| Per-person availability rules | ❓ Unknown | Not mentioned on landing page |
| Buffer/prep time between meetings | ❓ Unknown | Not mentioned on landing page |
| Professional booking pages | ⚠️ Partial | Claimed but no preview |
| Google Calendar + Meet | ✅ Met | Prominently featured |
| Single dashboard for all Partners | ❓ Unknown | Can't tell from landing page |

**Anna's reaction:** "Kostenlos und DSGVO-konform — gut. Aber meine Hauptfrage beantwortet die Seite nicht: Kann ich von EINEM Account aus die Kalender von drei Partnern verwalten? 'Team-Buchungen mit Round-Robin' klingt nach Verteilung auf mehrere Personen, nicht nach einer Assistentin, die mehrere Chefs koordiniert. Ich muss mich anmelden, um das herauszufinden. Wenn es das nicht kann, bin ich sofort wieder weg."

**Expectation gaps found:** 5+ (multi-calendar unclear, approval workflow unclear, buffer time unclear)
**Dealbreakers triggered:** 0 yet (she'll sign up to investigate, but the landing page doesn't answer her core question)

**CRITICAL FINDING:** Anna's #1 use case (managing 3 Partners' calendars from one dashboard) is not addressed on the landing page at all. "Team-Buchungen" sounds like employee scheduling, not executive assistant calendar management. This is the highest-risk persona — she'll sign up and leave within 5 minutes if the feature doesn't exist.

---

### David Kim — Freelance Strategy Consultant, Köln (4 timezones)

**First Impression (0-30 seconds):**
Score: 🟢 POSITIVE with caveats

| Expectation | Status | Notes |
|------------|--------|-------|
| Timezone handling prominently shown | ⚠️ Partial | Not explicitly mentioned on landing page — assumed but not stated |
| Embeddable widget | ✅ Met | "Einbettbares Widget (iFrame)" explicitly listed |
| Google Meet + Zoom support | ⚠️ Partial | Google Meet yes, Jitsi yes, Zoom NOT mentioned |
| Daily meeting limits | ❓ Unknown | Not mentioned |
| Focus time blocks | ❓ Unknown | Not mentioned |
| Free tier sufficient for solo | ✅ Met | Everything free |
| DSGVO compliant | ✅ Met | Strong emphasis |
| Custom domain for booking | ❓ Unknown | Not mentioned |
| 7-language booking pages | ✅ Met | DE, EN, FR, ES, IT, NL, PT — excellent for international clients |

**David's reaction:** "Free, embeddable, 7 languages — nice. But I don't see 'timezone' mentioned anywhere on this page? For a scheduling tool? That's... concerning. And no Zoom? Half my clients use Zoom. I'll sign up because it's free, but timezone handling better be bulletproof once I'm in."

**Expectation gaps found:** 3 (no timezone mention, no Zoom, no daily limits/focus time)
**Dealbreakers triggered:** 0 (he'll sign up to test, but timezone is make-or-break)

---

### Lena Wagner — HR Recruiterin, ScaleUp Solutions GmbH (Hamburg)

**First Impression (0-30 seconds):**
Score: 🟢 POSITIVE — surprisingly strong

| Expectation | Status | Notes |
|------------|--------|-------|
| Team scheduling with round-robin | ✅ Met | "Team-Buchungen mit Round-Robin-Zuweisung" — exactly what she needs |
| Affordable for 8+ users | ✅ Met | Free! Beats Calendly Teams at €128/month for 8 users |
| Automated reminders | ❓ Unknown | Not explicitly mentioned on landing page |
| DSGVO consent checkbox on booking | ❓ Unknown | Registration has DSGVO checkbox, unclear for guest booking |
| Google Calendar + Meet | ✅ Met | Featured |
| Candidate self-reschedule | ❓ Unknown | Not mentioned |
| Professional booking page | ⚠️ Partial | Claimed but no preview |
| Multiple event types per stage | ❓ Unknown | Not mentioned |

**Lena's reaction:** "Round-Robin, kostenlos, DSGVO — das ist fast zu gut um wahr zu sein. Bei Calendly zahlen wir €128/Monat für 8 Interviewer. Wenn das hier funktioniert, sparen wir sofort. Aber warum kostenlos? 'Community-Projekt' macht mich nervös — wird das in 6 Monaten noch existieren? Ich probiere es sofort, aber ich muss sicherstellen, dass automatische Erinnerungen funktionieren, sonst steigt unsere No-Show-Rate."

**Expectation gaps found:** 2 (reminder unclear, sustainability concern)
**Dealbreakers triggered:** 0

---

## Screen 2: Registration Page (https://zeitplanr.de/auth/register)

### What the page shows:
- Fields: Full name, email (business only — Gmail/GMX rejected), password, password confirmation
- DSGVO consent checkbox with privacy policy link
- "Konto erstellen" (Create Account) button
- No Google OAuth signup option
- Single-step process

### Cross-Persona Evaluation

| Expectation | Jan | Petra | Anna | David | Lena |
|------------|:---:|:---:|:---:|:---:|:---:|
| Quick signup (<2 min) | ✅ | ✅ | ✅ | ✅ | ✅ |
| Google OAuth option | ❌ | N/A | ❌ | ❌ | ❌ |
| Business email required | ✅ | ✅ | ✅ | ⚠️* | ✅ |
| DSGVO consent checkbox | ✅ | ✅ | ✅ | ✅ | ✅ |
| German language | ✅ | ✅ | ✅ | ✅ | ✅ |

*David uses a custom domain (david@davidkim.de) — fine. But freelancers sometimes use Gmail for business.

**FINDING:** No Google OAuth is a friction point for Jan (developer, expects OAuth everywhere) and David (efficiency-focused freelancer). For Petra, email/password is actually preferred (her IT doesn't allow OAuth to unknown services). Not a dealbreaker for anyone, but adds 30 seconds of unnecessary friction.

**FINDING:** Business email enforcement blocks freelancers using Gmail for business. David might hit this if he uses a Gmail address. Edge case but worth noting.

---

## Summary: Landing Page + Registration Readiness

### Per-Persona Readiness Scores (Landing Page Only)

| Persona | Score | Status | Key Risk |
|---------|-------|--------|----------|
| **Jan** (Tech startup) | 85% | 🟢 GREEN | Minor: no demo preview, no OAuth |
| **Petra** (Mittelstand/Outlook) | 60% | 🟡 YELLOW | Outlook support buried, no testimonials, "Community-Projekt" label |
| **Anna** (Exec Assistant) | 45% | 🔴 RED | Core use case (multi-calendar) not addressed on landing page |
| **David** (Freelancer) | 70% | 🟡 YELLOW | No timezone mention, no Zoom |
| **Lena** (HR Recruiter) | 80% | 🟢 GREEN | Strong fit, sustainability concern |

### Top 5 Findings (Prioritized by Impact)

1. **🔴 CRITICAL: Multi-calendar / EA use case invisible.** Anna's entire workflow (managing 3 Partners' calendars) is not mentioned. If this feature exists, it needs landing page real estate. If it doesn't, this persona segment is lost.

2. **🟡 HIGH: Outlook/Exchange support buried.** Petra (Mittelstand) almost bounced. "CalDAV & Outlook" is listed in features but the hero, comparison table, and CTA all scream Google. The DACH Mittelstand market is 70%+ Microsoft. This needs equal billing.

3. **🟡 HIGH: No customer references or testimonials.** "Community-Projekt" + zero logos/quotes = trust gap. Petra won't propose this to her IT department. Lena worries about sustainability. Even one Mittelstand logo would transform credibility.

4. **🟡 MEDIUM: Timezone handling not mentioned.** For a scheduling tool, this is table-stakes. David (4 timezones) noticed its absence. Should be a feature card.

5. **🟡 MEDIUM: No Zoom integration.** David's US/Asia clients use Zoom. Google Meet + Jitsi covers part of the market but not enterprise/international.

### Awaiting: Authenticated Experience Screenshots

To complete the walkthrough, I need to evaluate:
- [ ] Dashboard (first screen after login)
- [ ] Event type creation flow
- [ ] Availability settings
- [ ] Public booking page (guest view)
- [ ] Team/round-robin settings
- [ ] Calendar sync settings (Google + Outlook configuration)

Please provide screenshots or give me an alternative way to access the authenticated pages.
