# MVP architecture

Status: design draft. Nothing is built or measured. Labels: **FACT** (linked), **ESTIMATE**, **OPINION**.
Related: [alert_message_spec.md](alert_message_spec.md), [privacy_design.md](privacy_design.md), [paper_plan.md](paper_plan.md).

## 1. Components

```
 Crew app (Android)  --signed position + run state-->  Backend  --signed corridor-->  Area topic (geohash cell)
                                                        |  OSRM route prediction                   |
                                                        |  corridor builder + signer               v
                                                        |                                   Driver app (Android)
                                                        v                                   local matching + voice
                                                 Log store + analysis  <--opt-in outcome logs--/
```

| Component | Job | Key choices |
|---|---|---|
| **Crew app** (Android, Kotlin) | Dispatch button ("Start emergency run"), destination from a hospital list, siren/flasher toggle, GPS every 2-3 s, sends signed messages, shows "run ended". | Foreground service while a run is active. Key pair in Android Keystore, registered by the operator. Queue and retry when offline, but drop positions older than 10 s. |
| **Backend** | Verify crew signatures, snap positions to roads, predict the route, build the corridor, sign it, publish to the area topic, store logs. | OSRM on OpenStreetMap India extract (free, self-hosted; **FACT** OSRM and OSM are open-source). One small server for the pilot. |
| **Corridor builder** | Convert the route into the next 300-800 m of OSM way segments plus a time window (now to now+90 s), refreshed every 2-3 s. | Include layer tags (bridge, tunnel) and carriageway side. Corridor expires after 10 s without refresh. |
| **Pub/sub** | Deliver corridors to phones by coarse area. | MQTT broker (for example Mosquitto or EMQX) with topics per geohash cell, or WebSocket. **OPINION:** MQTT over a held connection, not FCM, for the alert path. FCM only as a wake-up fallback. |
| **Driver app** (Android, Kotlin) | Foreground service with location, MQTT subscription for nearby cells, local point-in-corridor and heading tests, voice alert, banner (cars only), vibration. | Pre-recorded audio in 4 languages stored on the device. No account needed for alerts. |
| **Logging and analysis** | Compare ambulance speed on alerted segments against matched runs without alerts; measure delivery latency and driver response (opt-in). | Postgres or SQLite plus Python notebooks. Separate research store (see privacy doc). |

Message shape (draft):

```
Corridor {
  v: 1, vehicle: "AMB-017" (operator code), seq: 1042,
  t: 1737000000 (unix s), ttl_s: 10,
  state: "EMERGENCY_RUN" | "ENDED" | "CANCELLED",
  segments: [ {way_id, layer, dir, s0_m, s1_m, eta_s} ... ],
  pos: {lat, lon, speed_mps, heading_deg},
  sig: base64(Ed25519 signature)
}
```

No patient, caller, hospital-admission or crew-name fields.

## 2. Phone-side matching (driver app)

1. Every location fix (1 Hz while in the foreground service), snap to the nearest OSM segment with a small on-device index (tile-based, downloaded per city).
2. For each valid corridor: is my segment in `segments`, is my heading within 45 degrees of `dir`, is my time-to-arrival `eta_s` in 30-60 s (recomputed from the latest ambulance position)?
3. If yes and not rate-limited, play the alert for the matching case in [alert_message_spec.md](alert_message_spec.md).
4. If any input is older than its limit, **fail silent**.

## 3. Failure handling

