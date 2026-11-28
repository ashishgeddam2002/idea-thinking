# Research paper plan

Status: plan only. No experiment has been run. Labels: **FACT** (linked), **ESTIMATE**, **OPINION**, **UNVERIFIED**.
**No novelty or patent claim is made.** The contribution is an *evaluation* of known ideas in an Indian setting.

## 1. Working title

"On-device corridor matching for emergency-vehicle alerts in Indian mixed traffic: latency, battery, message design and simulated travel-time effects" (working title; **simulated results will be labelled simulated and unvalidated**).

## 2. Research questions

| # | Question | Method |
|---|---|---|
| RQ1 | Can on-device corridor matching deliver an alert within a target time (X = 5 s median, 15 s p95; **ESTIMATE**, from the MVP gates) on low-cost Android phones from 5 brands, without the server learning driver locations? | Latency and battery benchmark |
| RQ2 | Which message design (voice, banner, vibration, wording) gets the legally correct response (move left, or stay put when left is blocked) fastest and most reliably in Indian mixed traffic? | Usability study |
| RQ3 | In a simulated Hyderabad corridor with heavy two-wheeler traffic, how does ambulance travel time change with no alert, alerts at different response rates, and signal preemption? | SUMO simulation (**simulated only**) |
| RQ4 (optional) | In a consented field pilot, do alerted riders slow down or move left more often than controls? | Field pilot |

RQ1 and RQ2 are measurable by one student. RQ3 depends on assumptions I cannot verify. RQ4 needs approvals that may not arrive in six months.

## 3. Related work to position against (no novelty claims)

