# Research gaps: what was checked, what is still open

Checked 27 Nov 2026 from a cloud container. Labels: **FACT** (linked), **ESTIMATE**, **OPINION**, **UNVERIFIED**. Not legal advice.
Confidence: High = official or mirrored text read directly; Medium = several consistent secondary sources; Low = one source, snippet, or inference.

**Blocked or unusable hosts (not guessed past):**
1. `egazette.gov.in`: no response (HTTP 000) from this environment.
2. `morth.nic.in` and `hmr.araiindia.com`: the MoRTH VTS guideline URL and the ARAI AIS-140 PDF returned an HTML page, not the PDF, so I could not read them.
3. `nhtsa.gov` PDF: HTTP 403.
4. `indiacode.nic.in` and `meity.gov.in`: reachable, but I did not read the Act or Rules text there; I used Indian Kanoon mirrors and a PIB note instead.
5. WebSearch is limited to US results and gives summaries, so many "Medium" answers rest on snippets.

## 1. Exact statute text (priority 1)

| Provision | Answer | Source | Confidence |
|---|---|---|---|
| MV Act s.194E | "Whoever while driving a motor vehicle fails to draw to the side of the road, on the approach of a fire service vehicle or of an ambulance or other emergency vehicle as may be specified by the State Government, shall be punishable with imprisonment for a term which may extend to six months, or with a fine of ten thousand rupees or with both." Says "draw to the side", not "left". | [Indian Kanoon mirror of the Act](https://indiankanoon.org/doc/132499746/). Delhi Police lists the same ₹10,000: [traffic.delhipolice.gov.in](https://traffic.delhipolice.gov.in/en/node/24) (seen in search results). | High for wording (mirror; official gazette not read) |
| Reg. 27(5)(a)-(b), Motor Vehicles (Driving) Regulations 2017 | Applies when the emergency vehicle has "its multi-toned horn and light flasher on" and is "overtaking, approaching or entering the path". Unless a police officer directs otherwise: (a) yield "by driving to the left as close as practicable to the kerb or edge of the roadway in the shortest possible time"; (b) "stop, if required, and remain stationary in that position until the emergency vehicle has passed". | [27(5)](https://indiankanoon.org/doc/21177923/) | High |
| Reg. 27(6) | Unless directed by the emergency vehicle's crew, maintain "a distance of at least fifty meters" from the emergency vehicle on which siren or flasher or both are operating. | [reg. 27](https://indiankanoon.org/doc/15262949/) | High |
| Reg. 27(3)(iv) | With siren and flasher on, an emergency vehicle may "with utmost care" drive "in either direction on a 'NO ENTRY' or a 'One Way' street". **Design consequence:** head-on ambulances on one-way roads are lawful, so "ahead, same direction" alerts cannot cover them. | [reg. 27](https://indiankanoon.org/doc/15262949/) | High |
| Reg. 37(1) base text | "The driver shall not use any hand held mobile phone or other communication device." | [Entire regulations, mirror](https://indiankanoon.org/doc/164893636/) | High for the base text |
| **Proviso to reg. 37(1), G.S.R. 586(E), 2020** (phone only for navigation, fixed on the dashboard) | **Not found in the mirror**, which shows the 2017 text without any proviso. The proviso could be missing from the mirror, or could be a later amendment. | none | **Unverified. Open.** Fetch the 2020 gazette notification from egazette.gov.in or ask a lawyer. |
| Related reg. (number not confirmed) | "The driver shall not watch digital motion pictures or videos while driving, except where required for route navigation: Provided that the driver shall use a device for route navigation in such a manner as not to distract his attention from driving." Also "ensure that loud music is not played in the vehicle." | [same mirror](https://indiankanoon.org/doc/164893636/) | Medium (regulation number not read) |

**Answer for the project:** the legal default is "left, close to the kerb, stop if needed", only when siren and flasher are on. No official exception to "left" other than a police officer's direction was found. The phone-use question stays open until the 2020 proviso is checked.

## 2. Who owns 108 ambulance data (priority 2)

**Answer: unknown. I found no 108 contract text that says who owns the data.**

| Finding | Source | Confidence |
|---|---|---|
| A CAG audit of a state e-governance project says the State Government did not have access to the project database, which impaired monitoring and research. (The search summary did not identify the state or project; this is a lead, not proof about 108.) | [CAG report](https://cag.gov.in/uploads/icisa_it_reports/f081103b45fccc4748d202e6c6ea7fbe-06245a65d635d22-75261345.pdf) | Low |
| Gujarat said data on patient referrals and ambulance use is centrally available through one organisation, 108 EMRI GHS. | [DeshGujarat](https://deshgujarat.com/?p=255329) | Low (news item) |
| Karnataka is moving 108 from the EMRI GHS PPP model to a government-run model on the 112 ERSS software; ownership terms not given. | [Deccan Herald](https://www.deccanherald.com/india/karnataka/now-health-dept-to-operate-108-ambulance-service-3585408) | Medium for the policy move; none for data terms |
| Evaluation of the 108 scheme in Andhra Pradesh by NHSRC (may contain contract points). | [NHSRC PDF](https://www.nhsrcindia.org/sites/default/files/2021-02/Evaluation_Report_108_Scheme_EMRI_in_Andhra_Pradesh.pdf) | Not read |
| Telangana 108 contract with EMRI GHS | not found | none |

**OPINION:** assume the state controls access and the operator holds the live feed; do not plan on 108 data without a written approval from the health department. Next step: request the Telangana agreement through the department or an RTI (**ESTIMATE**: weeks to months).

## 3. Do AIS-140 trackers cover ambulances? (priority 3)

**Answer: unresolved.**

| Finding | Source | Confidence |
|---|---|---|
| MoRTH inserted rule 125H in the Central Motor Vehicles Rules 1989 requiring a Vehicle Location Tracking Device and emergency button in "public service vehicles", through the 2018 VLTD and Emergency Button Order (effective date reported as 1 Apr 2018 in earlier notes and 1 Jan 2019 in another summary). | [Autocar Pro explainer](https://www.autocarpro.in/news-national/ais-140-norm-public-transport-vehicles-mean-28696) and search summaries | Medium |
| AIS-140 is the technical standard (ARAI). | [ARAI AIS-140](https://hmr.araiindia.com/Control/AIS/14201910518PMAIS-140.pdf) (blocked; HTML returned) | Not read |
| Several states (Karnataka, Goa, Odisha) describe command centres that pass emergency-button alerts to police, ambulance and fire; none states that ambulances themselves must carry the tracker. | [Tribune on Karnataka](https://www.tribuneindia.com/news/business/karnataka-govt-mandates-intelligent-transportation-system-ais-140-guidelines-on-public-vehicles-over-6-5-lakh-vehicles-to-be-fitted-with-panic-button), [Goa](https://gavlts.goa.gov.in/AIS140) | Low |
| MV Act definition of "public service vehicle" is passenger-for-hire (**from memory**, not re-read). An ambulance may not fit unless a state treats it that way. | none | Low |

**OPINION:** do not assume ambulances have AIS-140. Pings go to state backends anyway, so the app-on-the-crew-phone design stays the MVP. Next step: read rule 125H and the VLTD Order from the gazette; ask RED.Health what trackers its fleet has.

## 4. Emergency-vehicle features in Google Maps India, Mappls, Ola Maps (priority 4)

| Product | Finding | Source | Confidence |
|---|---|---|---|
| Waze | Alerts for emergency vehicles on route, only for vehicles reported by partners or editors; not on Android Auto, AAOS or CarPlay. Earlier research found rollout in the US, Canada, Mexico and France only as of Jan 2026. | [Waze Help](https://support.google.com/waze/answer/14716475?hl=en) (read); Android Authority via earlier notes | High (Waze); Medium (country list) |
| Google Maps India | India feature posts describe accident-prone area alerts, trip safety and disruption alerts; none mentions an approaching-ambulance alert. | [Google India blog](https://blog.google/intl/en-in/products/explore-communicate/google-maps-in-india-keeping-you-informed-with-new-safety-disruption-alerts/) (seen in results, not read in full); [TechCrunch Nov 2025](https://www.techcrunch.com/2025/11/06/google-maps-upgrades-navigation-in-india-with-gemini-safety-alerts/) | Medium that no such feature is announced; absence is not proof |
| Mappls (MapmyIndia) | Sells dispatch and routing tools for ambulance control rooms; police MoUs mention sharing ambulance positions with the Mappls app in Uttar Pradesh and Punjab; driver alerts cover speed breakers, signals, waterlogging; no confirmed driver-facing ambulance alert. | [Mappls emergency response](https://about.mappls.com/government-smart-city-solutions/emergency_response.php) (read); [UP Police MoU](https://www.marketscreener.com/quote/stock/C-E-INFO-SYSTEMS-LIMITE-130945925/news/C-E-Info-Systems-Limited-Signs-MoU-Between-Uttar-Pradesh-Police-and-Mapmylndia-41867515/) | Medium; MoU features may not have shipped |
| Ola Maps | **Nothing found.** | none | Unknown |

**Answer:** no confirmed driver-facing ambulance-approaching alert in any of the three Indian-market map products. This is absence of evidence and could change. Re-check the release notes before any pitch.

## 5. Human-factors research on audio alerts for two-wheeler riders (priority 5)

**Answer:** small, mixed evidence. Nothing I found proves that audio-only alerts help riders react faster.

| Finding | Source | Confidence |
|---|---|---|
| A US DOT connected-motorcycle warning study (2016) tested auditory, visual and haptic prototypes; most riders preferred combined modes; simple speech or haptics could fix weak directional information. | [ROSA P PDF](https://rosap.ntl.bts.gov/view/dot/30671/dot_30671_DS1.pdf) (abstract-level) | Medium |
| A 2026 simulator study of a helmet-integrated multimodal HMI (N=13) found no significant effect on reaction time or safety margins. | [preprint](https://bazilinskyy.github.io/publications/vanheuvelen2026second) | Low (small N, preprint) |
| Simulator studies found riders' reaction times longer and more variable than car drivers'. | [Connected Motorcycle Consortium work, via search](https://www.mdpi.com/2624-8921/3/4/50/htm) | Low |
| EEG study: spoken rear-end warnings raised motorcyclists' alertness (physiological, not reaction time). | [IEEE Access via search](https://bvbvf1.bib-bvb.de/vufind/PrimoRecord/cdi_proquest_journals_2455872953) | Low |
| TU Dresden work on auditory alert design for riders, considering helmet and ambient noise. | [portal](https://fis.tu-dresden.de/portal/en/publications/enhanced-motorcycle-safety-through-the-development-and-evaluation-of-auditory-alert-system(be22cd90-c1c8-4754-a5c0-eeb3a5c24441).html) | Low (abstract only) |
| For emergency-vehicle alerts specifically (car drivers): Swedish and Australian simulator studies show earlier yielding with warnings. | [Frontiers 2020](https://www.frontiersin.org/articles/10.3389/frsc.2020.00019), [SWOV](https://swov.nl/en/publicatie/detection-emergency-vehicles-driver-responses-advance-warning-driving-simulator) | Medium |

**Gap:** no study of Indian riders, Indian road noise, or emergency-vehicle alerts for riders. This is a publishable gap only if a proper literature search confirms it (see the paper plan).

## 6. Other items from the evaluation's "could not verify" list: status

| Item | Status now |
|---|---|
| DPDP Rules notification date | PIB says **14 Nov 2025**; some sources say 13 Nov (gazette date). Use 14 Nov for the Rules' notification and note the discrepancy. [PIB note](https://static.pib.gov.in/WriteReadData/specificdocs/documents/2025/nov/doc20251117695301.pdf). Medium-High. |
| DPDP penalties | PIB: up to ₹250 crore for security failure; up to ₹200 crore for breach non-notification and children's obligations; up to ₹50 crore otherwise. High (same PIB note). |
| DPDP phase-in | About 18 months (PIB); consent-manager rules from about 14 Nov 2026 and main duties about 12 May 2027 per law-firm summaries. Medium. |
| Telangana Act 21 of 2026 | Act text at [PRS](https://prsindia.org/files/bills_acts/acts_states/telangana/2026/Act21of2026TG.pdf) (not read in full). Summaries: in force 2 Jun 2026, rules notified 14 Nov 2026, welfare fee up to 2% of payouts, data submission duty on aggregators. Reports conflict on dates and on algorithm clauses. Medium-Low. |
| NHTSA 2 s / 12 s | Confirmed as voluntary Phase 1 guidelines for built-in devices ([Federal Register](https://www.govinfo.gov/link/fr/78/24861)); primary PDF 403. Medium-High. |
| ISO 15008 | Standard exists, 2017 edition, confirmed in 2025 ([ISO](https://www.iso.org/standard/62784.html)); text paid. ISO 15005: **not verified**. |
| Siren-detection accuracy, systematic Indian patent search, hospital in-house fleets, insurance for startups, micro-payout tax | Not worked on in this pass. Still open. |

## 7. Still open (ranked)

1. 2020 proviso to reg. 37(1): get the gazette text. **Now blocking** (legal check L1) for any two-wheeler screen; owner: founder; due week 7 (11-17 Jan 2027). See [alert_message_spec.md §4c](alert_message_spec.md#4c-blocking-legal-check-l1-phone-screens-while-riding-or-driving).
2. Telangana 108 contract data clauses.
3. Whether rule 125H covers ambulances.
4. Ola Maps and current Google Maps India features: re-check.
5. ISO 15005 and a proper human-factors literature search.
6. DPDP Act and Rules article numbers from the official text.
