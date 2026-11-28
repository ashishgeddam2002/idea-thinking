# Business plan: ambulance operations software, with a give-way alert as a feature

Status: draft for the founder to use when talking to operators, incubators and grant bodies. Written 27 Nov 2026; updated 28 Nov 2026 with the founder's answers ([questions_for_founder.md](questions_for_founder.md)): ₹0 own budget, no operator contacts, no sales or Android experience, CBIT backing, revenue and paper weighted equally.
Labels used throughout: **FACT** (with a link), **ESTIMATE** (a number with its assumptions shown), **OPINION** (a judgement), **UNVERIFIED** (not checked; do not repeat as fact).
**Not legal advice.** Lawyer questions are in [privacy_design.md §8](privacy_design.md#8-questions-for-a-lawyer).
**No novelty or patent claim is made anywhere in this plan.**
Earlier, longer research (linked, not copied): [India ambulance alert evaluation](https://github.com/ashishgeddam2002/BLATTA/blob/claude/ambulance-alert-india-analysis-b8uz09/reports/India%20ambulance%20alert%20evaluation.md) and its [research notes](https://github.com/ashishgeddam2002/BLATTA/tree/claude/ambulance-alert-india-analysis-b8uz09/research_notes/India%20ambulance%20alert%20evaluation).

---

## 0. One-page summary

| | |
|---|---|
| **What we sell** | Phone-based software for private ambulance operators in Hyderabad: dispatch board, live ETA to the receiving hospital, and response-time reports. The crew uses a web app on a phone already in the ambulance (a native Android app later), so no hardware is needed. |
| **The alert** | A give-way alert ("ambulance behind you: move left if safe, or stay where you are") is built in as an opt-in feature and a research pilot. It is **not** the business. |
| **Why the pivot** | Earlier research found that nobody pays drivers to give way, gig platforms publish no partner SDK, and the alert technology has no moat (see §1.3). An operator has a budget and a reason to pay. The driver network does not. |
| **First customers** | Small and mid-size private ambulance operators and hospital in-house fleets in Hyderabad. RED.Health is the best-known Hyderabad operator, but news reports say it already runs its own technology platform (§4), so treat it as a partner or a reference contact, not a sure buyer. |
| **Price** | ₹1,000-2,000 per ambulance per month. **ESTIMATE**, not tested with any buyer. Free 90-day pilot first. |
| **Traction** | None yet. No customers, letters of intent or pilots. `[to fill]` after the interviews. |
| **Ask (now)** | First, whatever CBIT's startup cell offers `[to confirm]`. Then a prototype grant of about ₹10 lakh (**ESTIMATE**) through a NIDHI-PRAYAS centre (CIE at IIIT Hyderabad or i-TIC at IIT Hyderabad), plus incubation. Later: Startup India Seed Fund, once the company is incorporated and a paid pilot exists. No angel round until an operator pays. **Own money: ₹0**, so everything before a grant is free or borrowed. |
| **12-month goal** | Equal weight: one paying operator with at least 10 ambulances and an operator-signed pilot report; and one workshop or conference paper on alert latency and message design, backed by CBIT. |
| **Biggest risks** | (1) Operators may not pay for software they get bundled from trackers or build themselves. (2) The alert creates a duty of care and phone-use legal questions (a two-wheeler screen is blocked until legal check L1 passes). (3) Solo founder with no contacts, no sales experience, no Android experience and no money. |

---

## 1. Problem

### 1.1 Facts
1. Indian law requires drivers to make way for ambulances. MV Act s.194E sets a penalty of up to six months in prison, a ₹10,000 fine, or both, for failing to "draw to the side of the road" ([Indian Kanoon mirror](https://indiankanoon.org/doc/132499746/)). Driving Regulations 2017, reg. 27(5) says to drive "to the left as close as practicable to the kerb" and stop if required ([reg. 27(5)](https://indiankanoon.org/doc/21177923/)). Details: [research_gaps.md §1](research_gaps.md#1-exact-statute-text-priority-1).
2. Private ambulance operators run their own fleets and dispatch. RED.Health, based in Hyderabad, raised a USD 20 million Series B in May 2024 ([YourStory](https://yourstory.com/2024/05/redhealth-raises-usd-20m-in-series-b-funding-led-by-jungle-ventures)). Reported fleet figures vary from 450 managed ambulances to a "10K+" network, depending on the source and year ([Entrepreneur India](https://india.entrepreneur.com/en-in/news-and-trends/ambulance-service-provider-redhealth-raises-usd-20-mn-led/474190), [Outlook Business](https://www.outlookbusiness.com/start-up/news/redhealth-to-raise-series-c-funding-by-fy25-end-eyes-tech-and-clinical-efficiency)). The fleet size is **not settled**.
3. No driver-facing "ambulance approaching" alert has been confirmed in Google Maps India, Mappls or Ola Maps. This is absence of evidence only ([research_gaps.md §4](research_gaps.md#4-emergency-vehicle-features-in-google-maps-india-mappls-ola-maps-priority-4)).

### 1.2 Problem hypotheses (to test in interviews; not yet evidence)
| # | Hypothesis | Who has the pain | How we will test it |
|---|---|---|---|
| H1 | Small operators dispatch by phone call and WhatsApp, with no record of response times. | Operator owner, dispatcher | Interviews; ask to see how a run is logged today |
| H2 | Hospitals, corporates and event organisers ask operators for response-time proof, and operators cannot produce it cheaply. | Operator owner (sales) | Ask: "Has a client ever asked for response-time data? What did you send?" |
| H3 | Emergency departments want a reliable ETA for incoming ambulances. | Hospital ED head | 3-5 hospital interviews |
| H4 | Crews lose minutes in traffic because drivers ahead do not notice the siren. | Crew | Crew interviews; later the paper's measurements |

**OPINION:** H1 and H2 are the ones that create a paying customer. H4 is the founder's original idea. It is real, but it does not create a buyer (next section).

### 1.3 Where the original idea is weak (honest verdict)
| Original assumption | What earlier research found | Consequence |
|---|---|---|
| Gig-fleet drivers (Rapido, Uber, Ola, Blinkit, Zomato, Swiggy) will install or receive the alert | These platforms publish no partner SDK for this. They face union and Labour Ministry pressure on rider monitoring. Telangana's gig-worker Act 21 of 2026 adds data duties on aggregators ([PRS Act text](https://prsindia.org/files/bills_acts/acts_states/telangana/2026/Act21of2026TG.pdf); details **UNVERIFIED**) | Distribution through platforms is blocked for now. A standalone driver app needs mass installs, which a solo founder cannot buy. |
| Someone pays for drivers to give way | Nobody anywhere pays drivers to give way (earlier research) | There is no revenue in the driver network. |
| The alert is defensible | Known prior art (HAAS Alert, Waze emergency alerts, Dutch national feed, patents listed in [paper_plan.md §3](paper_plan.md#3-related-work-to-position-against-no-novelty-claims)) | No moat. Compete on service, not on the technology. |
| A phone alert is legal to use while driving | The 2020 proviso on phone-as-navigation is **not verified**; two-wheeler use is the least clear ([research_gaps.md §1](research_gaps.md#1-exact-statute-text-priority-1)) | Car dash-mounted phones first; voice and vibration only; lawyer question 7. |

**Pivot:** sell the operator software. Keep the alert as (a) an opt-in feature the operator can switch on, (b) a research pilot that produces a paper, and (c) a platform API spec ([mvp_architecture.md §4](mvp_architecture.md#4-platform-api-server-to-server-no-rider-data)) for the day a map or gig platform wants it.

---

## 2. Solution and product scope

### 2.1 MVP (months 1-4)
| Module | What it does | Built from |
|---|---|---|
| Crew app (web/PWA first; native Android later) | Start or stop an emergency run, choose the destination hospital, send GPS every 2-3 s while the phone is mounted with the screen on, siren and flasher toggle | [mvp_architecture.md §6.1](mvp_architecture.md#61-two-stage-approach): the web version cannot track in the background, which is acceptable for the business pilot but not for alert road tests |
| Dispatch board (web) | Live map of the operator's ambulances, run status, assign a run | New; simple web app |
| ETA to hospital | Route and ETA from OSRM on OpenStreetMap; a shareable link for the receiving hospital | OSRM (open source) |
| Response-time report | Monthly PDF or CSV: call-to-dispatch, dispatch-to-scene, scene-to-hospital times per run | New; needs the operator to log call time |
| Give-way alert (opt-in; native Android driver app) | Signed corridor to opted-in driver phones; voice and vibration first; map-style screen on dash-mounted car phones with a blue left band and arrow; for two-wheeler and gig riders, a reduced handlebar screen (arrow and band only) **only if legal check L1 passes**; never "move right" | [alert_message_spec.md §4](alert_message_spec.md#4-channels), [§4c](alert_message_spec.md#4c-blocking-legal-check-l1-phone-screens-while-riding-or-driving), [privacy_design.md](privacy_design.md) |

Not in the MVP: patient records, billing, insurance claims, iOS, hardware trackers, any 108 integration.

### 2.2 Later (months 6-18, only if the pilot converts)
1. Integrations with GPS trackers the operator already has (AIS-140 coverage of ambulances is **unresolved**, [research_gaps.md §3](research_gaps.md#3-do-ais-140-trackers-cover-ambulances-priority-3)).
2. A hospital ED view showing incoming ambulances.
3. Service-level reports for corporate and event contracts.
4. A platform API for map or gig apps (spec exists; no partner expected soon, **OPINION**).
5. Traffic-police integration (green corridors, signal priority), only with written approval.

### 2.3 Design rules carried from earlier docs
1. No patient data anywhere ([privacy_design.md §2](privacy_design.md#2-ambulance-side-data)).
2. Driver location never leaves the phone by default (on-device matching).
3. The alert says "if safe", fails silent on stale data, and never says "move right".
4. Audio first for everyone. Screens confirm, never replace, the voice.
5. Pilot languages: English, Telugu and Hindi. Urdu later, after a native-speaker review.

---

## 3. Why now

| Driver | Type | Source |
|---|---|---|
| DPDP Rules notified Nov 2025, main duties due about May 2027: operators will need a processor that handles location data carefully | FACT (dates partly secondary) | [PIB note](https://static.pib.gov.in/WriteReadData/specificdocs/documents/2025/nov/doc20251117695301.pdf); [privacy_design.md §4](privacy_design.md#4-dpdp-duty-map) |
| Funded private emergency operators exist in Hyderabad and are expanding | FACT | [YourStory 2024](https://yourstory.com/2024/05/redhealth-raises-usd-20m-in-series-b-funding-led-by-jungle-ventures) |
| Open routing (OSRM, OpenStreetMap) and cheap Android phones make a no-hardware product possible | FACT (open source) / OPINION (cheapness) | [mvp_architecture.md](mvp_architecture.md) |
| Emergency-vehicle alerts are spreading abroad (Waze; HAAS Alert), so buyers already understand the idea | FACT for Waze | [Waze Help](https://support.google.com/waze/answer/14716475?hl=en) |
| Rising scrutiny of gig-worker monitoring | FACT (Act exists) | [PRS](https://prsindia.org/files/bills_acts/acts_states/telangana/2026/Act21of2026TG.pdf) |

The last row is a reason **not** to depend on gig platforms.

---

## 4. Customers and buyer map

| Segment | Buyer (signs) | User | Why they might pay (hypothesis) | Priority | Notes |
|---|---|---|---|---|---|
| Small/mid private operators (5-50 ambulances) in Hyderabad | Owner | Dispatcher, crew | Proof of response time for hospital and corporate clients; less chaos in dispatch | **1** | Number of such operators in Hyderabad: `[to fill]` |
| Hospital in-house fleets | Hospital admin or operations head | ED staff, drivers | Incoming ETA; fleet use | **2** | Earlier research lists hospital fleets as not yet researched |
| Large aggregators (RED.Health, Medulance) | Head of product or operations | Their own crews | Possibly the alert pilot or the research data | 3 (partner) | Both describe their own tech platforms ([Quartz on StanPlus](https://qz.com/india/1113437/stanplus-with-new-tech-and-an-old-school-helpline-a-hyderabad-startup-is-out-to-fix-indias-ambulance-services), [CXOToday on Medulance](https://cxotoday.com/corner-office/medulance-leveraging-technology-to-take-a-big-leap-in-ems-sector/)). **OPINION:** more likely to build than buy. |
| Corporate, event or industrial EMS contracts | Facility or HSE manager | n/a | SLA reports | 4 | Reached through the operator, not directly |
| State 108 (EMRI GHS in Telangana) | State health department | n/a | n/a | **Not now** | Data ownership unknown ([research_gaps.md §2](research_gaps.md#2-who-owns-108-ambulance-data-priority-2)); slow procurement |
| Gig platforms, map apps | Partnerships team | Riders | Brand safety | **Not now** | No SDK; see §1.3 |

**Change from earlier research:** the earlier verdict named RED.Health as the best first customer. Since it appears to run its own platform, this plan starts with smaller operators and keeps RED.Health as a meeting to request (it may want the alert pilot or a research partnership). Question 1 in [questions_for_founder.md](questions_for_founder.md) asks whether the founder has a contact there.

---

## 5. Business model and pricing

| Item | Proposal | Label |
|---|---|---|
| Unit | Per active ambulance per month | OPINION |
| List price | ₹1,500 per ambulance per month (range ₹1,000-2,000) | ESTIMATE; anchor from earlier research; untested |
| Pilot | Free for 90 days, for 5-10 ambulances, in exchange for a written pilot report and a reference | OPINION |
| Minimum | ₹5,000 per operator per month after the pilot, so small fleets are still worth serving | ESTIMATE |
| Alert feature | Included free. The operator switches it on for its runs. Drivers never pay. | OPINION |
| Taxes | GST is likely to apply to software sold as a service; confirm the rate and registration threshold with a CA | UNVERIFIED |
| Possible later revenue | Hospital ED view (per hospital); SLA reports for corporate contracts; research or data partnerships (aggregated, no personal data) | OPINION |

**Pricing test in interviews:** ask "what do you pay today for GPS tracking or software per vehicle?" and do the Van Westendorp four questions (too cheap, cheap, expensive, too expensive). Record answers in a sheet; do not quote any answer as a commitment.

---

## 6. Unit economics (all ESTIMATES)

Per ambulance per month, at ₹1,500 list price.

| Line | ₹ per month | Assumption |
|---|---|---|
| Revenue | 1,500 | List price, before GST |
| Cloud (server, broker, storage) | 50-150 | One small server shared by 50-200 ambulances at ₹5,000-10,000 a month (cloud prices not checked) |
| Crew phone and data | 0 | Operator's phone and SIM; if we must supply a phone, add about ₹300/month (a ₹7,500 phone over 24 months; ESTIMATE) |
| Support and onboarding | 150-300 | About 15-30 minutes of founder or support time per ambulance per month |
| Payment collection | 0-30 | Bank transfer or UPI |
| **Gross margin** | **about 70-85%** | Falls if we supply phones |

| Customer-level figure | Value | Assumption |
|---|---|---|
| Typical first customer | 10 ambulances = ₹15,000 per month = ₹1.8 lakh per year | ESTIMATE |
| Cost to win one customer | 40-80 hours of founder time over 2-4 months, plus ₹5,000-10,000 travel | ESTIMATE; founder-led sales |
| Churn | unknown | `[to fill]` after the first pilot |
| Payback | Under 6 months if the customer stays | Depends on churn |

**OPINION:** the numbers work only if one person can serve 100+ ambulances. That means self-serve onboarding and few custom requests.

---

## 7. Go-to-market: Hyderabad first

### 7.1 Steps
0. **Get a mentor (weeks 1-2).** The founder has no contacts and no sales experience. Ask CBIT's startup cell `[to confirm name]` and the alumni office for a sales or healthcare mentor. **Do not assume warm introductions** anywhere in this plan.
1. **Map the market (weeks 1-3).** List private operators in Hyderabad from Google Maps, JustDial, hospital tie-ups and the earlier research notes. Target 30 names, `[to fill]`. All contact is cold: calls, WhatsApp, and walk-ins at ambulance stands near large hospitals.
2. **Interview (weeks 2-9).** 12-15 interviews: 8+ operators, 3-5 hospitals, 3+ crews. Script in [project_plan.md](project_plan.md). No pitching in the first half of each interview.
3. **Get a pilot (weeks 10-15; cold-outreach case).** Offer the free 90-day pilot to the 2-3 operators with the clearest pain. Ask for a one-page pilot agreement (processor terms; lawyer question 8).
4. **Run the 90-day pilot (about weeks 15-28).**
5. **Convert (about weeks 26-30).** Pilot report, price conversation, first invoice.
6. **Use the reference** to reach the next 5 operators, then a second city only after 3 paying Hyderabad customers.

### 7.2 What the 90-day pilot must prove
| Days | Focus | Success measure (ESTIMATE thresholds) |
|---|---|---|
| 1-30 | Install, train crews, dispatch board live; alerts **off** | ≥80% of the pilot ambulances' emergency runs are tracked; dispatcher uses the board at least 4 days a week |
| 31-60 | First monthly response-time report; hospital ETA link in use | Owner uses the report with at least one client, or says in writing why not |
| 61-90 | Alert feature on for consenting crews and a small, consented rider group (only with ethics approval, written operator and police approval, the native driver app, and a grant for insurance; otherwise skipped) | No safety incident; latency gates met (median under 5 s, p95 under 15 s, [mvp_architecture.md §6](mvp_architecture.md#6-build-plan-ai-assisted-no-prior-android-experience)) |
| Day 90 | Decision | Operator agrees to pay (signed order or written refusal with reasons) |

Alert-on runs during the pilot are tied to the research protocol in [paper_plan.md §4.4](paper_plan.md#44-optional-consented-field-pilot-rq4). If approvals do not arrive, the operator pilot runs without alerts. **The business pilot must not depend on the alert.**

### 7.3 Channels
1. Founder-led direct sales (main channel).
2. Incubator introductions (CIE's medtech incubator, Ojas, is named in a CIE newsletter: [CIE Oct 2025 newsletter](https://cie.iiit.ac.in/monthly-newsletter-october-2025/); fit **UNVERIFIED**).
3. Hospital ED heads who introduce their contracted operators.
4. The paper and a public demo as credibility, not as a sales channel.

---

## 8. Competition and prior art

**No novelty or patent claim.** The table lists what exists; it is not a freedom-to-operate opinion. A patent search has not been done (lawyer question to add: see [questions_for_founder.md](questions_for_founder.md)).

| Name | What it is | Overlap with us | Source |
|---|---|---|---|
| RED.Health (was StanPlus), Hyderabad | Operator and aggregator with its own tech platform | High: could build all of this in-house | [Quartz](https://qz.com/india/1113437/stanplus-with-new-tech-and-an-old-school-helpline-a-hyderabad-startup-is-out-to-fix-indias-ambulance-services), [YourStory 2021](https://yourstory.com/2021/06/ambulance-startup-stanplus-10x-demand-covid-19-second-wave) |
| Medulance, Delhi | Aggregator with GPS booking, dispatch and dashboards | High in its cities | [CXOToday](https://cxotoday.com/corner-office/medulance-leveraging-technology-to-take-a-big-leap-in-ems-sector/) |
| eSahai, Hyderabad | Cloud fleet management for hospitals and fleet owners (2017 report; current status **UNVERIFIED**) | **Direct, same city** | [YourStory 2017](https://yourstory.com/2017/07/esahai-startup-medical-taxis-cloud/) |
| Drlogy | Hospital software with an ambulance module (tracking, dispatch, reports) | Direct for hospital fleets | [Drlogy](https://drlogy.com/hospital-management-software/ambulance) |
| Ziqitza (ZHL) | Large EMS operator with its own dispatch platform; also sells fleet tracking | Medium | [ZHL fleet page](https://zhl.org.in/fleet-management-system) |
| Mappls (MapmyIndia) | Dispatch and routing for emergency control rooms | Medium (government side) | [Mappls](https://about.mappls.com/government-smart-city-solutions/emergency_response.php) |
| Generic GPS and telematics vendors | Trackers with dashboards | Medium: cheap tracking may be "good enough" | e.g. [Vi connected ambulances](https://www.myvi.in/business/why-vi/case-studies/connected-ambulances-to-improve-workers-safety) |
| HAAS Alert; Waze emergency alerts; Dutch national feed | Driver alerts for emergency vehicles (abroad) | Prior art for the alert | [paper_plan.md §3](paper_plan.md#3-related-work-to-position-against-no-novelty-claims) |
| Patents US8483651B1, US10832579B2 | Alert phones near emergency vehicles; dispatch with route data | Prior art; **not read; no legal opinion** | same |

**Where we can differ (OPINION, unproven):**
1. No hardware: works on the crew's Android phone in a day.
2. Built for small operators: cheap, Telugu and Hindi interface, WhatsApp-style simplicity.
3. Response-time reports designed for the client conversations operators have.
4. Privacy by design that an operator can show to a hospital or a regulator.
5. The give-way alert as a visible extra that competitors do not ship in India (absence of evidence only).

None of these is a moat. The defensible parts would be customer relationships, operator data and speed of service.

---

## 9. Risks and mitigations

| # | Risk | Type | Likelihood (OPINION) | Mitigation |
|---|---|---|---|---|
| 1 | Operators will not pay; trackers or WhatsApp are "good enough" | Market | High | Interview gate before building past the MVP (kill criterion K1 in [project_plan.md](project_plan.md)); free pilot with a pre-agreed price |
| 2 | Big operators build in-house | Market | High | Target small and mid operators; offer the big ones a research partnership |
| 3 | A driver is hurt after an alert; liability | Legal | Low frequency, high impact | "If safe" wording; never "move right"; fail silent; terms of use; professional-indemnity cover (`[to fill]` quote); lawyer questions 6 and 10 ([privacy_design.md §8](privacy_design.md#8-questions-for-a-lawyer)). A 2024 FIR in Budaun named a Google Maps manager after a crash, per earlier research: liability is a real risk |
| 4 | Phone-use rules for drivers (2020 proviso to reg. 37(1) unverified) | Legal | Medium | Voice and vibration only; screen only on fixed car phones; no touch needed; lawyer question 7 |
| 5 | DPDP breach or misuse of location data | Data | Medium | On-device matching; no patient data; 30-day raw-track retention; processor contract with each operator ([privacy_design.md](privacy_design.md)) |
| 6 | Gig platforms block or ignore the alert | Platform gatekeeping | High | Not in the business plan's revenue; API spec only |
| 7 | Fake or false alerts | Security, trust | Medium | Signed corridors; operator audit of "emergency" flags |
| 8 | Android battery managers kill the app | Technical | High | Foreground service; per-brand setup; brand benchmark ([mvp_architecture.md §3](mvp_architecture.md#3-failure-handling)) |
| 9 | Founder time: M.Tech plus a startup | Team | Medium (3rd semester, mostly project work) | 10-12 hours a week plan `[to confirm]`; decision gates; cut order in [project_plan.md §4](project_plan.md#4-keeping-the-paper-and-the-business-in-step) |
| 12 | No Android experience; AI-assisted code fails on background and battery rules | Technical, team | High | Web crew app first (stage A); native driver app only for the alert and paper; test on real phones early; slip of 1.5-2× assumed ([mvp_architecture.md §6](mvp_architecture.md#6-build-plan-ai-assisted-no-prior-android-experience)) |
| 13 | No money: anything not free or borrowed cannot happen | Financial | Certain until a grant | CBIT cell first, then PRAYAS; list of grant-gated items in [project_plan.md §8](project_plan.md#8-what-cannot-be-done-without-a-grant) |
| 14 | No contacts and no sales experience slow the first pilot | Market, team | High | Mentor step; cold-outreach plan; G2 set at week 15 |
| 10 | Ethics or police approval delayed | Regulatory | Medium | The business pilot does not need them; only the alert field pilot does |
| 11 | 108 data or tenders demand things a student startup cannot meet | Market | High | Stay out of 108 for 12 months |

---

## 10. Financial model: three scenarios (all ESTIMATES)

**Assumptions common to all scenarios**
1. Price ₹1,500 per ambulance per month (₹18,000 a year), no price rise, before GST.
2. "Ambulances paying" is the year-end figure; revenue uses the average of the start and end of each year.
3. Year 1 starts when the first pilot converts (about month 7 from now). Earlier months are grant-funded build and pilot.
4. Founder stipend: ₹25,000 a month in year 1 from a grant, ₹50,000 a month from year 2.
5. Cloud cost: ₹10,000 a month in year 1, rising with fleet size (₹100 per ambulance per month).
6. Salaries: one engineer at ₹60,000 a month; one operations or sales person at ₹40,000 a month (Hyderabad rates; **not checked**).
7. No paid marketing. No hardware sales.

| | Low | Base | High |
|---|---|---|---|
| Ambulances paying, end of Y1 / Y2 / Y3 | 10 / 40 / 100 | 30 / 150 / 400 | 60 / 400 / 1,200 |
| Paying operators, end of Y3 (at about 10-20 ambulances each) | 6-10 | 20-40 | 60-120 |
| **Revenue Y1** | ₹0.9 lakh | ₹2.7 lakh | ₹5.4 lakh |
| **Revenue Y2** | ₹4.5 lakh | ₹16.2 lakh | ₹41.4 lakh |
| **Revenue Y3** | ₹12.6 lakh | ₹49.5 lakh | ₹1.44 crore |
| Team in Y3 | Founder only | Founder + 2 engineers + 1 ops | Founder + 4 engineers + 3 ops/sales |
| **Costs Y1** | ₹6 lakh | ₹7 lakh | ₹8 lakh |
| **Costs Y2** | ₹9 lakh | ₹19 lakh | ₹30 lakh |
| **Costs Y3** | ₹10 lakh | ₹40 lakh | ₹90 lakh |
| Net Y3 | about +₹2.6 lakh (see note) | about +₹9.5 lakh | about +₹54 lakh |
| Net over Y1-Y3 | about -₹7 lakh | about +₹2.4 lakh | about +₹63 lakh |
| What it means (OPINION) | A side project or a consulting line; not a venture business | A small, sustainable company; grant plus a small angel round is enough | Needs a second city and probably a hospital product; angel or seed round in Y2 |

Note on Low: Y3 revenue (₹12.6 lakh) is about ₹2.6 lakh above Y3 costs (₹10 lakh), but only because the founder works alone at ₹50,000 a month. Over three years the Low case loses about ₹7 lakh, which must come from grants.

**How the cost lines were built (Base case)**
| Line | Y1 | Y2 | Y3 |
|---|---|---|---|
| Founder stipend | 3.0 | 6.0 | 6.0 |
| Engineers | 0 | 7.2 (1 from month 13) | 14.4 (2) |
| Operations / sales | 0 | 0 | 4.8 (1) |
| Cloud | 1.2 | 1.8 | 4.8 |
| Company, legal, CA, insurance | 1.0 | 1.5 | 2.5 |
| Pilot costs (phones, crew stipends) | 1.2 | 1.0 | 2.0 |
| Travel, tools, misc | 0.6 | 1.5 | 5.5 |
| **Total (₹ lakh)** | **7.0** | **19.0** | **40.0** |

Pre-revenue build and pilot (next 6 months): **₹0 own money**. Without a grant, only free or borrowed resources are used. With a grant, about ₹1-1.5 lakh direct costs per [mvp_architecture.md §5](mvp_architecture.md#5-costs-estimates-in-inr-not-quotes), plus company registration and legal advice `[to fill quotes]`. The year-1 founder stipend in this model also needs a grant.

Update this table with real interview prices and pilot conversion after week 26. Every number here is a placeholder for a measured one.

---

## 11. Milestones

| By (week of [project_plan.md](project_plan.md), from 30 Nov 2026) | Milestone | Evidence |
|---|---|---|
| Week 1 | CBIT startup cell visited; ethics body identified | Notes |
| Week 2 | Mentor asked (CBIT cell or alumni) | Email or meeting note |
| Week 5 | 30-name operator list; 5 interviews done; ethics application submitted | Interview notes in the repo (anonymised) |
| Week 7 | Legal check L1 done (two-wheeler screen go or no-go) | L1 note |
| Week 9 | 10+ interviews; go or no-go on the operator product (gate G1); web crew app and dispatch board v0 | Gate decision recorded |
| Week 10 | PRAYAS or incubator application submitted (after the CBIT step) | Application copy |
| Week 15 | One pilot agreement signed (gate G2, cold-outreach case) | Signed agreement (not a quote or a promise) |
| Week 16 | Latency and battery benchmark (paper RQ1); may slip 3-4 weeks | Benchmark table |
| Week 20 | Pilot in use (gate G3); lab usability study done if ethics approved (paper RQ2) | Usage numbers; study data |
| Week 24 | Paper draft to the CBIT supervisor | Draft |
| About week 28 | Pilot day 90: first invoice or a documented "no" (gate G4) | Invoice or written reasons |

---

## 12. Funding ask

| Stage | Source | Amount | What it pays for | Eligibility notes | Status |
|---|---|---|---|---|---|
| **Step 1 (now)** | **CBIT startup or seed cell** `[to confirm name]` and any CBIT grant | `[to confirm]`: **not verified** what CBIT offers | Whatever it covers: mentoring, legal help, small grant, phones, introductions to PRAYAS centres | Founder says CBIT backs the work if the paper is strong. Ask in week 1 | Not asked |
| Step 2 | **NIDHI-PRAYAS** prototype grant via a PRAYAS centre | Up to ₹10 lakh under PRAYAS 1.0; DST's newer PRAYAS pages mention up to ₹20 lakh (and ₹40 lakh for specialised centres) | Build, phones, pilot, legal advice, founder stipend if allowed | Individual innovators can apply; centres include CIE at IIIT Hyderabad ([CIE PRAYAS](https://cie.iiit.ac.in/dst-nidhi/)) and i-TIC at IIT Hyderabad ([i-TIC PRAYAS page](https://itic.iith.ac.in/nidhi-prayas.html)). Which version is open now: **UNVERIFIED** ([DST PRAYAS 2.0](https://nidhi.dst.gov.in/prayas2-0/)) | Not applied |
| Step 2 | Incubation (desk, mentors, introductions) | In kind | Credibility with operators | CIE (IIIT-H), i-TIC (IIT-H; listed as a NIDHI-TBI focused on energy, biomedical and robotics: [India Science & Technology listing](https://www.indiascienceandtechnology.gov.in/listingpage/tbis)), ASPIRE (UoH; has an IT/electronics centre, ASPIRE-TIDE: [ASPIRE](https://aspire.uohyd.ac.in/about-us-2/)). Ask each which fits mobility or health software | Not applied |
| Step 3: after incorporation (founder is willing) and a pilot | **Startup India Seed Fund Scheme** via an incubator | Grant up to ₹20 lakh for proof of concept, prototype or product trials; debt or convertible up to ₹50 lakh for scale-up | Second engineer; first paid pilots | DPIIT recognition, incorporated less than 2 years, at least 51% Indian promoters; milestone-based tranches ([myScheme SISFS](https://myscheme.gov.in/schemes/sisfs-fs)). Still open: **check the portal** | Not eligible yet (no company) |
| After 3 paying operators | Angels (for example Hyderabad Angels) | `[to fill]`; size after Y1 numbers are real | Team of 3-4; second city | Only with paying customers | Not started |

**Ask, in one line for a grant panel:** "₹10 lakh and incubation to build and run a 90-day pilot of no-hardware ambulance operations software with one Hyderabad operator, and to publish an evaluation of a privacy-preserving give-way alert." (ESTIMATE; adjust to the scheme's limits.)

**Do not** claim to a grant body that the alert is novel, that any operator has committed, or that any number in §10 is measured.

---

## 13. Team and gaps

| Role | Today | Gap | Cheapest fix |
|---|---|---|---|
| Founder: product and engineering | Solo M.Tech student (3rd semester), CBIT Hyderabad; web app built with AI help | No Android experience; no sales experience | Supervisor as academic mentor; CBIT cell mentor; AI-assisted build with a peer code review |
| Domain (EMS operations) | None | High | Adviser: an ED doctor or a retired operator manager, 1 hour a month, `[to fill name]` |
| Sales and operations | None; no operator contacts | High | Sales mentor from CBIT cell or alumni (week 2); founder does cold outreach; hire after first revenue. Co-founder: question open |
| Second engineer (Android) | None | **High** (founder has no Android experience) | CBIT B.Tech or M.Tech student for project credit; reviews the native driver app |
| Legal and privacy | None | High for the alert | Incubator legal clinic; pro-bono law-school clinic; questions in [privacy_design.md §8](privacy_design.md#8-questions-for-a-lawyer) |
| Human-factors and statistics | Supervisor? `[to fill]` | Medium | Co-author on the paper |
| Native-language review | Founder speaks English, Hindi, Telugu | Low for the pilot; Urdu later | Founder reviews; 5 volunteer speakers per language test the strings; Urdu waits for a native reviewer |

---

## 14. What would change this plan

1. Interviews show operators do pay for software today: speed up, raise the price test.
2. Interviews show operators will not pay: stop the business, keep the paper (kill criterion K1).
3. A map or gig platform asks for the corridor feed: revisit the driver-network idea as a B2B API, still without rider data.
4. A lawyer says the alert creates unmanageable liability: drop the alert from the product; keep the operator software.

See ranked questions in [questions_for_founder.md](questions_for_founder.md).
