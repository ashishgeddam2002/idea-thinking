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

## 5. Costs (ESTIMATES in INR; not quotes)

Monthly, assuming 1 crew app on 5-10 ambulances and 100-300 riders in Hyderabad. Cloud prices are not checked against current lists.

| Month | Build and pilot stage | Cloud | Tools and misc | Test phones and incentives | Total (about) |
|---|---|---|---|---|---|
| 1 | Crew app and backend skeleton | 1,000 | 500 | 15,000 (2 used phones) | 16,500 |
| 2 | Driver app, corridor logic, lab tests | 2,000 | 500 | 15,000 (2 more used phones) | 17,500 |
| 3 | Baseline logging with crew app, alerts off | 3,000 | 1,000 | 25,000 (rider install bonuses) | 29,000 |
| 4 | Alerts on, roadside and rider study | 4,000 | 1,000 | 35,000 (bonuses, crew stipends) | 40,000 |
| 5 | Analysis, write-up | 3,000 | 1,000 | 5,000 | 9,000 |
| 6 | Paper and operator pilot offer | 3,000 | 1,000 | 5,000 | 9,000 |
| **Total** |  |  |  |  | **about ₹1.2 lakh** |

The evaluation report gave ₹1-2 lakh for the 90-day pilot, so these figures are consistent. Larger line items: rider bonuses and crew stipends. Not included: professional-indemnity cover, legal advice, company registration, any paid map or SMS service.

## 6. Eight-week build plan (solo)

| Week | Deliverable | Done when |
|---|---|---|
| 1 | OSRM running on an India or Telangana extract; route prediction script; message format | Route for a test A-to-B path returns segments with layer tags |
| 2 | Crew app v0: start/stop run, GPS every 2-3 s, signing | Positions arrive signed and verified on the backend |
| 3 | Corridor builder and signer; MQTT broker; replay tool for recorded GPS tracks | Replayed track produces a stream of corridors |
| 4 | Driver app v0: foreground service, subscription, point-in-corridor, one English voice alert | Walking test: phone alerts at the right distance |
| 5 | All four languages (draft strings), banner, vibration, rate limit, fail-silent rules | Unit tests for stale, expired and bad-signature cases |
| 6 | Logging pipeline and baseline analysis script; opt-in consent screen | Logs from a test run give per-segment speed |
| 7 | Brand benchmark: latency and battery on 5 Android brands; battery-manager setup flows | Table of p50 and p95 latency per phone |
| 8 | Lab usability test (section 8 of the alert spec), fix list, go or no-go | Decision recorded; list of top 10 defects |

**Gates** (from the evaluation report; **ESTIMATE**): median delivery under 5 s and 95th percentile under 15 s; at least 95% of alerts delivered in the test; no safety incident.

## 7. What is not decided

1. MQTT versus WebSocket and which hosted broker; **ESTIMATE** only.
2. Whether iOS is needed (assume no in the pilot; two-wheeler riders in Hyderabad mainly use Android, **OPINION**, not verified).
3. Whether an operator will let us install the crew app (see the interview plan in the evaluation report).
4. Local vs. hosted OSRM, depending on a laptop or a ₹2,000-5,000 a month server (**ESTIMATE** from the evaluation report).
