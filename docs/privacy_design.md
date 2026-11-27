# Privacy by design (DPDP Act 2023 and Rules 2025)

Status: design draft. **Not legal advice.** See section 8 for questions to put to a lawyer.
Labels: **FACT** (with link), **ESTIMATE**, **OPINION**, **UNVERIFIED**.

Goal: the server never learns where any individual driver is, and no patient data exists anywhere in the system.

## 1. Core design: on-device matching

1. The crew app sends the ambulance's position and route to the backend (vehicle ID and position only).
2. The backend predicts the route and publishes only a **corridor**: a polygon of road segments plus a time window, signed by the backend. It publishes to a coarse **area topic** (for example a geohash cell of about 5 km, **ESTIMATE**).
3. A driver phone subscribes to the cells it is in or near. It checks locally whether it is inside the corridor, ahead of the ambulance and moving the same way, then decides whether to alert.
4. The driver's location never leaves the phone. The server sees only "some device subscribed to cell X".

| | On-device matching (proposed) | Server-side matching |
|---|---|---|
| Privacy | Server sees no driver location. A phone only reveals its coarse cell through the topic it subscribes to. | Server holds a live location of every driver: a DPDP data-fiduciary duty and a breach target. |
| Latency | One broadcast from server to phones. **ESTIMATE** (to be measured): the same or lower than server matching, as the server does not look up each driver. | Server must match, then push to each driver. |
| Battery | Phone runs location in a foreground service and does a cheap point-in-polygon test. Extra CPU is small. **ESTIMATE**, to be benchmarked. | Phone must also send location often: radio use costs more battery. |
| False alarms | Depends on phone GPS and map matching; the corridor must be generous. Slightly higher risk of both over- and under-alerting. | Server can use better snapping, but only as good as the uploaded GPS. |
| Cost | Cheaper (no per-driver state). | Needs per-driver state and a stream of location messages. |
| Auditing | Harder to audit alert outcomes unless drivers opt in to log. | Easy to audit; easy to abuse. |

**OPINION:** on-device matching is the better default. **Open problem:** the geohash cell a phone subscribes to still reveals a coarse area. Mitigation: subscribe to a larger neighbourhood (the cell and its 8 neighbours) so the cell does not pinpoint the phone, and do not log subscriptions.

### Signed alerts
1. Each crew device has a key pair registered by the operator. The backend verifies the crew message and signs the corridor with a backend key (Ed25519, **OPINION**).
2. Driver apps ship the public key and reject any unsigned or expired corridor (validity window of 60 s at most).
3. Replay protection: include a sequence number and a timestamp; reject old ones.
4. This stops someone from making a fake ambulance alert by writing to a topic. It does **not** stop a crew member who sets "emergency" falsely; handle that through operator audit.

## 2. Ambulance-side data

