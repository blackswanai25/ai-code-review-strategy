---
product: zuschlagr
date: 2026-04-08
personas_count: 5
phase: expectation-mapping
---

# Zuschlagr — Phase 1: Expectation Mapping

Pre-exposure expectations from 5 German public procurement personas, articulated before seeing the product.

---

## Dr. Andrea Fischer — Leiterin Vergabestelle at Stadtverwaltung Freiburg

### Before I see this tool, I expect:

**First Screen (what should greet me):**
1. A dashboard showing all my active Vergabeverfahren organized by status — Submission, Wertung, Zuschlag, Abschluss — so I see immediately where each procedure stands
2. Deadlines and pending actions highlighted in red or amber, because missed Fristen are non-negotiable in Vergaberecht
3. Team assignments per Verfahren — which Sachbearbeiter owns it, which Fachgutachter are still outstanding — so I can intervene before bottlenecks become problems

**Within 2 minutes of signing up, I should be able to:**
1. Create a Vergabeverfahren, enter the Bewertungskriterien from my Bekanntmachung, and see a Bewertungsmatrix generated that exactly mirrors those criteria and their Gewichtung
2. Understand where my data is hosted — I need to see "EU" or "Frankfurt" prominently, not buried in a legal footnote I have to hunt for
3. Invite one of my Sachbearbeiter to a test Verfahren so I can see how the multi-user workflow works before committing my team

**What would make me trust this tool immediately:**
1. A Bewertungsmatrix that uses the exact Wortlaut from my Bekanntmachung criteria, not AI-paraphrased versions — if even one word differs, the entire Zuschlagsentscheidung is angreifbar
2. A visible, detailed Audit-Trail showing every scoring action with timestamp, user, and justification — the kind of trail that would survive a Nachprüfungsverfahren
3. References to other Kommunalverwaltungen already using the tool — if Mannheim or Stuttgart uses it, I know the IT-Sicherheit and Vergaberecht questions have been answered

**What would make me close the tab within 30 seconds:**
1. The tool uses "Du" instead of "Sie" — this is an official government procurement tool, not a startup playground
2. Any indication that data is processed outside the EU — my IT-Sicherheitsbeauftragter will kill this before I even finish the demo
3. AI-generated scores with no explanation or audit trail — if I cannot trace exactly how a score was derived, step by step, reproducibly, this tool creates legal risk instead of reducing it

**My #1 job this tool MUST do better than my current approach:**
Generating a legally defensible Bewertungsmatrix that consolidates multiple evaluator scores without copy-paste errors. Currently my team builds this in Excel — formulas break, versions diverge, Rechnungsprüfer find inconsistencies months later, and we spend days reconstructing what happened. The tool must produce a Bewertungsmatrix that is correct, complete, traceable, and exportable to PDF for the Vergabeausschuss on the first try.

**What "good enough" looks like for me:**
The tool reliably produces a consolidated Bewertungsmatrix with correct weighted scores, a complete audit trail, and exports a Vergabevermerk draft that my Sachbearbeiter only needs to review and adjust rather than write from scratch. If it saves my team 50% of the time they currently spend on Excel-based evaluation while producing zero additional audit findings from the GPA, it is good enough.

**What would make me recommend this to a colleague:**
If, during our next GPA audit, the Rechnungsprüferin pulls up our Vergabevermerk and Bewertungsmatrix and says "this is the cleanest documentation I have seen from any Kommune" — that is the moment I pick up the phone and call my counterparts in Mannheim and Heidelberg.

**What would make me cancel after the first month:**
If my Sachbearbeiter still need to export to Excel to "fix" things the tool cannot handle — different Wertungsmethoden, custom Gewichtungsmodelle, or if the Vergabevermerk export is so generic it needs to be rewritten from scratch. If it adds a step instead of removing one, it is dead.

**My biggest fear about trying this tool:**
That the AI component makes the evaluation less transparent, not more. If a Bieter files a Nachprüfungsantrag and we have to explain our Zuschlagsentscheidung before the Vergabekammer, and the answer is "the AI calculated it" — I will be personally responsible for a Vergabefehler that could void a multi-million euro contract. My career is on the line.

**Features I expect but won't explicitly ask for:**
1. 4-Augen-Prinzip enforcement — the tool should require a second sign-off before any Zuschlagsentscheidung is finalized, because that is how every Vergabestelle in Germany works
2. Automatic version control — every change to a Bewertungsmatrix creates a new version with a timestamp, because that is what auditors expect
3. Role-based access control that distinguishes between Vergabestellenleitung, Sachbearbeiter, Fachgutachter, and Prüfer — because these roles have fundamentally different permissions in every Vergabeverfahren