| Work | What it is | Source / status |
|---|---|---|
| HAAS Alert Safety Cloud (US, EU) | Responder vehicles report while lights are on; alerts reach Waze, Apple Maps and carmakers. | Company claim; see [evaluation report](https://github.com/ashishgeddam2002/BLATTA/blob/claude/ambulance-alert-india-analysis-b8uz09/reports/India%20ambulance%20alert%20evaluation.md). |
| Waze emergency-vehicle alerts | Alerts for emergency vehicles on route; only for reported vehicles; not on Android Auto or CarPlay. | [Waze Help](https://support.google.com/waze/answer/14716475?hl=en) (read directly). |
| Dutch Talking Traffic / Flitsmeister | National feed of ambulance data to apps since 2022 (from earlier research). | [research notes](https://github.com/ashishgeddam2002/BLATTA/tree/claude/ambulance-alert-india-analysis-b8uz09/research_notes/India%20ambulance%20alert%20evaluation); primary source not re-checked. |
| Swedish EVA simulator studies | FM-radio "Emergency Vehicle Approaching" messages made drivers yield sooner. | [Frontiers 2020](https://www.frontiersin.org/articles/10.3389/frsc.2020.00019); [GUPEA thesis](https://gupea.ub.gu.se/handle/2077/77614). |
| Australian in-vehicle advance warning | Simulator study of a 300-400 m warning. | [SWOV record](https://swov.nl/en/publicatie/detection-emergency-vehicles-driver-responses-advance-warning-driving-simulator). |
| FHWA connected-vehicle alerts | Simulator study with mixed automation. | [FHWA](https://highways.dot.gov/media/49166). |
| Chennai mSiren (2023) | Junction LED boards and loudspeakers warn traffic 200 m ahead of hospital ambulances. | From earlier research notes (DT Next); not re-checked. |
| Signal preemption (Opticom/Miovision; Indian ITMS) | Gives green lights to ambulances; US field studies measured 14-23% faster trips. | From earlier research notes; not re-checked. |
| US8483651B1 (Sprint) | Alerts phones within a set distance of an emergency vehicle. | Patent number as in earlier notes; **not re-read; no legal opinion**. |
| US10832579B2 (Accenture) | Dispatch, route data to police and signal control. | Same caveat. |

**Gap this paper addresses (OPINION):** I did not find a published evaluation of on-device matching with Indian road geometry and low-cost phones, or of alert wording in Telugu, Hindi and English (Urdu later). A real literature search is needed before writing this claim; I did not do a systematic search. State it only as "to our knowledge, after a search of X, Y, Z".

## 4. Methods

### 4.1 SUMO simulation (RQ3)
1. Pick a corridor, for example Gachibowli to Jubilee Hills (as in the evaluation report). Import it from OpenStreetMap with `netconvert`.
2. Traffic mix heavy on two-wheelers and autos. SUMO's default car-following models do not capture lane-less two-wheeler filtering well; use a sublane model (`--lateral-resolution`) and document its limits. **Mixed-traffic calibration data is unavailable** unless the founder collects GPS or counts; without it the results are illustrative only.
3. Scenarios: (a) no alert; (b) alert with driver response rate r = 10, 30, 50, 70% (assumed; no Indian measurement yet); (c) signal preemption only; (d) both. Several demand levels, including near gridlock.
4. Metrics: ambulance travel time, time below 10 km/h, effect on other vehicles, number of stops.
5. **Every figure and table is labelled "simulated, unvalidated, assumed parameters".** Never present as measured. This follows the rule already used in the BLATTA project's CLAUDE.md for simulated numbers ([BLATTA](https://github.com/ashishgeddam2002/BLATTA/blob/claude/ambulance-alert-india-analysis-b8uz09/CLAUDE.md)).
6. Sensitivity analysis: response rate, share of two-wheelers, compliance direction, gridlock.

### 4.2 Latency and battery benchmark (RQ1)
1. 5 Android brands (for example Xiaomi/Redmi, Realme, Samsung, Oppo or Vivo, Motorola or OnePlus), 2 phones each if possible. Mid and low price tiers.
2. Test: corridor published at known times; phone logs receive time; compare to server time with measured clock offset. 500 messages per phone per condition (screen on, screen off, battery saver, app in background, after 6 h).
3. Metrics: p50, p95, p99 latency; delivery rate; battery drain per hour over a 2-hour trace with the foreground service.
4. Compare on-device matching with a server-side-matching baseline built for comparison only.
5. Brand differences are part of the finding (battery-manager behaviour; [dontkillmyapp.com](https://dontkillmyapp.com/)).

### 4.3 Usability study (RQ2)
See the test plan in [alert_message_spec.md](alert_message_spec.md): lab with 20 participants, then a roadside test with no real ambulance. Measures: correct-action rate, time to correct action, subjective workload (NASA-TLX or a short form), comprehension by language (English, Telugu, Hindi). Ethics approval first.

### 4.4 Optional consented field pilot (RQ4)
Only after: ethics approval, operator and police written approval, no incident in 4.3. Alerts on alternate runs or days as a control; opt-in riders; pseudonymous logs per [privacy_design.md](privacy_design.md). If approvals do not arrive, omit it and list it under future work.

## 5. Metrics and analysis

| Metric | Used in | Note |
|---|---|---|
| Alert latency (p50, p95) | RQ1 | Gates in the MVP doc are **ESTIMATES**. |
| Delivery rate | RQ1 | Include dropped alerts. |
| Battery per hour | RQ1 | Same phone, same trace. |
| Correct-action rate and time | RQ2 | Binary and continuous. |
| Ambulance travel time | RQ3 | **Simulated.** |
| Speed change and lane shift of alerted riders | RQ4 | Needs consented logs. |

Statistics: report medians and bootstrap confidence intervals; for the small N usability study use non-parametric tests; pre-register hypotheses informally in the repo before running.

## 6. Threats to validity

1. Simulation: assumed response rates; no calibration to Hyderabad; SUMO's limits for lane-less traffic. **The central threat; say so on the first page.**
2. GPS and map matching error in dense urban areas (flyovers, service roads).
3. Small sample, volunteer bias, young male riders over-represented.
4. Lab or roadside behaviour is not behaviour under real stress or a real siren.
5. Phone sample of 5 brands is not India-wide.
6. Hawthorne effect: knowing one is in a study.
7. Language: translations were drafted by the model; native-speaker validation needed.
8. Evidence gaps: no published field result that alerts shorten ambulance trips (see the spec's evidence table).

## 7. Ethics and approvals

1. **Institutional ethics committee (IEC or IRB) approval at the founder's institute before any human-participant work**, including the lab test. UNVERIFIED which body applies; ask the supervisor.
2. Informed consent in the participant's language; right to withdraw; no payment tied to compliance; participants must be 18 or older.
3. DPDP compliance for any logs (see the privacy doc). **Not legal advice.**
4. **No real-ambulance test without the operator's and the police's written approval.** No simulated siren on a public road.
5. Stop rules: any near-miss ends the session.
6. No claims about patient outcomes.
7. Data sharing: release only aggregated or synthetic data.

## 8. Venues and deadlines

Checked on 27 Nov 2026 by web search. Most dates come from third-party trackers, so **confirm on the official site before relying on them**.

| Venue | What I found | Fit |
|---|---|---|
| IEEE ITSC 2027 (Boston, about 21 Sep 2027) | Paper deadline **1 Mar 2027** per a [third-party listing](https://www.myhuiban.com/conference/853?lang=en-us); the 2026 deadline was also 1 Mar. Official page not found. | Possible for RQ1 and RQ3 only (simulation and benchmark). Tight: about 3 months. |
| IEEE VTC2027-Spring (Hamburg, 20-23 Jun 2027) | Regular paper deadline 1 Sep 2026 on the [official page](https://events.vtsociety.org/vtc2027-spring/); already passed. | Missed. |
| IEEE VTC2027-Fall (Osaka, 27-30 Sep 2027) | No official deadline found; a third-party site says 1 Feb 2027 ([myhuiban](https://www.myhuiban.com/conference/609?lang=en-us)), **unverified**. | Possible, tight. |
| COMSNETS 2027 (5-9 Jan 2027) | Deadline reported as 31 Aug 2026, passed ([myhuiban](https://www.myhuiban.com/conference/903?lang=en-us)); official page said "to be announced". | Missed. Watch COMSNETS 2028. |
| ACM COMPASS 2027 | No 2027 call found. COMPASS 2026 had deadlines around March 2026 ([compass.acm.org](https://compass.acm.org/?p=7231)). | Likely a March 2027 deadline; **unverified**. A good fit for the ICTD angle (low-cost phones, India). |
| Transportation Research Record (via TRB Annual Meeting) | The 2027 meeting (10-14 Jan 2027) had its submission window 1 Jul to 1 Aug 2026 ([TRB](https://www.nationalacademies.org/events/887/presenter-info-2)); the next cycle is likely 1 Aug 2027, **unverified**. | Good fit for the full paper including field data. |
| IEEE Transactions on ITS | No deadline information found. Rolling submission is typical for IEEE journals (**not verified**). | Best for a full journal version later. |

**OPINION:** a realistic plan is (1) a benchmark plus simulation paper for ITSC 2027 only if finished by mid-Feb, (2) otherwise aim at COMPASS or TRB 2028 (1 Aug 2027) with usability results, (3) a T-ITS journal paper later with any field data.

## 9. Six-month timeline (December 2026 to May 2027, alongside an M.Tech)

| Month | Research work | Hours per week (**ESTIMATE**) |
|---|---|---|
| Dec 2026 | Ethics application drafted and submitted; literature search; SUMO network from OSM; benchmark harness | 8 |
| Jan 2027 | Latency and battery benchmark on 5 brands; start the lab usability study after approval | 10 |
| Feb 2027 | SUMO scenarios and sensitivity runs; draft 6-page ITSC paper if going for 1 Mar | 12 |
| Mar 2027 | Submit (ITSC or COMPASS if dates hold); finish the usability study | 8 |
| Apr 2027 | Roadside test (no real ambulance) if approved; analysis | 8 |
| May 2027 | Write the long version; plan the field pilot; decide on a journal | 8 |

Dependencies: the MVP build in [mvp_architecture.md](mvp_architecture.md) runs in parallel for the first 2 months; the ethics approval gates all human-participant work; the M.Tech course load is an unknown, so the hours are guesses.

## 10. Open items

1. Systematic literature search (IEEE Xplore, Scopus, Google Scholar): not done.
2. Calibration data for SUMO (traffic counts, speeds, vehicle mix): none yet.
3. Whether the institute's ethics body covers a lab study with riders.
4. The supervisor's view on venue choice and authorship.

## 8. Resources and funding (added 28 Nov 2026)

1. **Own budget is ₹0.** Phones for RQ1 are borrowed (5 brands from friends, classmates or a CBIT lab). RQ2 participants are unpaid volunteers unless a grant pays ₹300 each (**ESTIMATE**, ₹6,000 total). RQ4 needs insurance and incentives, so it is **impossible without a grant**.
2. **Institute:** CBIT (Hyderabad) will back the work "if the paper has enough strength" (founder's words). Share the outline with the supervisor at week 23 of [project_plan.md](project_plan.md) for a strength check. Ethics committee: `[to confirm]`.
3. **Languages:** English, Telugu and Hindi only (the founder speaks all three); Urdu is future work, pending a native reviewer.
4. **Two-wheeler screen:** tested in RQ2 only if legal check L1 passes ([alert_message_spec.md §4c](alert_message_spec.md#4c-blocking-legal-check-l1-phone-screens-while-riding-or-driving)).
5. **Equal weight with the business:** see [project_plan.md §4](project_plan.md#4-keeping-the-paper-and-the-business-in-step) for shared assets and the cut order.
6. **Build risk:** the native driver app is built AI-assisted with no prior Android experience; RQ1 may slip 3-4 weeks (**ESTIMATE**, [mvp_architecture.md §6.2](mvp_architecture.md#62-timeline-estimate)).