| Failure | Cause | Mitigation |
|---|---|---|
| Push delay or drop | Firebase high-priority messages wake a phone but carry no latency guarantee; Firebase may downgrade them if no visible notification follows (**FACT** per Android Authority, via earlier research notes). | Alert path uses a held MQTT connection inside the driver app's foreground service; FCM is only a nudge to restart the service. Measure latency (see below). |
| Battery managers kill the app | Xiaomi, Samsung, Oppo, Vivo and others kill background apps. See [dontkillmyapp.com](https://dontkillmyapp.com/) (reachable; content not reviewed in detail). | Foreground service with a persistent notification; guided "disable battery optimisation" setup per brand; a health check that tells the user when the service stopped; recruit riders with a test phone list. |
| GPS error | Urban canyons, flyovers; error may exceed a lane width. | Corridor is generous in length, narrow in logic: match on segment and heading, not lateral offset. Prefer silence when the snap confidence is low. No lane-level claims. |
| Flyovers and service roads | Overlapping or parallel roads. | OSM layer, bridge, tunnel tags and per-carriageway ways. Layer unknown means no alert. |
| Lost network | Tunnel, weak signal. | Fail silent; never replay a stale alert. A 10 s TTL on corridors and a 5 s grace on the phone's staleness check. |
| Fake or replayed alerts | Anyone could publish to a topic. | Signed corridors, sequence numbers and a 60 s maximum validity (see privacy doc). |
| False alarm | Siren with no patient, crew forgets to end run. | Alert only in the "EMERGENCY_RUN" state with siren/flasher flag on; the crew app auto-ends the run at the destination; operator can force-cancel. |
| Crew phone dies | Battery or crash. | Crew app power warning; corridor expires after 10 s; no alert on expiry. |
| Time sync | Phone clocks drift. | Corridor carries server time; phones use a monotonic delta from their last server contact, not wall time. |

## 4. Platform API (server-to-server, no rider data)

Intended for Rapido, Swiggy, Ola Maps, Mappls or any partner. **OPINION:** they will likely say "not now"; build it as a spec and a demo.

1. The partner calls `GET /v1/corridors?cell=<geohash>` or subscribes to the same topic with a read-only token. **The partner's apps do the matching on their own devices.** We never receive rider positions.
2. Same signed corridor format as above, plus an `x-api-key` for rate limits.
3. Optional webhook: `POST /v1/corridors/events` with `{vehicle, state, cell}` only, no rider IDs.
4. Optional outcome feedback, aggregated only: `POST /v1/outcomes` with segment-level counts ("alerts shown: 40; slowed or moved: 22"), no individual rows. Off by default.
5. Terms: partner is responsible for how and whether it shows the alert; we provide the corridor, not an instruction to any driver. The wording stays "if safe" (see alert spec).
6. Rate limits and uptime SLO are **not** promised in the pilot.

## 5. Costs (ESTIMATES in INR; not quotes). Updated 28 Nov 2026: own budget is ₹0

The founder has **no own money** to spend (only a Claude Pro plan). Everything below is free, borrowed, or gated on a grant (**[G]**). Cloud free-tier limits and India-region availability are **not checked**.

| Item | Without a grant | With a grant **[G]** (ESTIMATE) |
|---|---|---|
| Development machine, OSRM, broker | Founder's laptop; open-source OSRM, Mosquitto, Postgres | same |
| Pilot hosting | A free-tier server or database `[to check: India region, limits]`; laptop is not acceptable for a live pilot | ₹2,000-5,000 a month for one small server in India |
| Crew phones | The operator's own Android phones (a pilot condition) | Buy 2 used phones, about ₹15,000 |
| Test phones for the 5-brand benchmark | Borrowed from friends, classmates or a CBIT lab | Buy used phones, about ₹30,000 |
| Rider install bonuses, crew stipends | **Impossible: dropped** | ₹25,000-60,000 (earlier estimate) |
| Lab-study payments (20 × ₹300) | Unpaid volunteers, if ethics allows | ₹6,000 |
| Native-language review | Founder (Telugu, Hindi) + 5 volunteer speakers each | ₹2,000-5,000 per language |
| Legal advice, insurance | Free clinic or CBIT cell; **no field pilot without insurance** | `[to fill quote]` |
| Maps, SMS | None used | none |
| **Total own spend** | **₹0** | about ₹1-1.5 lakh over 6 months, as before |

## 6. Build plan (AI-assisted, no prior Android experience)

The founder has no Android experience and builds with AI help (has shipped a website this way). So the first version avoids native Android where it can.

### 6.1 Two-stage approach

| Stage | What | Tech | What it can do | What it **cannot** do |
|---|---|---|---|---|
| **A: business pilot** | Web dispatch board; web crew app (PWA) on a phone mounted and charging in the ambulance; reports; hospital ETA link | Web app, browser geolocation, Wake Lock to keep the screen on | Track an ambulance while the app is open and the screen is on; dispatch; ETA; reports. Enough for the operator pilot. | No reliable GPS with the screen off or the app in the background; the browser may pause it. No guaranteed delivery when the crew switches apps. **Cannot be the alert's crew source for a public road test.** |
| **B: alert and paper** | Native Android driver app (and later a native crew app) | Kotlin, foreground service, held MQTT connection, on-device audio | Background location, reliable alerts with the screen off, the RQ1 benchmark | Needs native skills; slower to build; battery managers still interfere ([§3](#3-failure-handling)) |

**Why:** a web or PWA driver app cannot deliver the alert: web push is not reliable enough on Android for a time-critical alert, and browsers do not allow continuous background location. Background location and reliable alerts need a native foreground service. (**OPINION**, from general platform knowledge; not tested here.)

### 6.2 Timeline (ESTIMATE)

| Weeks of [project_plan.md](project_plan.md) | Deliverable | Done when |
|---|---|---|
| 3 | Web stack and OSRM on the laptop | A route returns segments with layer tags |
| 6 | Web crew app v0 (start/stop run, GPS while screen on) | Positions reach the backend, signed by a key held server-side for the operator |
| 7 | Web dispatch board v0 | Live map of a test ambulance |
| 10-12 | ETA link, response-time report, corridor builder and signer | Report generated from test runs |
| 13-14 | Native driver app v0 (AI-assisted) | Walking test alerts at the right distance |
| 16 | 5-brand benchmark on borrowed phones | p50/p95/p99 table |
| 17 | Telugu and Hindi audio, fail-silent unit tests | Tests pass for stale, expired and bad-signature cases |

**Realistic slip (ESTIMATE):** 1.5-2 times the original 8-week build for the native part, because of no Android experience. Expect the native driver app in weeks 16-18 rather than 13-14. Stage A has less risk of slipping because it reuses web skills.

**Risk note:** AI-generated Android code can look right and still fail on foreground-service rules, battery managers and permission changes between Android versions. Mitigations: test on real borrowed phones from week 13; keep the driver app small; add unit tests for fail-silent rules; ask a CBIT student with Android experience to review `[to find]`.

**Gates** (unchanged; **ESTIMATE**): median delivery under 5 s and 95th percentile under 15 s; at least 95% of alerts delivered in the test; no safety incident.

## 7. What is not decided

1. MQTT versus WebSocket and which hosted broker; **ESTIMATE** only.
2. Whether iOS is needed (assume no in the pilot; two-wheeler riders in Hyderabad mainly use Android, **OPINION**, not verified).
3. Whether an operator will let us install the crew app (see the interview plan in the evaluation report).
4. Local vs. hosted OSRM, depending on a laptop or a ₹2,000-5,000 a month server (**ESTIMATE** from the evaluation report). With ₹0 own budget, a hosted server waits for a grant or a free tier.
5. Whether the crew side moves from the web app (stage A) to a native app (stage B) before any alert road test. **OPINION:** it must.