---

## Markus Hoffmann — Sachbearbeiter Vergabe at Bayerisches Staatsministerium für Wohnen, Bau und Verkehr

### Before I see this tool, I expect:

**First Screen (what should greet me):**
1. My active Vergabeverfahren listed by deadline urgency — the one where Zuschlag is due Friday must be at the top, not alphabetically buried under some infrastructure project from last month
2. A clear status indicator per Verfahren: "Warte auf Wertungsbögen von Koch, Müller" or "Alle Wertungen eingegangen — Konsolidierung ausstehend" — I need to see at a glance who is holding things up
3. A count of pending actions that I personally need to take, not a generic feed of everything happening across the ministry

**Within 2 minutes of signing up, I should be able to:**
1. Create a new Vergabeverfahren, select the applicable Wertungsmethode (Richtwertmethode, erweiterte Richtwertmethode, UfAB, Schulnotensystem), and enter the criteria from my Bekanntmachung
2. Invite my 5 Fachgutachter by email so they can access their individual Wertungsbögen without needing ministry IT to install anything on their machines
3. See a preview of the consolidated Bewertungsmatrix — even if empty — so I know what the final output will look like before I invest hours setting up the full Verfahren

**What would make me trust this tool immediately:**
1. It offers multiple Wertungsmethoden out of the box and lets me configure them precisely — Richtwertmethode with Kennzahl Z = L/P, UfAB-Methode with Leistungspunkten, Schulnotensystem 1-5 or 1-6 — because every Vergabestelle in Germany uses something slightly different
2. It runs entirely in the browser with no installation — my ministry IT will reject any tool that requires local software deployment, full stop
3. BSI-compliant data hosting in Germany — I need to see this stated explicitly, not just "EU"

**What would make me close the tab within 30 seconds:**
1. Only one Wertungsmethode is available — if I cannot use Richtwertmethode for my VOB-Verfahren and UfAB for my IT-Vergaben, this tool covers maybe 30% of my work
2. Fachgutachter need to create accounts with ministry-level onboarding — my evaluators are external engineers; they will not fill out a 3-page registration form
3. No Begründungsfeld per Kriterium — every score needs a written justification. If the tool treats scoring as just picking a number, it does not understand German Vergaberecht

**My #1 job this tool MUST do better than my current approach:**
Consolidating Wertungsbögen from 5 different Fachgutachter into one consistent Bewertungsmatrix. Right now I receive 5 Excel files, each with slightly different formatting, copy scores by hand into a master sheet, recalculate weighted averages, and pray I did not transpose a number. Last quarter I found a copy-paste error after the Vergabevermerk was already signed — we had to redo the entire evaluation. The tool must collect individual scores in a structured way and consolidate them automatically with zero manual data entry.

**What "good enough" looks like for me:**
I set up the Verfahren once, my Fachgutachter score in the tool, and I get a consolidated Bewertungsmatrix plus a Vergabevermerk draft with one click. Even if the Vergabevermerk draft needs editing, eliminating the Excel consolidation nightmare alone justifies the tool.

**What would make me recommend this to a colleague:**
When a Fachgutachter is 3 days late with their Wertungsbogen and the tool automatically sends a reminder email — and I see the scores arrive the next morning without me having to write a single follow-up email. That is the moment this tool goes from "nice" to "essential."

**What would make me cancel after the first month:**
If Fachgutachter refuse to use it because the interface is confusing or registration is complicated. My evaluators are engineers and architects, not procurement specialists. If they push back and demand "just send me the Excel like before," I am back to square one but now paying for a tool nobody uses.

**My biggest fear about trying this tool:**
That I invest time migrating my active Verfahren into the tool, and then discover mid-evaluation that the Wertungsmethode does not work as expected — wrong formula, wrong Gewichtung, wrong consolidation logic — and I have to fall back to Excel under time pressure with a Zuschlagsfrist breathing down my neck.

**Features I expect but won't explicitly ask for:**
1. Deadline management with automatic reminders to Fachgutachter — because chasing people is 40% of my job and any procurement tool should know this
2. A way to handle Nachforderungen (requesting missing documents from bidders) within the evaluation workflow, because this happens in nearly every Verfahren
3. Offline capability or at minimum reliable auto-save — because the ministry VPN drops connections regularly and losing an hour of work is unacceptable

---

## Claudia Braun — Vergaberechtsexpertin / Juristin at Stadtwerke Karlsruhe GmbH

### Before I see this tool, I expect:

