# Project plan: 26 weeks, alongside an M.Tech

Status: plan, 27 Nov 2026. Week 1 starts Monday 30 Nov 2026; week 26 ends Sunday 30 May 2027.
Labels: **FACT** (linked), **ESTIMATE**, **OPINION**, **UNVERIFIED**. Hours and durations are **ESTIMATES**.
Related: [business_plan.md](business_plan.md), [mvp_architecture.md](mvp_architecture.md), [paper_plan.md](paper_plan.md), [privacy_design.md](privacy_design.md), [alert_message_spec.md](alert_message_spec.md).

## 1. Assumptions (change these first if they are wrong)
1. The founder has **10-12 hours a week** for this, and **4-6 hours** in exam weeks. Semester and exam dates are `[to fill]`; this plan assumes light weeks 4-5 (end-semester, December) and 21-23 (April-May). See [questions_for_founder.md](questions_for_founder.md).
2. The M.Tech supervisor is willing to back the paper and the ethics application `[to confirm]`.
3. No co-founder; one unpaid or project-credit intern may join from week 9.
4. Budget for the 6 months: about ₹1.2 lakh direct costs ([mvp_architecture.md §5](mvp_architecture.md#5-costs-estimates-in-inr-not-quotes)) plus registration and legal `[to fill]`. Funded from savings or a grant.
5. The business pilot does **not** need ethics or police approval (no human-participant research, no alerts to the public). The alert study does.

## 2. Workstreams
| Code | Stream | Share of time (ESTIMATE) |
|---|---|---|
| C | Customer: operator, hospital and crew interviews; pilot sales | 35% |
| B | Build: crew app, dispatch board, reports, alert | 35% |
| F | Funding and company: incubator, PRAYAS, incorporation, DPIIT | 10% |
| E | Ethics and legal: IEC application, lawyer questions | 5% |
| P | Paper: benchmark, usability study, writing | 15% |

## 3. Decision gates and kill criteria
| Gate | Week | Question | Pass (ESTIMATE thresholds) | Kill or change |
|---|---|---|---|---|
| **G1** | 8 | Do operators have a pain they would pay to fix? | ≥8 operator interviews; ≥4 describe H1 or H2 ([business_plan.md §1.2](business_plan.md#12-problem-hypotheses-to-test-in-interviews-not-yet-evidence)) unprompted; ≥2 agree to a pilot meeting; stated price range overlaps ₹1,000-2,000 per ambulance per month | **K1:** fewer than 2 of 8 show the pain → stop the operator product; keep only the paper. If the pain is real but the price is far lower → re-scope (reports-only product, or sell to hospitals) |
| **G2** | 12 | Will one operator commit? | One signed pilot agreement for ≥5 ambulances with a named contact | **K2:** none by week 14 → pause building; do 6 more interviews in a second segment (hospital fleets); if still none by week 18, stop the business |
| **G3** | 17 | Is the product used? | ≥80% of the pilot's emergency runs tracked over 2 weeks; dispatcher uses the board ≥4 days a week | **K3:** under 50% after fixes → find why (phones, crew habits, value); one more 3-week try, then stop |
| **G-alert** | 15 | Is the alert safe and fast enough to test with people? | Median latency under 5 s, p95 under 15 s, ≥95% delivery on 5 brands ([mvp_architecture.md §6](mvp_architecture.md#6-eight-week-build-plan-solo)); ethics approval in hand | **K4:** fail → no human tests; publish the benchmark only; the alert stays out of the product |
| **G4** | 26 | Will they pay? | Signed order or invoice at ≥₹1,000 per ambulance per month | **K5:** a clear "no" with reasons → stop or pivot to the reason given; do not extend the free pilot more than once |

Kill criteria are commitments made now, before results, so the founder does not keep a weak business going for 2 years. **OPINION.**

## 4. Week-by-week plan

Hours per week shown as **ESTIMATE**. "Done when" is the check for the week.

| Wk | Dates (Mon) | Hrs | Main tasks | Done when |
|---|---|---|---|---|
| 1 | 30 Nov | 10 | C: build a list of 30 Hyderabad operators and 10 hospitals. E: ask supervisor about the institute ethics committee (IEC), forms, dates. F: read CIE and i-TIC PRAYAS pages; note open calls | List in a sheet; IEC process known |
| 2 | 7 Dec | 10 | C: write interview script (§5); book 5 interviews. B: OSRM running on a Telangana extract | 5 interviews booked; a route returns segments |
| 3 | 14 Dec | 10 | C: 3 interviews. E: draft ethics application for the lab usability study (RQ2) and the benchmark. B: message format | 3 notes written within 24 h of each call |
| 4 | 21 Dec | 5 | Exams (assumed). C: 2 interviews by phone | 5 interviews total |
| 5 | 28 Dec | 5 | Exams or break (assumed). E: submit ethics application. C: email RED.Health and Medulance for a research or partnership meeting | Application submitted |
| 6 | 4 Jan | 12 | C: 3 interviews (include 2 crews). B: crew app v0 (start/stop run, GPS, signing) | Signed positions reach the backend |
| 7 | 11 Jan | 12 | C: 2 operator + 2 hospital interviews. B: dispatch board v0 (live map, run list) | Board shows a test ambulance live |
| 8 | 18 Jan | 12 | **Gate G1.** C: summarise interviews (pains, prices, objections). Decide go, re-scope or kill | Gate note committed in `docs/` |
| 9 | 25 Jan | 12 | F: apply to CIE and/or i-TIC (incubation + PRAYAS if open). B: ETA-to-hospital link. C: pilot proposal to top 2-3 operators | Applications sent; proposals sent |
| 10 | 1 Feb | 12 | C: pilot meetings; draft one-page pilot agreement (processor terms). E: send lawyer questions ([privacy_design.md §8](privacy_design.md#8-questions-for-a-lawyer)) to an incubator or law-clinic lawyer | Draft agreement ready |
| 11 | 8 Feb | 12 | B: response-time report v0 (CSV + PDF). B: corridor builder and signer, MQTT broker | Report generated from test runs |
| 12 | 15 Feb | 12 | **Gate G2.** C: sign a pilot agreement. F: decide on incorporation (needed for SISFS and DPIIT; [myScheme SISFS](https://myscheme.gov.in/schemes/sisfs-fs)) | Signed agreement or K2 path |
| 13 | 22 Feb | 12 | C/B: install crew app on pilot ambulances; train crews and dispatcher; alerts off | All pilot phones reporting |
| 14 | 1 Mar | 12 | B: fix pilot bugs; driver app v0 (foreground service, local matching, English voice) | Walking test alerts at the right distance |
| 15 | 8 Mar | 12 | **Gate G-alert.** P: latency and battery benchmark on 5 brands (RQ1) | Table of p50/p95/p99 per phone |
| 16 | 15 Mar | 12 | C: first weekly check-in with the operator. B: 4 languages (after native review), banner, vibration, fail-silent tests | Unit tests pass for stale, expired and bad-signature cases |
| 17 | 22 Mar | 12 | **Gate G3.** C: usage review with the operator. P: lab usability study setup (if ethics approved) | Usage numbers recorded |
| 18 | 29 Mar | 12 | C: first monthly response-time report delivered. P: run lab study sessions (10 of 20) | Report delivered; 10 sessions |
| 19 | 5 Apr | 12 | P: lab study sessions (20 of 20). C: ask the operator to use the report with a client | 20 sessions done |
| 20 | 12 Apr | 12 | P: analyse RQ1 and RQ2. If approvals exist (ethics, operator, police in writing), start the consented alert field pilot; otherwise skip | Analysis notebook committed |
| 21 | 19 Apr | 6 | Exams (assumed). C: weekly check-in only | Check-in done |
| 22 | 26 Apr | 6 | Exams (assumed). P: paper outline and figures | Outline committed |
| 23 | 3 May | 6 | Exams (assumed). C: second monthly report | Report delivered |
| 24 | 10 May | 12 | P: paper draft to supervisor. C: draft pilot report with the operator | Draft sent |
| 25 | 17 May | 12 | C: price conversation; send order form. F: if incorporated, apply for DPIIT recognition and SISFS via an incubator | Order form sent |
| 26 | 24 May | 12 | **Gate G4.** C: invoice or documented "no". Update [business_plan.md](business_plan.md) §10 with real numbers. P: choose venue and submit if ready | Gate note; plan updated |

Pilot calendar: the operator pilot starts about week 13 and its day 90 falls about week 26.

## 5. Operator interview script (30 minutes)
1. Tell me about the last emergency run. Who took the call, how was the ambulance chosen, how did the crew know where to go?
2. How do you record a run today? Can you show me?
3. Has a hospital, company or government body ever asked you for response times? What did you send?
4. What software or GPS do you pay for today? How much per vehicle per month?
5. What goes wrong most often in dispatch?
6. Do crews complain about traffic not making way? How often, and where?
7. (Only at the end) Show a 2-minute demo or mock-up. "If this cost ₹X per ambulance per month, would you try it for 90 days for free and then decide?" Ask the four price questions (too cheap, good value, expensive, too expensive).
8. Who else should I talk to?

Rules: no promises, no invented features, write notes within 24 hours, anonymise names in the repo, never record without consent.

## 6. Ethics and legal track
| Step | Week | Note |
|---|---|---|
| Find which ethics body applies (institute IEC or IRB) | 1 | **UNVERIFIED** which body; ask supervisor |
| Submit application for the benchmark (if needed) and lab usability study | 5 | Uses [alert_message_spec.md §8](alert_message_spec.md#8-usability-test-plan-20-participants) and [paper_plan.md §7](paper_plan.md#7-ethics-and-approvals) |
| Approval expected | about 12-16 | **ESTIMATE**; depends on committee dates |
| Lawyer questions sent | 10 | Through incubator legal clinic if possible |
| Field alert pilot | 20+ | Only with ethics approval and written operator and police approval; otherwise dropped |

## 7. Paper track
1. Scope: RQ1 (latency, battery) and RQ2 (message design lab study). RQ3 (SUMO) only if time remains, labelled simulated. RQ4 (field) is optional ([paper_plan.md §2](paper_plan.md#2-research-questions)).
2. Do the systematic literature search in weeks 9-12 before claiming any gap.
3. Venue: `[to fill with supervisor]`. Candidate types: an Indian systems or computing-for-development venue, or an intelligent-transport conference or workshop. Deadlines **not checked**.
4. No novelty or patent claims in the paper; report it as an evaluation.

## 8. If time runs out, cut in this order
1. RQ3 simulation.
2. RQ4 field alert pilot.
3. Urdu and Hindi alert audio (keep Telugu and English).
4. Hospital ETA link polish.
5. **Never cut:** operator interviews, gate decisions, the ethics application, the pilot check-ins.
