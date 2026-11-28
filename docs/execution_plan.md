# Execution plan: build at zero cost and earn the first rupees

Status: plan, 28 Nov 2026. Starts Monday 30 Nov 2026 (week 1).
Labels: **FACT** (with link), **ESTIMATE** (assumptions shown), **OPINION**, **UNVERIFIED**, `[to fill]` (data missing).
Nothing here is traction: there are **no customers, pilots, letters or quotes** yet. Not legal advice. No novelty or patent claims.
Builds on [business_plan.md](business_plan.md), [mvp_architecture.md](mvp_architecture.md), [alert_message_spec.md](alert_message_spec.md), [privacy_design.md](privacy_design.md), [paper_plan.md](paper_plan.md). For weeks 1-12 this file is the working schedule; where dates differ from [project_plan.md](project_plan.md), this file wins (gates are brought forward because the plan is money-first). **OPINION.**

**Deferred (per founder):** CBIT startup cell and seed-fund details, IP ownership, ethics committee. One fact cannot wait, though: CBIT's IPR policy says software and mobile apps developed using CBIT resources stay with CBIT ([CBIT IPR policy, §4.1.2](https://cbit.ac.in/wp-content/uploads/2020/11/CBIT-IPR-Policy-Upload.pdf), read 28 Nov 2026). **Until this is settled in writing, build on your own laptop and your own internet, outside lab hours.** CBIT also runs an Incubation Centre, ACIC-CBIT and an MSME incubator, and its policy mentions a seed loan and 3-6% revenue sharing for incubatees ([CBIT startup policy](https://cbit.ac.in/wp-content/uploads/2020/11/CBIT-Innovation-Inncubation-start-up-policy-28th-July-NISP-PDF.pdf)). Look at these later.

---

## 1. What to build, in order, at ₹0

### 1.1 Free tools (the stack)
Free tiers exist for all of these. **Their limits and India-region options were not checked in this session (UNVERIFIED).** Read each pricing page before relying on it.