| Item | Decision |
|---|---|
| Collected | Vehicle ID (operator's own ID, not the registration number if avoidable), position, speed, heading, time, "emergency run" flag, siren/flasher flag. |
| Never collected | Patient name, caller number, diagnosis, hospital admission, pickup address, crew personal identity beyond a role ID. |
| Hospital | Only a destination point (lat, lon) chosen from a list. Not linked to a case ID. |
| Retention | Raw tracks 30 days (**ESTIMATE**), then aggregated per road segment (speed, count) with no vehicle ID. Aggregates kept longer. |
| Crew | The crew are people too: a crew member's phone location is personal data. Get consent from the operator and crew; location only during a run. |
| Link to patients | **Never join ambulance tracks with patient or case data.** If an operator wants this for its own purposes, it must do that in its own system. |

## 3. Pilot data (research and measurement)

1. **Opt-in consent** in the driver app, in the user's language, before any location is logged. Separate toggles: (a) get alerts (on-device only); (b) share anonymous trip data for research (optional).
2. **Pseudonymous IDs:** random per-install ID, rotated every 7 days (**ESTIMATE**).
3. **Separate research dataset**, kept apart from operations, with only segment-level speed and alert-response outcomes. No raw home or work locations: trim 200 m from the start and end of any logged trace, and drop traces from known fixed points.
4. **Retention:** a fixed period stated in the notice (propose 6 months, then delete or aggregate; **ESTIMATE**).
5. **Withdraw** any time in the app; delete the pseudonymous ID's data within 30 days (**ESTIMATE**; the Rules allow up to 90 days for access, correction and erasure requests, [PIB note](https://static.pib.gov.in/WriteReadData/specificdocs/documents/2025/nov/doc20251117695301.pdf)).
6. Ethics-committee approval for the pilot (see [paper_plan.md](paper_plan.md)).

## 3b. Where DPDP applies and where it may not

If the phone matches locally and sends nothing, the founder may not "process" the driver's location at all; the processing is on the user's own device. **UNVERIFIED legal question for a lawyer.** Once the app uploads opt-in logs, the founder becomes a Data Fiduciary for that data.

## 4. DPDP duty map

Dates: Rules notified 14 Nov 2025, with an 18-month phase-in ([PIB note](https://static.pib.gov.in/WriteReadData/specificdocs/documents/2025/nov/doc20251117695301.pdf); other sources say the gazette is dated 13 Nov). Consent-manager rules are due about 14 Nov 2026 and the main duties about 12 May 2027 ([law-firm summaries, not primary](https://www.scconline.com/blog/post/2025/12/26/digital-personal-data-protection-rules-2025-key-highlights/)). **UNVERIFIED:** exact rule numbers and commencement dates; read the Rules text on [meity.gov.in](https://www.meity.gov.in/) or [egazette.gov.in](https://egazette.gov.in/) (the egazette host did not respond from this environment). Act section numbers below are from my knowledge of the Act and **not re-read in this session**.

| Duty | Act ref (check) | What it requires | Status in this design |
|---|---|---|---|
| Notice | s.5 | Itemised notice of what data, why, how to withdraw, how to complain. PIB confirms a separate, clear consent notice stating the specific purpose. | **Needed**: one-page notice below, shown in-app in 4 languages. |
| Consent | s.6 | Free, specific, informed, unconditional, unambiguous, withdraw as easily as given. | **Done by design** for the optional research logging; alerts need no server-side personal data. |
| Purpose limitation | s.4, s.6 | Use data only for the stated purpose. | **Done by design**: research logs are never used for ratings, ads or sale. |
| Data minimisation | principle (PIB) | Collect only what is needed. | **Done by design**: no server-side location in default mode. |
| Accuracy | s.8(3) | Keep data accurate if used to decide about someone. | **Not applicable** (no decisions about individuals). |
| Retention and erasure | s.8(7) | Delete when the purpose ends or consent is withdrawn. | **Needed**: automatic deletion jobs; test them. |
| Security safeguards | s.8(5) | Reasonable safeguards; top penalty up to ₹250 crore ([PIB note](https://static.pib.gov.in/WriteReadData/specificdocs/documents/2025/nov/doc20251117695301.pdf)). | **Needed**: encryption in transit and at rest, key management, access logs, least privilege. |
| Breach notice | s.8(6) | Tell the Board and affected people; penalty up to ₹200 crore (PIB). | **Needed**: a written incident plan; if no location is stored server-side, impact is small. |
| Grievance and contact | s.8(10) | Publish contact of a responsible person. | **Needed**: an email and a named person in the app. |
| Data principal rights | s.11-14 | Access, correct, erase, nominate; respond within 90 days (PIB). | **Needed**: simple email or in-app process. |
| Children | s.9 | Verifiable parental consent; no tracking or behavioural monitoring of children. PIB notes an exception for real-time safety. | **Needed**: 18+ only in the pilot; no sign-up under 18. Delivery riders under 18 must not be recruited. |
| Section 7 "legitimate uses" | s.7 | Allows processing without consent for listed uses, including a medical emergency that threatens life or health. | **Not relied on.** **OPINION:** do not rely on the emergency limb for routine app data; consent is cleaner. A lawyer should say whether it covers the ambulance-side data. |
| Significant Data Fiduciary | s.10 | Extra duties for notified large entities. | **Not applicable** at pilot scale. |
| Consent managers | Rules (check rule no.) | Optional platform for consent. | **Not applicable** now. |
| Cross-border transfer | s.16 | Allowed unless restricted by notification. | **Needed**: host servers in India (**OPINION**, simpler). |
| Research exemption | s.17(2)(b) | Research or statistical use exempt if the data is not used to decide about a person and standards are met. | **Possibly useful**; **UNVERIFIED**. Do not rely without legal advice. |

## 5. Ambulance operators and 108 data

1. For a private operator, the operator is the Data Fiduciary for its own tracking data. The founder is a processor under a written contract.
2. For 108 (state), data ownership is **unverified**: I found no contract text. See [research_gaps.md](research_gaps.md). A CAG audit noted a state without access to a project's databases; Gujarat says 108 data is held centrally by EMRI GHS.
3. Never sign a 108 data deal with the operator alone; get the state health department's written approval.

## 6. Gig-worker law and rider surveillance

1. **Telangana Platform Based Gig Workers (Registration, Social Security and Welfare) Act 2026 (Act 21 of 2026)**, [Act text](https://prsindia.org/files/bills_acts/acts_states/telangana/2026/Act21of2026TG.pdf). Press and law-firm summaries say the Act is in force from 2 June 2026, the rules were notified 14 Nov 2026, aggregators must submit worker databases, and pay a welfare fee up to 2% of payouts ([summary](https://www.dcpsol.com/telangana-platform-based-gig-workers-rules-2026)). **UNVERIFIED:** I did not read the Act or Rules text; algorithm and data-use clauses need checking.
2. The Code on Social Security 2020 also covers gig and platform workers (**not read in this session**).
3. **Design rules (OPINION):**
   1. The app does not report to a rider's platform, employer or union. No individual data is shared with a platform.
   2. Alert behaviour (who moved, who did not) is never used for ratings, rewards, penalties or e-challans in the pilot.
   3. The platform API (see [mvp_architecture.md](mvp_architecture.md)) carries no rider data back to us.
   4. Recruit through the union with written consent; no pressure from platforms.
   5. Publish this promise in the notice.

## 7. Plain-language privacy notice (draft, one page)

> **Ambulance Alert: your privacy**
>
> **What this app does.** When an ambulance on an emergency run is coming up behind you, the app tells you by voice to move left, or to stay where you are. It is not a rule-checking or scoring app.
>
> **Where you are.** Your phone checks your location **on the phone itself**. By default, your location is **not** sent to us. We only send your phone the ambulance's route. We do not know who you are or where you are.
>
> **Optional research sharing.** If you say yes, we log how the alert worked: time, your speed near the alert, and whether you moved over. We remove your home and work areas and use a random ID, not your name or phone number. We keep it for 6 months, then delete or combine it. This is only for research and to improve the alert.
>
> **What we never do.** We never sell your data. We never tell your company or platform what you did. We never use it to rate you, pay you or punish you. We never collect patient information.
>
> **Your choices.** You can switch off research sharing or stop alerts at any time in Settings. You can ask us to see, fix or delete your data. We answer within 90 days.
>
> **Safety.** The app helps you notice an ambulance. You decide what is safe. Move left only if it is safe. Do not touch the phone while riding or driving.
>
> **Who to contact.** [Name, email, address to be filled]. You can also complain to the Data Protection Board of India.
>
> **You must be 18 or older to use this app.**

## 8. Questions for a lawyer

1. If matching is fully on-device and nothing is uploaded, is the founder a Data Fiduciary for driver location at all?
2. Does section 7 (medical emergency) cover ambulance-side tracking without consent, and should we rely on it?
3. Is a pseudonymous research dataset "personal data"? Does the s.17(2)(b) research exemption apply to a student pilot?
4. Who owns Telangana 108 GPS data under the EMRI GHS agreement, and can a startup receive it?
5. Does the Telangana Act or Rules limit "nudging" or monitoring riders, even if the app is not the platform's?
6. What liability follows if a rider is hurt after an alert? Is a terms-of-use disclaimer enforceable? (Budaun 2024 named a Google Maps manager in an FIR.)
7. Does a phone-as-navigation exception (the 2020 proviso to reg. 37(1)) cover a voice alert on a two-wheeler?
8. What contract and indemnity should we sign with an ambulance operator (processor terms)?
9. Does the app need a registered entity and an in-India data-protection contact before a pilot?
10. What cheapest professional-indemnity cover is available to a student startup?

## 9. Not verified

1. DPDP Act section numbers and Rules rule numbers (from memory); commencement dates (secondary sources).
2. Whether s.7 or s.17 fits this design.
3. Telangana Act and Rules wording on algorithms and data.
4. Primary hosts: egazette.gov.in did not respond; the Act PDF on prsindia.org and PIB were reachable; the DPDP Act and Rules text from indiacode.nic.in and meity.gov.in were not read.
