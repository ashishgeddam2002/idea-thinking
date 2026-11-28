# Project plan: 26 weeks, alongside an M.Tech

Status: plan, updated 28 Nov 2026 with the founder's answers ([questions_for_founder.md](questions_for_founder.md)). Week 1 starts Monday 30 Nov 2026; week 26 ends Sunday 30 May 2027.
Labels: **FACT** (linked), **ESTIMATE**, **OPINION**, **UNVERIFIED**, `[to confirm]` (founder's answer was vague). Hours and durations are **ESTIMATES**.
Related: [business_plan.md](business_plan.md), [mvp_architecture.md](mvp_architecture.md), [paper_plan.md](paper_plan.md), [privacy_design.md](privacy_design.md), [alert_message_spec.md](alert_message_spec.md).

## 1. Assumptions (from the founder's answers; change these first if they are wrong)
1. **Time:** 3rd-semester M.Tech with mostly project work, so the founder says time is "no problem". The plan still budgets **10-12 hours a week** `[to confirm]` and keeps 2 buffer weeks (5 and 22) for exams or thesis deadlines `[to confirm dates]`.
2. **Money: ₹0 of own money.** The only paid tool is the founder's Claude Pro plan. Everything before a grant must be free, borrowed or skipped. Grant-gated steps are marked **[G]**.
3. **Goals:** revenue and the paper have **equal weight** (§4).
4. **Institute:** CBIT (Hyderabad) backs the work "if the paper has enough strength". The ethics committee is not named `[to confirm]`. CBIT has a startup or seed cell `[to confirm name and what it offers; not verified]`.
5. **Skills:** no Android experience; has deployed a website with AI-assisted coding. No sales experience. Speaks English, Hindi and Telugu.
6. **Contacts:** none at any ambulance operator. **All outreach is cold.** Do not plan on warm introductions.
7. **Incorporation:** the founder is willing to incorporate. Do it only after gate G1 passes (fees need a source; `[to fill quote]`).

## 2. Workstreams
| Code | Stream | Share of time (ESTIMATE) |
|---|---|---|
| C | Customer: operator, hospital and crew interviews; pilot sales; mentor | 30% |
| B | Build: web dispatch board, web crew app, reports; later the native Android driver app | 30% |
| P | Paper: literature search, benchmark, usability study, writing | 25% |
| F | Funding and company: CBIT cell, PRAYAS, incorporation, SISFS | 10% |
| E | Ethics and legal: ethics application, lawyer questions, legal check L1 | 5% |

## 3. Decision gates and kill criteria
G2 is set for the **cold-outreach case**: with no contacts, expect about 1 interview per 5-8 cold calls or messages and 6-10 weeks to a first pilot (**ESTIMATE**, no data).

| Gate | Week | Question | Pass (ESTIMATE thresholds) | Kill or change |
|---|---|---|---|---|
| **G1** | 9 | Do operators have a pain they would pay to fix? | ≥8 operator interviews; ≥4 describe H1 or H2 ([business_plan.md §1.2](business_plan.md#12-problem-hypotheses-to-test-in-interviews-not-yet-evidence)) unprompted; ≥2 agree to a pilot meeting; stated price range overlaps ₹1,000-2,000 per ambulance per month | **K1:** fewer than 2 of 8 show the pain → stop the operator product; the paper continues alone. Pain real but price far lower → re-scope (reports only, or hospitals) |
| **G-L1** | 7 | Legal check L1 done? (2020 proviso to reg. 37(1); [alert_message_spec.md §4c](alert_message_spec.md#4c-blocking-legal-check-l1-phone-screens-while-riding-or-driving)) | Gazette text read and, if possible, a lawyer's view | Not done → **no screen for two-wheelers** in any test; voice and vibration only |
| **G2** | 15 | Will one operator commit? | One signed pilot agreement for ≥5 ambulances with a named contact | **K2:** none by week 17 → 6 interviews with hospital fleets; if still none by week 21, stop the business and finish the paper |
| **G-alert** | 16 | Is the native driver app fast and reliable enough to test with people? | Median latency under 5 s, p95 under 15 s, ≥95% delivery on 5 borrowed brands ([mvp_architecture.md §6](mvp_architecture.md#6-build-plan-ai-assisted-no-prior-android-experience)); ethics approval in hand | **K4:** fail → no human tests; publish the benchmark only; the alert stays out of the product |
| **G3** | 20 | Is the product used? | ≥80% of pilot emergency runs tracked over 2 weeks; dispatcher uses the board ≥4 days a week | **K3:** under 50% after fixes → one more 3-week try, then stop |
| **G4** | 26+ | Will they pay? | Signed order at ≥₹1,000 per ambulance per month | **K5:** clear "no" → stop or pivot to the reason; extend a free pilot once at most. If the pilot started late, G4 moves to its day 90 (about week 28) |

Kill criteria are fixed now, before results. **OPINION.**

## 4. Keeping the paper and the business in step
| Shared asset | Business use | Paper use |
|---|---|---|
| Crew app and backend (corridor, signing) | Dispatch, ETA, reports | Corridor source for RQ1 benchmark |
| Native driver app | Optional alert feature (later) | RQ1 latency and battery; RQ2 study app |
| Operator interviews | Product and pricing | Context section (anonymised; with consent) |
| Pilot logs (with operator consent) | Response-time reports | Possible RQ4 data, only with ethics approval |

**If time runs short, cut in this order** (each step protects one business item and one paper item):
1. RQ3 SUMO simulation (paper) and the hospital ED view (business).
2. RQ4 field alert pilot (paper) and the alert feature in the operator pilot (business).
3. Map-style screen variant; keep voice plus arrow only.
4. **Never cut:** operator interviews, gate decisions, the ethics application, RQ1 benchmark, RQ2 lab study, pilot check-ins.

If gate G1 kills the business, the paper continues with RQ1 and RQ2. If the paper's ethics approval stalls, the business pilot continues (it needs no human-participant approval).

## 5. Week-by-week plan
Hours are **ESTIMATES**. **[G]** = needs grant money; if none, use the free fallback shown.

| Wk | Dates (Mon) | Hrs | Main tasks | Done when |
|---|---|---|---|---|
| 1 | 30 Nov | 12 | F: visit CBIT's startup cell `[to confirm name]`: ask about grants, mentors, legal help, incubation, ethics committee. C: build a list of 30 Hyderabad operators and 10 hospitals | Cell visited; list in a sheet |
| 2 | 7 Dec | 12 | C: ask the cell and CBIT alumni office for a **sales or healthcare mentor** (no warm intros assumed). C: write the interview script (§6); start 20 cold contacts (calls, WhatsApp, walk-ins at ambulance stands near hospitals). P: start the literature search | 20 contacts attempted; mentor asked |
| 3 | 14 Dec | 12 | C: 2-3 interviews. E: draft the ethics application (benchmark and lab study). B: set up the web stack (AI-assisted) and OSRM on the laptop | Notes written within 24 h |
| 4 | 21 Dec | 12 | C: 20 more cold contacts; 2-3 interviews. E: legal check L1 starts: find the 2020 gazette notification (CBIT library, egazette from a different network) | 5 interviews total |
| 5 | 28 Dec | 6 | Buffer week `[to confirm exams]`. E: submit ethics application | Application submitted |
| 6 | 4 Jan | 12 | C: 2-3 interviews (include 2 crews). B: web crew app v0 (start/stop run, GPS while screen on) | Test positions reach the backend |
| 7 | 11 Jan | 12 | **G-L1.** E: record legal-check result. C: 2 hospital interviews. B: web dispatch board v0 (live map, run list) | L1 note committed; board shows a test ambulance |
| 8 | 18 Jan | 12 | C: 2-3 operator interviews. F: if the CBIT cell offers a grant or PRAYAS link, apply. P: literature search done | 8+ operator interviews |
| 9 | 25 Jan | 12 | **Gate G1.** C: summarise pains, prices, objections; decide go, re-scope or kill | Gate note in `docs/` |
| 10 | 1 Feb | 12 | F: apply to CIE (IIIT-H) and/or i-TIC (IIT-H) PRAYAS if a call is open. B: ETA-to-hospital link. C: pilot proposal to top 2-3 operators | Applications and proposals sent |
| 11 | 8 Feb | 12 | C: pilot meetings with the mentor if possible; draft one-page pilot agreement. E: lawyer questions via CBIT cell or a free law clinic | Draft agreement |
| 12 | 15 Feb | 12 | B: response-time report v0. B: corridor builder and signer. F: decide on incorporation | Report generated from test runs |
| 13 | 22 Feb | 12 | B: native Android driver app v0 (AI-assisted; foreground service, MQTT, one English voice alert). C: follow up pilot leads | App runs on one borrowed phone |
| 14 | 1 Mar | 12 | B: driver app: local matching, fail-silent rules. C: follow-ups | Walking test alerts at the right distance |
| 15 | 8 Mar | 12 | **Gate G2.** C: sign a pilot agreement (or K2 path). C/B: install web crew app on pilot ambulances (operator's phones) | Signed agreement |
| 16 | 15 Mar | 12 | **G-alert.** P: latency and battery benchmark on 5 borrowed brands (RQ1) | p50/p95/p99 table |
| 17 | 22 Mar | 12 | C: pilot training and first check-in. B: Telugu and Hindi strings (founder reviews; 5-speaker test) | Pilot phones reporting |
| 18 | 29 Mar | 12 | P: lab usability study setup (if ethics approved; volunteers, or ₹300 each **[G]**). C: weekly check-in | Study materials ready |
| 19 | 5 Apr | 12 | P: lab sessions 1-10. C: check-in | 10 sessions |
| 20 | 12 Apr | 12 | **Gate G3.** P: lab sessions 11-20. C: usage review | Usage numbers; 20 sessions |
| 21 | 19 Apr | 12 | P: analyse RQ1 and RQ2. C: first monthly response-time report | Notebook committed; report delivered |
| 22 | 26 Apr | 6 | Buffer week `[to confirm exams]`. C: check-in only | Check-in done |
| 23 | 3 May | 12 | P: paper outline, figures; share with the CBIT supervisor for a strength check | Outline shared |
| 24 | 10 May | 12 | P: paper draft. C: second monthly report | Draft sent |
| 25 | 17 May | 12 | C: draft pilot report with the operator; price conversation. F: if incorporated, apply for DPIIT recognition and SISFS via an incubator | Order form sent |
| 26 | 24 May | 12 | **Gate G4** (or note its new date). Update [business_plan.md](business_plan.md) §10 with real numbers. P: choose venue | Gate note; plan updated |

Pilot calendar: the operator pilot starts about week 15-17 (cold-outreach case), so its day 90 falls about weeks 28-30, after this plan ends. That is expected.

**Realistic slip (ESTIMATE):** with no Android experience and AI-assisted coding, the build tasks may take 1.5-2 times as long. If so, the native driver app (weeks 13-14) slips to weeks 16-18, G-alert and the RQ1 benchmark slip by 3-4 weeks, and the paper draft moves into June 2027. The business pilot does not depend on the native app, so G2 and G3 do not slip with it.

## 6. Operator interview script (30 minutes)
1. Tell me about the last emergency run. Who took the call, how was the ambulance chosen, how did the crew know where to go?
2. How do you record a run today? Can you show me?
3. Has a hospital, company or government body ever asked you for response times? What did you send?
4. What software or GPS do you pay for today? How much per vehicle per month?
5. What goes wrong most often in dispatch?
6. Do crews complain about traffic not making way? How often, and where?
7. (Only at the end) Show a 2-minute mock-up. "If this cost ₹X per ambulance per month, would you try it for 90 days for free and then decide?" Ask the four price questions (too cheap, good value, expensive, too expensive).
8. Who else should I talk to? (With no contacts, this question is how the list grows.)

Rules: no promises, no invented features, notes within 24 hours, anonymise names in the repo, never record without consent. Cold-outreach tips (**OPINION**): go in person to ambulance stands outside large hospitals at quiet hours; say you are a CBIT student researching ambulance response times; ask for 15 minutes, not a sale.

## 7. Ethics and legal track
| Step | Week | Owner | Note |
|---|---|---|---|
| Find which ethics body applies at CBIT | 1 | Founder | `[to confirm]`; ask the supervisor and the startup cell |
| Legal check L1: 2020 proviso to reg. 37(1) | 4-7 | Founder | Blocking for any two-wheeler screen; see [alert_message_spec.md §4c](alert_message_spec.md#4c-blocking-legal-check-l1-phone-screens-while-riding-or-driving) |
| Submit ethics application | 5 | Founder + supervisor | Covers benchmark (if needed) and lab study |
| Approval expected | about 12-16 | Committee | **ESTIMATE** |
| Lawyer questions | 11 | Founder, via CBIT cell or free clinic | [privacy_design.md §8](privacy_design.md#8-questions-for-a-lawyer) |
| Field alert pilot | 21+ | — | Only with ethics approval, written operator and police approval, and insurance **[G]**; otherwise dropped |

## 8. What cannot be done without a grant
| Item | Without a grant | Fallback |
|---|---|---|
| Test phones | Cannot buy | Borrow 5 brands from friends, classmates or a CBIT lab |
| Lab-study payments (₹300 × 20 = ₹6,000, ESTIMATE) | Cannot pay | Unpaid volunteers if the ethics committee allows |
| Rider install incentives and crew stipends | **Impossible** | Dropped from the plan |
| Field alert pilot with public riders | **Impossible** (needs insurance and incentives) | Dropped unless funded |
| Paid lawyer, insurance | **Impossible** | Free clinic or CBIT cell; no field pilot without insurance |
| Company incorporation fees | Probably impossible `[to fill quote]` | Wait for a grant or the CBIT cell's help |
| Cloud server in India | Free tiers only (limits **UNVERIFIED**) | Laptop for development; free tier for the pilot |
| Travel to operators | Only small amounts | Phone and WhatsApp first; walk-ins on routes already travelled |