| Need | Tool | Note |
|---|---|---|
| Database, login, live updates | [Supabase](https://supabase.com/pricing) (Postgres + Realtime + Auth) | Choose an India region if offered (**UNVERIFIED**); free projects may pause when idle |
| Web hosting | [Vercel](https://vercel.com/pricing), Netlify or Cloudflare Pages | You already deployed a site this way |
| Map | [Leaflet](https://leafletjs.com/) + OpenStreetMap tiles | The OSM tile servers have a [usage policy](https://operations.osmfoundation.org/policies/tiles/); light pilot use only, then a tile provider's free tier |
| Routing and ETA | [OpenRouteService](https://openrouteservice.org/plans/) free key, or OSRM on your laptop | The OSRM demo server is [not for production](https://github.com/Project-OSRM/osrm-backend/wiki/Demo-server) |
| Browser features | [Geolocation](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API), [Screen Wake Lock](https://developer.mozilla.org/en-US/docs/Web/API/Screen_Wake_Lock_API), HTML audio | The page must stay open with the screen on |
| Voice clips | **Record them yourself** in English, Hindi and Telugu (phone voice recorder, free editor such as Audacity) | You speak all three; still test with 5 speakers per language ([alert_message_spec.md §3](alert_message_spec.md#3-wording-by-language-draft-native-speaker-review-needed)) |
| Reports | CSV download + browser "Print to PDF" | No PDF library needed in V0 |
| Native Android (later) | Android Studio (free), Kotlin | Share the APK directly for the pilot. Publishing on the Play Store has a one-time fee ([Google Play Console help](https://support.google.com/googleplay/android-developer/answer/6112435)); not needed yet |
| AI help | Claude Pro (already paid) | Use the prompts pattern in §1.3 |
| Code and tasks | GitHub (this repo), a free GitHub Project board | — |

### 1.2 Products and versions

Days are **ESTIMATES** for a founder who is new to the stack, coding with AI help at about 3-4 focused hours a day.

#### A. Crew app + dispatch board (browser)
| Version | Exact features | Proves | Days |
|---|---|---|---|
| **V0** | Ambulance logs in with a 6-digit code; big "Start run" / "End run" buttons; GPS sent every 5 s while the page is open; dispatch page shows all ambulances on a Leaflet map with "free" or "on run" and last-seen time | Live tracking on a normal phone with no hardware | 5-7 |
| **V1** | Run stages with one tap each (call received, dispatched, at scene, left scene, at hospital); pick the hospital from a list; siren on/off toggle; queue points when offline and send later (drop points older than 10 s for live view, keep them for the report); several operators kept apart; screen-wake lock; Telugu/Hindi/English labels | The timestamps an operator needs for reports | 7-10 |
| **V2** | Dispatcher assigns a run to an ambulance; crew sees and accepts it; shift roster; "install to home screen"; battery and signal warning; audit log of who changed what | It can replace phone-call dispatch | 10-14 |

**Cannot do (all versions):** track with the screen off or the browser in the background (browsers pause it, **OPINION** from platform behaviour, to be tested on your phones); guarantee delivery when the crew switches apps; work as the source for real-road alert tests. **Never stores patient data** ([privacy_design.md §2](privacy_design.md#2-ambulance-side-data)).

#### B. Shareable live ETA link
| Version | Exact features | Proves | Days |
|---|---|---|---|
| **V0** | Dispatcher taps "Share" and gets a link with a random token; the page shows the ambulance marker and straight-line distance to the hospital; it expires when the run ends | The hospital can see an incoming ambulance with no login | 2 |
| **V1** | Road ETA from the routing API, refreshed each minute; "arriving in N min" in large text; opens on WhatsApp; shows only vehicle code and destination | Useful ETA for the emergency department | 3-4 |
| **V2** | Hospital board: every ambulance heading to that hospital, from any operator that agrees | A hospital-side product (later revenue) | 5-7 |

**Cannot do:** be more accurate than the crew phone's GPS and the routing data; work if the crew page is closed.

#### C. Response-time report
| Version | Exact features | Proves | Days |
|---|---|---|---|
| **V0** | CSV per month: run ID, ambulance, stage timestamps, durations | The data is captured | 1-2 |
| **V1** | One-page monthly PDF: number of runs, median and 90th-percentile call-to-dispatch, dispatch-to-scene and scene-to-hospital times, per ambulance; operator logo | Something the owner can show a client | 3-5 |
| **V2** | Client-specific report (one hospital or company), month-on-month trend, gaps highlighted (runs with missing stages) | Supports contract renewals (hypothesis H2 in [business_plan.md §1.2](business_plan.md#12-problem-hypotheses-to-test-in-interviews-not-yet-evidence)) | 4-6 |

**Cannot do:** record the call time unless the dispatcher taps "call received"; prove anything about runs done without the app.

#### D. Browser alert simulator (English, Hindi, Telugu)
| Version | Exact features | Proves | Days |
|---|---|---|---|
| **V0** | Replays a recorded ambulance track on the map; you drag a "driver" dot; when the driver is ahead, on the same road and direction, it plays your recorded voice clip ("Ambulance behind you, 200 metres. Move left if safe.") and shows the blue left band and arrow; never "move right" | The alert idea in a 1-minute demo to operators, grant panels and the supervisor | 4-6 |
| **V1** | All six cases of the decision table ([alert_message_spec.md §2](alert_message_spec.md#2-direction-logic-decision-table)); language switch; car screen and the reduced two-wheeler screen (arrow and band only, shown **for lab tests only** until legal check L1 passes, [§4c](alert_message_spec.md#4c-blocking-legal-check-l1-phone-screens-while-riding-or-driving)); "test mode" that logs time from alert start to the participant's answer | The lab usability study app (paper RQ2) | 5-7 |
| **V2** | A phone with the page open receives live corridors from a real crew session (foreground only) | End-to-end demo with no native code | 4-6 |

**Cannot do:** alert anyone on a real road; run in the background; count as evidence of real-world benefit. Label every demo "simulation".

#### E. Native Android alert app (later; after weeks 8-12)
| Version | Exact features | Proves | Days |
|---|---|---|---|
| **V0** | Foreground service with persistent notification; location at 1 Hz; subscribes to corridors (Supabase Realtime or MQTT); local point-in-corridor and heading test; plays pre-recorded clip; fail silent on stale data | Alerts with the screen off | 15-25 (no prior Android experience; 1.5-2× slip assumed, [mvp_architecture.md §6.2](mvp_architecture.md#62-timeline-estimate)) |
| **V1** | Logs receive time for the 5-brand latency and battery benchmark (paper RQ1); signed-corridor check | RQ1 data | 7-10 |
| **V2** | Per-brand "don't kill this app" setup screens; vibration pattern; 3 languages; opt-in research logging | Ready for a consented field study | 10-15 |

**Cannot do:** reach riders who have not installed it; guarantee delivery on every brand (battery managers). Field use needs ethics approval and written operator and police approval ([paper_plan.md §7](paper_plan.md#7-ethics-and-approvals)).

**Build order (OPINION):** A-V0 → B-V0 → C-V0 → D-V0 (all by week 4) → A-V1 → C-V1 → B-V1 (by week 8) → D-V1 → A-V2/C-V2 as customers ask → E later. Products A-C earn money; D sells the story and feeds the paper; E is the research track.

### 1.3 How to build with AI help (each feature)
1. Write a 10-line spec: who taps what, what is stored, what the screen shows, what must never happen.
2. Ask Claude for the database table first, then the page, then tests. One feature per chat.
3. Run it on your phone the same day. Drive or walk a real route for every GPS feature.
4. Commit after every working step; write in the commit message what you tested.
5. Ask Claude to review the code for security: row-level security in Supabase so one operator can never see another's data; no patient fields.
6. Keep a "known limits" list in the repo and show it to customers honestly.

---

## 2. How to make money (ranked, OPINION)

Ranked by speed to first money for a solo founder with no contacts, weighed against how much it builds the real business.

| Rank | Stream | Who pays | Price (**ESTIMATE**) | Assumptions | Time to first money (ESTIMATE) |
|---|---|---|---|---|---|
| 1 | **Paid pilot → subscription** per ambulance | Private operator owner | 30 days free, then a "founding customer" price of ₹1,000 per ambulance per month for 3 months, then ₹1,500; minimum ₹5,000 per month after the founding period | Anchor ₹1,000-2,000 from earlier research, untested; minimum covers support time for small fleets | 2-4 months |
| 2 | **Custom build** for one operator or hospital fleet (e.g. their own branded booking page, a report in their format, a WhatsApp booking form linked to dispatch) | Operator or hospital admin | ₹25,000-75,000 fixed per project, 50% upfront | 2-4 weeks of your time; Hyderabad freelance rates not checked; you keep the right to reuse general code (write this in the letter) | 1-3 months |
| 3 | **Grants** (non-dilutive) | Government schemes via incubators | NIDHI-PRAYAS: up to ₹10 lakh (PRAYAS 1.0) ([CIE](https://cie.iiit.ac.in/dst-nidhi/)); Startup India Seed Fund: grant up to ₹20 lakh after incorporation ([myScheme](https://myscheme.gov.in/schemes/sisfs-fs)) | Calls, eligibility and timing **UNVERIFIED**; usually months | 4-9 months |
| 4 | **Corporate and campus fleets** (industrial units, large campuses, event medical teams) | Facility, HSE or event manager | ₹1,500-2,500 per vehicle per month + ₹10,000 setup | Fewer vehicles, but SLA reports may matter more to them (hypothesis) | 3-6 months |

**Change from earlier docs:** [business_plan.md](business_plan.md) offered a 90-day free pilot. This plan uses **30 days free, then a paid founding period**, because a long free pilot delays the first rupee and tests nothing about willingness to pay. **OPINION.**

### 2.1 Finding the first 5 buyers with no contacts

**Where to look in Hyderabad**
| Place | What to do | Note |
|---|---|---|
| Google Maps and JustDial searches: "private ambulance service" + area (Kukatpally, Ameerpet, Dilsukhnagar, Secunderabad, Gachibowli, LB Nagar, Kondapur) | List name, phone, number of vehicles visible, reviews | Target 40 names in week 1 |
| Ambulance stands near large hospitals (for example around Osmania General Hospital, Gandhi Hospital, NIMS Punjagutta, and private hospital clusters in Somajiguda, Banjara Hills, Jubilee Hills, Gachibowli) | Talk to drivers at quiet hours (11:00-15:00, **OPINION**); ask who owns the vehicle and who dispatches | Whether stands exist at each site: **verify on the spot** |
| Mid-size hospitals (50-200 beds) with their own ambulance | Ask at the front desk for the administrator or operations manager | Hospital websites list ambulance services |
| Ambulance painted phone numbers | Note numbers seen on vehicles in traffic; call later | Free, everywhere |
| Industrial areas (Jeedimetla, Patancheru, Genome Valley) and large IT campuses (HITEC City, Financial District) | Ask security or facility offices whether they keep an ambulance on site or on contract | For stream 4; **hypothesis** |
| Event medical teams (marathons, concerts, college fests) | Ask the organiser who provides the ambulance | For stream 4 |
| LinkedIn | Search "ambulance" + "Hyderabad" for owners and operations managers | Message after 1 walk-in |
| Your cousin (Zepto rider) | Not a buyer. A way to talk to riders about the alert (paper RQ2 recruitment later) | Do not call it a platform tie |

**Scripts** (say them in Telugu or Hindi when that is easier; keep them short)

1. *Walk-in to a driver (30 seconds):* "Namaste. I'm an M.Tech student in Hyderabad studying ambulance response times. Who owns this ambulance, and who tells you where to go? Could I talk to them for 15 minutes? I am not selling anything today."
2. *Phone call to an owner (1 minute):* "Hello sir/madam, my name is [name], an M.Tech student. I'm building a free tool that shows all your ambulances on one map and makes a monthly response-time report you can show hospitals. I'd like 15 minutes to learn how you dispatch today. Can I come to your office this week, or call you at a better time?"
3. *WhatsApp after the call:* "Thank you for your time, [name]. As discussed: a 30-day free trial for [N] ambulances, nothing to install except a web page on the crew's phone. After 30 days you decide. Here is a 1-minute video: [link]. Can we start on [date]?"
4. *Email to a hospital administrator:* Subject: "Live ambulance ETA link for your emergency department, free trial." Body: 3 lines: what it shows, that no patient data is collected, ask for 15 minutes.
5. *Follow-up cadence:* day 2 WhatsApp, day 7 call, day 14 last message ("Shall I close this for now?"). Then move on.

**Funnel target (ESTIMATE, no data):** 40 contacts → 12 conversations → 4 demos → 2 free trials → 1 paying customer. Track every contact in a sheet: date, channel, outcome, next step.

### 2.2 Running a free trial that converts
1. **Day 0:** sign the one-page trial letter (§4.4). Write down the price after the trial and the 3 success measures **before** starting.
2. **Day 1:** install on the crew phones yourself; 30 minutes of training per shift; give the dispatcher your WhatsApp.
3. **Days 2-7:** check data daily; fix bugs within 24 hours; visit once.
4. **Day 14:** show a mid-trial report: runs tracked, median times.
5. **Day 21:** show the draft monthly report; ask "Who would you show this to?"
6. **Day 28:** decision meeting. Show the success measures against the targets. Ask directly: "Shall we continue at the founding price from [date]?" Bring the invoice.
7. If the answer is no: use the playbook in §5.3.

**Success measures (ESTIMATE thresholds):** ≥80% of emergency runs tracked; dispatcher opens the board ≥4 days a week; owner uses the report or ETA link at least once with a client or hospital.

### 2.3 Twelve-month cash view (all **ESTIMATES**; ₹ thousand)
Months: M1 = Dec 2026 … M12 = Nov 2027. Own money spent: **₹0** in every scenario; costs are paid only from revenue. Grants are shown separately because the timing is not controllable.

**Assumptions**
| | Low | Base | High |
|---|---|---|---|
| Paying operators | 1 (5 ambulances) from M7, at the ₹5,000 minimum | A: 8 ambulances from M4 (₹1,000, then ₹1,500 from M7); B: 10 from M8 (₹1,000, then ₹1,500 from M11) | A: 10 from M3; B: 10 from M5; C: 15 from M8 (each ₹1,000 for 3 months, then ₹1,500); campus fleet 3 vehicles at ₹2,000 from M7 |
| Custom builds | none | one ₹30,000 project in M4 | ₹20,000 in M2, ₹50,000 in M4 |
| Costs | free tiers only | ₹1,000/month travel and phone from M4; +₹2,000/month hosting from M7 | ₹2,000/month from M3; ₹6,000/month from M7 |
| Grant (separate) | none | ₹3 lakh first tranche in M8 if approved (size and timing UNVERIFIED) | ₹3 lakh in M6 if approved |

**Revenue by month (₹ thousand)**
| Scenario | M1 | M2 | M3 | M4 | M5 | M6 | M7 | M8 | M9 | M10 | M11 | M12 | Total |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Low | 0 | 0 | 0 | 0 | 0 | 0 | 5 | 5 | 5 | 5 | 5 | 5 | **30** |
| Base | 0 | 0 | 0 | 38 | 8 | 8 | 12 | 22 | 22 | 22 | 27 | 27 | **186** |
| High | 0 | 20 | 10 | 60 | 20 | 25 | 31 | 51 | 51 | 51 | 58.5 | 58.5 | **436** |

**Net cash after costs, 12 months (excluding grants):** Low ≈ ₹30k; Base ≈ ₹186k − ₹21k = ₹165k; High ≈ ₹436k − ₹44k = ₹392k.
**What it means (OPINION):** even the High case does not pay a salary before a grant. Year 1 is about proving that operators pay; the grant pays for time.

---

## 3. Twelve-week calendar (tick the boxes)
"Mon" and "Thu" are the two fixed task days; do the build work on the other days. Hours: about 15-20 a week (**ESTIMATE**; you said time is not a problem).

**Week 1 (30 Nov)**
- [ ] Mon: create the contact sheet; list 40 operators (Google Maps, JustDial)
- [ ] Mon: set up Supabase, Vercel, GitHub board (own laptop)
- [ ] Thu: walk-in at 2 hospital ambulance stands; 10 conversations with drivers
- [ ] Thu: crew app A-V0 started (login code, start/end run)
- [ ] Sun: write down what you learned (5 lines)

**Week 2 (7 Dec)**
- [ ] Mon: 10 phone calls to owners (script 2)
- [ ] Mon: A-V0 sends GPS; dispatch map shows it
- [ ] Thu: 10 more calls; book 3 meetings
- [ ] Thu: test A-V0 on a real 20-minute drive or bus ride with 2 phones

**Week 3 (14 Dec)**
- [ ] Mon: 3 owner meetings (interview script in [project_plan.md §6](project_plan.md#6-operator-interview-script-30-minutes))
- [ ] Mon: ETA link B-V0; CSV report C-V0
- [ ] Thu: record voice clips in 3 languages; simulator D-V0 started
- [ ] Thu: 10 new contacts (hospitals, LinkedIn)

**Week 4 (21 Dec): Gate G1**
- [ ] Mon: D-V0 done; record a 1-minute demo video
- [ ] Mon: 3 more meetings or demos
- [ ] Thu: **Gate G1** review (below); write the gate note in `docs/`

**Week 5 (28 Dec)**
- [ ] Mon: offer a free trial to the best 2 prospects (WhatsApp script 3)
- [ ] Mon: A-V1 run stages and hospital list
- [ ] Thu: draft the trial letter (§4.4) for each prospect
- [ ] Thu: 10 new contacts (corporate and event fleets)

**Week 6 (4 Jan)**
- [ ] Mon: start trial 1 (install, train crews)
- [ ] Mon: daily data check begins
- [ ] Thu: fix the top 3 bugs; second prospect follow-up
- [ ] Thu: C-V1 monthly PDF started

**Week 7 (11 Jan)**
- [ ] Mon: visit trial 1; collect complaints
- [ ] Mon: legal check L1 (find the 2020 gazette notification), see [alert_message_spec.md §4c](alert_message_spec.md#4c-blocking-legal-check-l1-phone-screens-while-riding-or-driving)
- [ ] Thu: start trial 2 if signed
- [ ] Thu: B-V1 road ETA

**Week 8 (18 Jan): Gate G2**
- [ ] Mon: mid-trial report to trial 1 (day 14)
- [ ] Thu: **Gate G2** review; gate note
- [ ] Thu: check the PRAYAS call at CIE and i-TIC; draft the application ([CIE](https://cie.iiit.ac.in/dst-nidhi/), [i-TIC](https://itic.iith.ac.in/nidhi-prayas.html))

**Week 9 (25 Jan)**
- [ ] Mon: offer one custom build to a trial customer if they asked for something specific (§2 stream 2)
- [ ] Mon: D-V1 test mode (for the paper)
- [ ] Thu: 10 new contacts; aim for trial 3
- [ ] Thu: submit the PRAYAS application if a call is open

**Week 10 (1 Feb)**
- [ ] Mon: day-21 draft report to trial 1; "Who would you show this to?"
- [ ] Thu: prepare the invoice and the founding-price offer
- [ ] Thu: paper: literature search, 2 hours

**Week 11 (8 Feb)**
- [ ] Mon: **decision meeting with trial 1** (day 28); bring the invoice
- [ ] Thu: same for trial 2 if it is at day 28
- [ ] Thu: if a "no", run the §5.3 playbook within 48 hours

**Week 12 (15 Feb): Gate G3**
- [ ] Mon: send the first invoice, or write the reasons for each "no"
- [ ] Thu: **Gate G3** review; update [business_plan.md §10](business_plan.md#10-financial-model-three-scenarios-all-estimates) with real numbers
- [ ] Thu: plan weeks 13-24 (native app E-V0, paper RQ1)

### Gates and kill criteria (ESTIMATE thresholds)
| Gate | When | Pass | If it fails |
|---|---|---|---|
| **G1** | Week 4 | A-V0 works on 2 phones on a real drive; ≥30 contacts; ≥6 conversations with owners or managers; ≥2 say they would try it | <2 interested: change the segment (hospital fleets or corporate) for 4 weeks. Still <2 by week 8: **stop the operator business**; keep the paper and the simulator |
| **G2** | Week 8 | ≥1 free trial running with ≥3 ambulances | No trial: offer a custom build instead (stream 2); if no one will even try it for free by week 10, stop selling and focus on grants and the paper |
| **G3** | Week 12 | ≥1 signed paid order or invoice (any amount ≥ the minimum), or a signed custom-build letter with 50% paid | **K:** zero paying customers after 2 completed trials → the price or the product is wrong; run 5 "why not" interviews, then decide: re-price once, or stop the subscription business |

---

## 4. Sales kit

### 4.1 Pricing sheet (all **ESTIMATES**, untested)
| Item | Price | Notes |
|---|---|---|
| Free trial | ₹0 for 30 days | Up to 10 ambulances; trial letter signed |
| Founding price (first 5 customers only) | ₹1,000 per ambulance per month, first 3 paid months | Then list price |
| List price | ₹1,500 per ambulance per month | Includes crew app, dispatch board, ETA links, monthly report |
| Minimum | ₹5,000 per operator per month | After the founding period |
| Setup and training | Free for founding customers; ₹5,000 later | One visit, up to 2 hours |
| Custom build | ₹25,000-75,000 fixed per project | 50% upfront, 50% on delivery; scope in writing |
| Corporate or campus fleet | ₹1,500-2,500 per vehicle per month + ₹10,000 setup | SLA report included |
| Alert simulator demo | Free | It is a demo, not a product |
| Taxes | GST if and when registration applies; ask a CA | **UNVERIFIED** threshold |

### 4.2 One-page offer for operators
Use the longer version in [pitch_outline.md Part B](pitch_outline.md#part-b-one-page-operator-pitch-print-or-whatsapp-pdf) as the base, with these terms:

> **See every ambulance live. Prove your response times.**
> - Works in the browser of any Android phone in the ambulance. Nothing to fit.
> - Live map for your dispatcher. One-tap run stages for the crew.
> - A live ETA link you can WhatsApp to the hospital.
> - A monthly response-time report to show hospitals and corporate clients.
> - No patient data collected. Your data is yours.
>
> **Offer:** 30 days free for up to 10 ambulances. Then ₹1,000 per ambulance per month for 3 months (founding customers only), then ₹1,500. Cancel any month.
> **We agree on day 1** what success looks like: at least 80% of runs tracked, the dispatcher uses the map most days, and you use the report or ETA link with a client.
> **Contact:** [name], [phone], [email]

### 4.3 Five-minute demo script
| Time | Show | Say |
|---|---|---|
| 0:00-0:30 | Nothing; listen | "How do you dispatch today? What does a hospital ask you for?" (Use their words later.) |
| 0:30-1:30 | Dispatch map with 2 test ambulances | "This is your control room on one screen: who is free, who is on a run, last seen." |
| 1:30-2:30 | Your phone as the crew app: tap Start run, Dispatched, At scene | "The crew taps one big button per stage. That's all they do." |
| 2:30-3:15 | Share the ETA link to their WhatsApp | "The hospital sees the ambulance coming. No login, no patient details. The link dies when the run ends." |
| 3:15-4:00 | Sample monthly report (test data, labelled **sample**) | "This is what you can show a hospital or a company: median times, per ambulance." |
| 4:00-4:30 | Alert simulator, 20 seconds, labelled **simulation** | "Later: drivers ahead hear 'move left if safe' in Telugu, Hindi or English. This is a simulation today." |
| 4:30-5:00 | The offer | "30 days free for your ambulances, then you decide. Can we start on [date]?" |

Rules: never show invented numbers as real; say "sample" and "simulation" out loud.

### 4.4 Pilot or trial letter: outline (not legal advice; have it reviewed when you can)
1. Parties: [operator legal name], [founder name or company].
2. Scope: crew web app, dispatch board, ETA links, reports for [N] ambulances from [start] to [end, 30 days].
3. Price: free during the trial; after the trial, [₹/ambulance/month] if the operator continues; either side can stop with 7 days' notice.
4. Success measures (the 3 in §2.2) and the decision date.
5. Operator duties: one contact person, phones for the crews, the crew's consent to location tracking during runs only.
6. Data: the operator owns its data; the founder processes it only to provide the service; no patient data is entered; data deleted or returned within 30 days of the end ([privacy_design.md §5](privacy_design.md#5-ambulance-operators-and-108-data)).
7. No guarantee: the tool supports dispatch; it does not replace the operator's judgement or legal duties; the alert feature is not included.
8. Liability: limited to fees paid (founder has no insurance yet; say so).
9. Reuse: the founder may reuse general code and anonymous, aggregated statistics; never the operator's name or data without permission.
10. Signatures and date.

For a custom build add: deliverables, 50% upfront, delivery date, one round of changes, and who owns the custom parts (**OPINION:** the operator gets a licence; you keep the code).

---

## 5. Risks and responses

### 5.1 Build risks
| Risk | Likelihood (OPINION) | Response |
|---|---|---|
| Browser stops GPS when the screen turns off | High | Wake lock; phone mounted and charging; show "tracking paused" loudly; measure in week 2 |
| AI-written code has security holes (one operator sees another's data) | Medium | Supabase row-level security; ask for a security review per feature; test with 2 operator accounts |
| Free tiers pause, change or hit limits | Medium | Read pricing pages; keep a backup export; move to paid hosting only from revenue |
| GPS errors near flyovers make ETAs wrong | Medium | Show ETA as a range; tell hospitals it is an estimate |
| Native Android app slips months | High | It is not needed for revenue in weeks 1-12; simulator covers demos |
| Building on CBIT resources gives CBIT the IP | Medium-High | Own laptop and own network until settled (see the deferred note at the top) |

### 5.2 Selling risks
| Risk | Likelihood (OPINION) | Response |
|---|---|---|
| No one takes a meeting | High | Walk-ins at stands, then calls; 40 contacts per fortnight; ask every contact "who else?" |
| Interest but no payment after the trial | High | Price and success measures agreed on day 0; invoice at the day-28 meeting |
| Big operators build their own | High | Target small and mid operators |
| Crews refuse tracking | Medium | Track during runs only; show the privacy promise; the owner decides |
| Founder looks too junior | Medium | Demo on real phones, a clear one-pager, honest "known limits" list |
| Pilot turns into free support forever | Medium | Free only for 30 days, written; one extension maximum |

### 5.3 When an operator says no
| What they say | What it may mean | Do this |
|---|---|---|
| "We don't need it; we use WhatsApp." | Pain is low | Ask: "What happens when a hospital asks for response times?" If no pain, thank them and ask for one referral; mark "no pain" |
| "Too expensive." | Value unclear or price wrong | Ask what they pay for GPS today; offer reports only at a lower price; record the number they name |
| "Crews won't use it." | Adoption risk | Offer a 7-day test on 1 ambulance; simplify to Start and End only |
| "We already have GPS." | Tracking is not the value | Show the report and ETA link, which their GPS may not give; ask if their GPS exports times |
| "Come back later." | Not a priority | Agree a date; send a monthly 2-line update; move on |
| "Who are you? Are you a company?" | Trust | Show the CBIT student ID, the one-pager, the demo; offer the free trial with the written letter |
| Silence after the demo | Usually "no" | Day 2, 7, 14 follow-ups (§2.1); then close the lead |

After every "no": write the reason in the sheet the same day. After 5 "no"s with the same reason, change the product or the segment, not the script. **OPINION.**

---

## 6. What this plan does not cover
1. The deferred CBIT items (top of this file).
2. Hiring, incorporation and GST: after the first paying customer ([business_plan.md §12](business_plan.md#12-funding-ask)).
3. The research timeline beyond week 12: [project_plan.md](project_plan.md) and [paper_plan.md](paper_plan.md).