**First Screen (what should greet me):**
1. I do not need a dashboard. I need to land directly on the specific Bewertungsmatrix I have been asked to review for legal compliance — send me a link, I click it, I see the evaluation
2. A clear indication of which Rechtsrahmen applies to this Verfahren — VgV, SektVO, VOB/A, UVgO — displayed prominently, because the legal requirements differ fundamentally between these frameworks
3. A side-by-side view: Bekanntmachung criteria on the left, Bewertungsmatrix on the right — so I can verify Konsistenz in seconds instead of switching between two PDF windows

**Within 2 minutes of signing up, I should be able to:**
1. Open a completed Bewertungsmatrix and verify that every Zuschlagskriterium from the Bekanntmachung appears in the Matrix with identical wording and correct Gewichtung
2. Check whether each Einzelbewertung has a legally sufficient Begründung — not just "gut" or "befriedigend" but a substantive justification that would survive Vergabekammer scrutiny
3. See which legal framework the evaluation follows and whether the tool has applied the correct procedural rules (SektVO for my Stadtwerke, not VgV)

**What would make me trust this tool immediately:**
1. Correct and specific Paragraphenverweise — when the tool references scoring methodology, it cites § 127 GWB, § 58 VgV, or § 52 SektVO as appropriate, not generic "according to procurement law"
2. The tool actively flags inconsistencies between Bekanntmachung and Bewertungsmatrix — different wording, missing criteria, changed Gewichtung — because these are the errors that trigger Nachprüfungsverfahren
3. Evidence that a Vergaberechts-Jurist was involved in developing the legal logic — a name, a legal advisory board, a published methodology document — not just "AI-powered"

**What would make me close the tab within 30 seconds:**
1. The tool applies VgV rules to my Sektorenauftraggeber-Verfahren — if it does not even ask which Rechtsrahmen applies, it is legally ignorant and therefore dangerous
2. AI-generated legal statements without Quellenangaben — "This evaluation complies with procurement law" means nothing without citing specific paragraphs
3. Informal language in the generated Vergabevermerk — Vergaberecht documents have a specific formal register. If the tool writes like a blog post, it produces legally unusable output

**My #1 job this tool MUST do better than my current approach:**
Checking consistency between the Bekanntmachung and the Bewertungsmatrix. Currently I print both documents, lay them side by side, and manually compare every criterion, every Gewichtung percentage, every sub-criterion — word by word. It takes 45 minutes per Verfahren and is the single most tedious yet most legally critical task I perform. One missed discrepancy and the entire Vergabeverfahren is anfechtbar. The tool must automate this comparison with 100% reliability.

**What "good enough" looks like for me:**
The tool catches every discrepancy between Bekanntmachung and Bewertungsmatrix automatically. It flags Begründungen that are too short or too generic. And the Vergabevermerk template follows the correct legal structure for the applicable Rechtsrahmen. I will still review everything myself — but the tool does the initial check that currently takes me 45 minutes in 30 seconds.

**What would make me recommend this to a colleague:**
If a Bieter files a Rüge claiming the evaluation criteria were inconsistent with the Bekanntmachung, and I can open the tool, show the automatic consistency check with green checkmarks, and respond within 24 hours with a legally airtight Nichtabhilfeentscheidung — that efficiency under pressure is what would make me an evangelist.

**What would make me cancel after the first month:**
If the legal references are wrong or outdated. Vergaberecht changes frequently — OLG decisions, VK rulings, GWB amendments. If the tool cites a paragraph number that was renumbered in the last Vergaberechtsmodernisierungsgesetz, it creates the exact kind of error I am supposed to prevent.

**My biggest fear about trying this tool:**
That my Fachabteilungen start trusting the AI's legal compliance signals and stop sending evaluations to me for review. The tool should support my work, not replace it. If people start thinking "the tool said it's compliant, we don't need Claudia to check" — and then a Nachprüfungsantrag succeeds because the AI missed a SektVO-specific requirement — the liability falls on the organization, and ultimately on me for not having insisted on manual review.

**Features I expect but won't explicitly ask for:**
1. A clear distinction between AI-suggested and human-confirmed legal assessments — because in Vergaberecht, only a qualified jurist can make binding legal determinations
2. Changelog for every Bewertungsmatrix modification with legal impact analysis — because even a small wording change in a criterion can change the legal defensibility of the entire evaluation
3. Support for the Sektorenverordnung alongside VgV and VOB — because 90% of procurement tools are built for classical Vergabe and completely ignore Sektorenauftraggeber, which is my entire professional reality

---

## Stefan Koch — Technischer Prüfer / Fachgutachter at Bundesanstalt für Straßenwesen (BASt)

### Before I see this tool, I expect:

**First Screen (what should greet me):**
1. A list showing only the proposals assigned to me for evaluation — I do not want to see the full Vergabeverfahren overview, only my part of the work
2. My scoring progress per proposal — "Kriterium 1: bewertet, Kriterium 2: bewertet, Kriterium 3: ausstehend" — so I know exactly where I left off
3. Absolutely no visibility into how other Fachgutachter scored — not a hint, not an average, not a "3 of 5 evaluators completed." My evaluation must be completely independent

**Within 2 minutes of signing up, I should be able to:**
1. Open a proposal PDF and begin scoring against the first criterion with a structured Wertungsbogen that matches the published Zuschlagskriterien
2. Write a Begründung for my score and save it as a draft that I can return to tomorrow — without fear that a browser crash loses 30 minutes of work
3. Understand the scoring scale and method being used — is this Schulnoten 1-5? Punkteskala 0-10? Richtwertmethode? I need to see this immediately, not discover halfway through that I used the wrong scale

**What would make me trust this tool immediately:**
1. Explicit evaluator isolation — a clear message like "Sie sehen ausschließlich Ihre eigene Bewertung. Andere Gutachter-Bewertungen sind bis zum Abschluss der Konsolidierung nicht einsehbar" — because if there is any chance of Bewertungskontamination, I refuse to use the tool
2. Reliable auto-save with visible confirmation — a timestamp showing "Entwurf gespeichert: 14:32 Uhr" — because I evaluate 100-page proposals and I will not risk losing detailed Begründungen
3. The scoring form exactly mirrors the criteria from the Bekanntmachung — same wording, same order, same Gewichtung — because scoring against different criteria than what was published is a Vergabefehler

**What would make me close the tab within 30 seconds:**
1. I can see a summary, average, or any indication of other evaluators' scores — this is not a preference, it is a legal requirement. Evaluator independence is sacrosanct in German Vergaberecht
2. The tool does not auto-save — if I write a 500-word technical Begründung and the browser crashes and it is gone, I will never open this tool again
3. I need to understand procurement law to use the tool — I am an engineer. Show me the criteria, give me a scoring form, let me write my justification. Do not make me navigate procurement workflows

**My #1 job this tool MUST do better than my current approach:**
Structured scoring with proper documentation. Currently I receive a Word template Wertungsbogen via email, open 4 proposal PDFs side by side on my monitor, flip through 100+ pages to find the relevant sections for each criterion, type my scores and Begründungen into Word, and email the completed form back. The tool must let me score criterion by criterion with the proposal accessible alongside the scoring form, ideally highlighting which sections of the proposal are relevant to each criterion.

**What "good enough" looks like for me:**
A clean, simple scoring form that matches the criteria. Auto-save that works. A way to view the proposal PDF without leaving the scoring interface. And when I click "Abschließen und einreichen," my Wertungsbogen is submitted to the Vergabestelle with zero additional steps. If it feels simpler than the Word template, I will use it.

**What would make me recommend this to a colleague:**
If the tool uses AI to highlight the exact sections in a 120-page technical proposal that are relevant to each scoring criterion — so instead of reading the entire document for every criterion, I can jump directly to the relevant passages. That would save me hours per evaluation and transform the most tedious part of my work.

**What would make me cancel after the first month:**
If the tool is more cumbersome than the Word template. If I need to click through 7 screens to do what I currently do in one document. If submission requires 3 confirmations and a password. The Word template is simple and offline — any replacement must be simpler, or I go back.

**My biggest fear about trying this tool:**
That the AI pre-fills scores or suggests ratings based on analyzing the proposals, and this is visible before I form my own independent judgment. Even a subtle hint — a highlighted section, a suggested score, a "similar proposals were rated X" — compromises my evaluation independence. I need the AI to assist after I score, not before.

**Features I expect but won't explicitly ask for:**
1. The ability to attach direct quotes from the proposal as evidence for my scoring — because a Begründung that says "methodology is good" is worthless, but one that says "Bieter describes on page 47 a three-phase approach that addresses all requirements" is defensible
2. A PDF export of my completed Wertungsbogen for my own records — because I need documentation of what I submitted in case questions arise months later
3. A simple, uncluttered interface that does not assume I know Vergaberecht terminology — label things "Ihre Bewertung," "Begründung," "Einreichen" — not "Wertungsmatrixkonsolidierung" or "Zuschlagsentscheidungsvorbereitung"

---

## Ingrid Neumann — Rechnungsprüferin at Gemeindeprüfungsanstalt Baden-Württemberg (GPA)

### Before I see this tool, I expect:

**First Screen (what should greet me):**
1. A read-only Prüfungsansicht (audit view) of a completed Vergabeverfahren — I am not here to create or score anything, I am here to verify that everything was done correctly
2. A complete chronological Audit-Trail: who created the Verfahren, who defined the criteria, who scored what and when, who consolidated, who signed off — every action with a timestamp and user ID
3. An immediate overview showing whether all required elements are present: Bekanntmachung criteria defined, all evaluator scores submitted, Vergabevermerk completed, Zuschlagsentscheidung documented

**Within 2 minutes of accessing a Verfahren, I should be able to:**
1. Verify that the Bewertungskriterien in the Matrix exactly match the Bekanntmachung — this is the number one finding in 40% of my audits, and if the tool does this check for me, it saves me an hour per Verfahren
2. Check that every Einzelbewertung has a documented Begründung and that no scores were changed after the Vergabevermerk was signed
3. Export the complete Verfahrensakte as a PDF or ZIP file that I can attach to my Prüfungsmitteilung — because my audit documentation must be self-contained and independent of the tool

**What would make me trust this tool immediately:**
1. Immutable records — once a Wertungsbogen is submitted, it cannot be edited without creating a new, auditable version with a documented reason for the change. If scores can be silently altered, the entire audit trail is worthless
2. Complete timestamps on every action — not just "bewertet am 15.03.2026" but "bewertet am 15.03.2026, 14:23:07 Uhr durch Koch, Stefan (Technischer Prüfer)" — this level of detail is what I need
3. A compliance checklist that maps the Verfahren against VgV/VOB/GWB requirements — showing which procedural steps were completed and which are missing — because this is literally what I produce manually for every audit

**What would make me close the tab within 30 seconds:**
1. No audit trail — if I cannot see who did what and when, this tool is not just useless for my work, it is actively harmful because it creates a false sense of documentation
2. The ability for anyone to edit past evaluations without a version trail — if a Sachbearbeiter can change a score from 3 to 4 after the Zuschlagsentscheidung and there is no trace, this tool enables fraud rather than preventing it
3. AI-generated scores that were accepted without documented human review — if I see "AI Score: 8/10" without a human evaluator confirming and justifying that score, this is an automatic finding in my audit report

**My #1 job this tool MUST do better than my current approach:**
Reconstructing the evaluation logic from incomplete documentation. Currently, I receive a box of files (sometimes literally paper) from a municipality, spend half a day organizing them, then manually trace: Did the criteria match the Bekanntmachung? Were all evaluators' scores documented? Was the consolidation arithmetic correct? Were Begründungen provided? The tool must produce a complete, self-contained, exportable documentation package where every question I typically ask during an audit is already answered by the audit trail.

**What "good enough" looks like for me:**
When I open the audit view of a Verfahren, I can answer my standard 15-point Prüfungskatalog within 30 minutes instead of 3 hours. Every evaluator's score is documented with a timestamp and Begründung. The Bewertungsmatrix arithmetic is verifiably correct. And I can export everything as a PDF that stands on its own without needing access to the tool.

**What would make me recommend this to a colleague:**
If, after auditing 10 Verfahren conducted in this tool, I have zero documentation-related findings — no missing Begründungen, no inconsistent criteria, no unexplained scoring changes. If the tool eliminates the documentation problems that account for 70% of my current findings, I would recommend it to every Kommune in Baden-Württemberg.

**What would make me cancel after the first month:**
If the audit trail is incomplete or if the tool allows data to be modified without proper versioning. Also if the export is a pretty summary rather than a complete record — I need the raw data, every version, every timestamp, every Begründung. A polished PDF that hides the messy details is the opposite of what I need.

**My biggest fear about trying this tool:**
That municipalities adopt this tool and it becomes harder to audit, not easier. If the tool introduces AI-assisted evaluations with opaque logic, or if the digital format makes it easier to quietly "clean up" evaluations after the fact, I am now auditing a black box instead of a paper trail. At least with Excel files, I can see the formula bar. With AI, I cannot see the reasoning — and "the AI recommended this score" is not a legally sufficient Begründung.

**Features I expect but won't explicitly ask for:**
1. A dedicated auditor role with read-only access that cannot be circumvented — because my access must never create the possibility that I influenced or modified the evaluation
2. Data retention and archival compliance — Vergabeunterlagen must be retained for years (§ 8 VgV: 4 years, longer for EU-funded projects), and the tool must guarantee this or support export for external archival
3. A comparison function showing the original submitted scores versus any subsequent changes, with reasons — because "version 2" means nothing without knowing exactly what changed and why

---

*Report generated as part of Phase 1 (Expectation Mapping) of the UX testing framework. These expectations represent pre-exposure assumptions and should be validated against actual product experience in Phase 2.*
