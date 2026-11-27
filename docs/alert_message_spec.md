# Alert message spec: what the driver sees and hears

Status: design draft. Nothing here is tested. Not legal advice.
Labels used below: **FACT** (with link), **ESTIMATE**, **OPINION**, **DRAFT** (needs native-speaker or test validation).

Earlier research (not copied here): [evaluation report](https://github.com/ashishgeddam2002/BLATTA/blob/claude/ambulance-alert-india-analysis-b8uz09/reports/India%20ambulance%20alert%20evaluation.md), [research notes](https://github.com/ashishgeddam2002/BLATTA/tree/claude/ambulance-alert-india-analysis-b8uz09/research_notes/India%20ambulance%20alert%20evaluation).

## 1. The law the alert must follow

| Source | Text (verified from a mirror; official gazette not reachable) | Design consequence |
|---|---|---|
| MV Act s.194E ([text mirror](https://indiankanoon.org/doc/132499746/)) | "Whoever while driving a motor vehicle fails to draw to the side of the road, on the approach of a fire service vehicle or of an ambulance or other emergency vehicle as may be specified by the State Government, shall be punishable with imprisonment ... up to six months, or with a fine of ten thousand rupees or with both." | The Act says "draw to the side", not "left". |
| Driving Regulations 2017, reg. 27(5)(a)-(b) ([27(5)](https://indiankanoon.org/doc/21177923/)) | When an emergency vehicle "with its multi-toned horn and light flasher on, is overtaking, approaching or entering the path of any other vehicle", the driver or rider shall, unless a police officer directs otherwise, "(a) yield the right of way ... by driving to the left as close as practicable to the kerb or edge of the roadway in the shortest possible time; (b) stop, if required, and remain stationary in that position until the emergency vehicle has passed." | Default = left. Add "stop if needed". Police direction overrides the app. |
| Reg. 27(6) ([reg. 27](https://indiankanoon.org/doc/15262949/)) | Driver "shall, unless otherwise directed by the crew of the emergency vehicle, maintain a distance of at least fifty meters" from an emergency vehicle with siren or flasher on. | Do not tell followers to close in. Alert says nothing about following distance. |
| Reg. 27(3)(iv) (same page) | An emergency vehicle with siren and flasher on may, "with utmost care", drive "in either direction on a 'NO ENTRY' or a 'One Way' street". | A one-way street can have an ambulance coming head-on. See the contra-flow rule in section 2. |
| Reg. 27(1)-(2) (same page) | Siren and flasher only when responding to an emergency call; with them on, the vehicle has right of way. | Alert only while the crew app says "emergency run" AND siren/flasher is on. |

I found no official exception that allows "move right". The only departures from "left" in the text are a police officer's direction and the stop-if-required clause.
**Not verified:** the 2020 proviso to reg. 37(1) (G.S.R. 586(E)) that allows a phone "solely for route navigation". The mirror shows reg. 37(1) as only "The driver shall not use any hand held mobile phone or other communication device" ([full regulations, mirror](https://indiankanoon.org/doc/164893636/)). See [research_gaps.md](research_gaps.md). **OPINION:** treat the alert as voice-only and never need a touch, whatever the proviso says.

## 2. Direction logic (decision table)

The phone decides locally. Inputs: distance and time-to-arrival (TTA) of the ambulance behind, own lane position (best effort), speed, road type.

| # | Situation (checked in order) | Voice (English) | Banner (max 5 words) | Arrow |
|---|---|---|---|---|
| 0 | Ambulance not on an emergency run, or siren/flasher off | no alert | none | none |
| 1 | Driver is not ahead of the ambulance on its predicted path, or not moving the same way | no alert (see "Other road" below) | none | none |
| 2 | TTA > 60 s | no alert yet | none | none |
| 3 | TTA 30-60 s, left side is free (default) | "Ambulance behind you, 200 metres. Move left if safe." | "AMBULANCE. MOVE LEFT" | left |
| 4 | Left impossible: leftmost lane already, kerb or parked cars, bus stop, median on left (best effort from map), or speed under 5 km/h for 10 s (gridlock) | "Ambulance behind you. Stay where you are." | "AMBULANCE. STAY PUT" | stop icon |
| 5 | Ambulance closer than 100 m, driver still in its lane and moving | "Ambulance close behind. Move left and stop." | "MOVE LEFT. STOP" | left |
| 6 | Ambulance has passed or alert cancelled | "Ambulance has passed." (short chime, no speech if under 5 s since the last alert) | "PASSED" | none |
| 7 | Contra-flow (ambulance approaching head-on on a one-way street) | **No alert in the pilot** | none | none |

Rules:
1. Never say "move right". Case 4 says "stay" because standing still is the lawful fallback under 27(5)(b).
2. Say "if safe". **OPINION:** this reduces the platform's and the founder's liability and does not weaken the message. It is the wording the Budaun precedent argues for ([report notes](https://github.com/ashishgeddam2002/BLATTA/tree/claude/ambulance-alert-india-analysis-b8uz09/research_notes/India%20ambulance%20alert%20evaluation)).
3. Case 7 is excluded because reg. 27(3)(iv) lets an ambulance run against a one-way flow, which the "ahead and same direction" rule cannot cover. Revisit after the pilot.
4. Lane position is **DRAFT**: urban phone GPS cannot reliably give a lane. If the phone cannot tell, use case 3 and rely on "if safe".

### Who is alerted: geometry
1. The ambulance's predicted route is cut into road segments (OSM way IDs). The corridor is the next 300-800 m of segments plus a time window.
2. A phone alerts only if (a) it is snapped to a segment in the corridor, (b) its heading is within 45 degrees of the segment direction, and (c) it is ahead of the ambulance with TTA 30-60 s.
3. **Flyovers and underpasses:** segments carry a layer tag (OSM `layer`, `bridge`, `tunnel`). A phone on layer 1 is not alerted for a corridor on layer 0, and the reverse. If the layer is unknown, do not alert.
4. **Service roads and divided carriageways:** use separate OSM ways for each carriageway and service road. A phone on the other carriageway, or on a parallel service road, gets case 1 (no alert). Wording "Ambulance on the next road, no action" is shown only for a phone within 50 m of the corridor but on a different way, and only in the pilot to measure confusion. **OPINION:** the default release shows nothing here, to cut alert fatigue.
5. Prefer silence when unsure. A missed alert costs one "I didn't notice" case; a false alert costs trust.

## 3. Wording by language (DRAFT, native-speaker review needed)

Translations were drafted by the model and are **not** checked by native speakers. Test with 5 speakers per language before any use. Distances are rounded to the nearest 50 m.

| Case | English | Telugu | Hindi | Urdu |
|---|---|---|---|---|
| 3 | Ambulance behind you, 200 metres. Move left if safe. | అంబులెన్స్ మీ వెనుక, 200 మీటర్లు. వీలైతే ఎడమవైపుకు వెళ్లండి. | एम्बुलेंस आपके पीछे, 200 मीटर। सुरक्षित हो तो बाईं ओर हो जाइए। | ایمبولینس آپ کے پیچھے، دو سو میٹر۔ محفوظ ہو تو بائیں طرف ہو جائیں۔ |
| 4 | Ambulance behind you. Stay where you are. | అంబులెన్స్ మీ వెనుక ఉంది. ఉన్న చోటే ఉండండి. | एम्बुलेंस पीछे है। अपनी जगह रुके रहिए। | ایمبولینس پیچھے ہے۔ اپنی جگہ رکے رہیں۔ |
| 5 | Ambulance close behind. Move left and stop. | అంబులెన్స్ దగ్గరగా ఉంది. ఎడమకు వెళ్లి ఆగండి. | एम्बुलेंस बहुत पास है। बाईं ओर होकर रुकिए। | ایمبولینس بہت قریب ہے۔ بائیں طرف ہو کر رک جائیں۔ |
| 6 | Ambulance has passed. | అంబులెన్స్ వెళ్లిపోయింది. | एम्बुलेंस निकल गई। | ایمبولینس گزر گئی۔ |

Banner strings (max 5 words, large type, one language at a time, chosen in app settings; default from phone language):

| Case | English | Telugu | Hindi | Urdu |
|---|---|---|---|---|
| 3 | AMBULANCE. MOVE LEFT | అంబులెన్స్. ఎడమకు | एम्बुलेंस। बाएँ | ایمبولینس۔ بائیں |
| 4 | AMBULANCE. STAY PUT | అంబులెన్స్. ఆగండి | एम्बुलेंस। रुकिए | ایمبولینس۔ رکیں |
| 5 | MOVE LEFT. STOP | ఎడమకు. ఆగండి | बाएँ। रुकिए | بائیں۔ رکیں |
| 6 | PASSED | వెళ్లింది | निकल गई | گزر گئی |

Voice rules: one sentence of at most 8 words when TTA is under 30 s; no jargon; speak the direction last or first consistently (**OPINION:** "left" last, because the final word is remembered best, to be tested); Urdu text is right-to-left, so check the banner layout. Voice must be pre-recorded or pre-synthesised on the device (no network call at alert time).

## 4. Channels

| Channel | Spec | Why |
|---|---|---|
| Voice | First channel. Lower ("duck") other audio, including navigation, by 70% for the sentence, then restore. Audio focus: `AUDIOFOCUS_GAIN_TRANSIENT_MAY_DUCK`. Prefer the call/navigation audio stream so it plays through Bluetooth helmets and earphones. | Eyes stay on the road. |
| Banner | Cars only. Full screen, shown over the lock screen if the OS allows (see 4b for limits). Black on bright yellow, or white on dark blue (both pass colour-blind checks below). Arrow at least 40% of screen height. Max 5 words. No buttons: nothing to tap. Auto-dismiss on "passed" or after 15 s. | Glance under 2 s. |
| Vibration | Pattern distinct from calls and messages: three short pulses then one long (100-100-100-100-100-100-500 ms), amplitude high. Different pattern for "passed" (one short). | Deaf or noisy-road drivers. |
| Two-wheelers | Audio only, through earphones or a Bluetooth helmet. Screen stays off or dim. No banner needed. If no earphones are connected, do not use the loudspeaker as the only channel: **OPINION:** road noise makes it unreliable; use vibration (phone in pocket) as backup and record the case in the pilot. | The rider cannot read a screen. |
| Car, hands-free | Voice plus banner on a dash-mounted phone. | Same reg. 37 caution. |

### 4b. Map-style visual alert (added after founder feedback)

Idea: on a dash-mounted phone or a car screen, show a map-like screen with the safe side marked, instead of text only. Auto-open it when an alert starts.

| Part of the idea | Spec | Reason |
|---|---|---|
| Map view with the user's own road | Simple top-down road, the driver's car in the centre, the ambulance marked behind with its distance, the **left edge of the road shaded** as the "go here" side. Drawn by our own app from the local OSM tiles, not by opening Google Maps. | Google Maps has no public hook for an outside app to draw on it or take it over. Our own screen works the same on any map the driver uses. |
| Side colouring | Case 3 (move left): left half of the screen and left road edge in a bright **blue** band with a big left arrow. Case 4 (stay put): whole screen **amber** with a stop icon. Case 5 (move left and stop): left blue band plus a stop icon. **Red is not used for the whole screen.** | **OPINION:** a fully red screen reads as "danger, brake hard" and can cause a panic stop or a swerve. About 1 in 12 men are red-green colour blind (common figure, not checked in this session), so side must be shown by position and an arrow, not by colour alone. |
| "Stay on the right" | **Not offered.** If the driver is already in the leftmost lane, the screen says "stay put", not "stay right". | Reg. 27(5)(a) says left. The only exception found is a police officer's direction. If a police officer directs otherwise, the officer wins, and the app cannot know that. |
| Auto-open on cars | If the phone is on a dash mount and the app has permission, show the alert as a full-screen overlay. On Android Auto or CarPlay, the alert would have to come from a navigation or similar approved app category. | See "Platform limits" below. |
| Two-wheelers | **No map and no screen.** Voice and vibration only. | The rider cannot look at a screen. |

Rules for the screen:
1. At most 5 words, the arrow, and the distance. No buttons, no zoom, nothing to touch.
2. A glance of about 2 s must be enough (see section 7). The map is a **confirmation**, not something to read. If a simple arrow and band test as faster in the lab than the map, drop the map.
3. It appears only while the voice alert is active, and closes on "passed" or after 15 s.
4. In daylight it must stay readable: bright band, black text (see accessibility).
5. Must never cover a navigation turn warning for more than the alert's duration.

**Platform limits (OPINION, from general Android and iOS knowledge; not verified in this session):**
1. Android restricts apps from opening themselves from the background (since Android 10), and full-screen alerts are meant for calls and alarms (tightened in Android 14). A draw-over-other-apps overlay needs a special permission the user grants once, and some phone brands add further limits. So "auto-open" cannot be assumed to work on every phone. It must be tested on the 5 brands (see the paper plan).
2. iOS does not let a third-party app take over the screen in the background. An iPhone could only get a notification and voice. The pilot is Android only.
3. Android Auto and CarPlay allow only certain app categories, and they limit what these apps can draw. A map alert there would need a navigation-category build, so leave it for later.
4. Opening the Google Maps app itself is a different matter. **I found no way for a third-party app to force Google Maps to show a coloured side**, so do not promise it. The partner route in [mvp_architecture.md](mvp_architecture.md) lets Google, Mappls or Ola draw this on their own maps if they want to.
5. Rules for phones in cars: reg. 37 says the driver shall not use a hand-held phone. A phone fixed on the dashboard is a grey area ([research_gaps.md](research_gaps.md)). An alert that needs no touch is safer on this point.

**New test in the usability plan (section 8):** compare (a) voice only, (b) voice plus arrow banner, (c) voice plus map with left band, (d) full-red screen. Measure correct action, time to action, and glance time (video or eye tracker if available). If (d) is slower or causes wrong or panicked moves, drop it.

## 5. Accessibility

1. Colour-blind safe: do not rely on red/green. Use yellow-black and blue-white with an arrow shape. Check with a simulator (for example Coblis or the Android Accessibility Scanner).
2. Icon meaning without text: a big left arrow means "move left"; an octagon means "stay put"; a tick means "passed".
3. Deaf or hard of hearing: vibration plus banner; setting "visual and haptic only".
4. Low literacy: voice is the primary channel.
5. Text contrast target: at least 7:1. **ESTIMATE** (a common accessibility target; ISO 15008 requirements are for passenger-car displays and not read in full, see sources).

## 6. Alert fatigue controls

1. Alert only when the crew app has set "emergency run" AND siren/flasher on (matches reg. 27(1) and 27(5)).
2. One alert per driver per ambulance, plus one "passed". No repeats, except case 5 once if the ambulance closes under 100 m.
3. Rate limit: at most 3 alerts per driver per 10 minutes (**ESTIMATE**, tune in the pilot).
4. Cancel: if the crew ends the run, or the ambulance leaves the corridor, send "cancel" and play nothing (or "passed" only if an alert was already spoken).
5. Staleness: if the phone has not received a corridor update for 10 s, drop the alert silently.
6. Riders on two-wheelers get voice and vibration only, never a banner.
7. User can mute for 1 hour. The app never ranks or scores the driver (see [privacy_design.md](privacy_design.md)).

## 7. Human-factors evidence

Evidence level: summaries come from search results and abstracts. I could open some but not all full texts. "Seen" means I saw the page or abstract; "Not opened" means I did not read the primary document.

| Choice | Evidence | Status |
|---|---|---|
| Glance under 2 s, total under 12 s | NHTSA Phase 1 visual-manual guidelines set 2 s for a single average glance and 12 s total eyes-off-road for a task; voluntary and written for built-in devices. [Federal Register 78 FR 24817](https://www.govinfo.gov/link/fr/78/24861), [Justia copy](https://regulations.justia.com/regulations/fedreg/2013/04/26/2013-09883.html). Phase 2 covers portable and aftermarket devices: [SWOV record](https://swov.nl/en/publicatie/visual-manual-nhtsa-driver-distraction-guidelines-portable-and-aftermarket-devices). | Seen (search results). The NHTSA PDF host returned 403 to my fetch. |
| ISO 15008 display legibility | ISO 15008:2017 sets image quality and legibility minima for dynamic visual displays for passenger-car drivers; it excludes coding, format and dialogue, and heavy vehicles are excluded from contrast and font size. [ISO 15008](https://www.iso.org/standard/62784.html). | Seen (ISO page, summary only). Standard text is paid and not read. |
| ISO 15005 dialogue management | I found no ISO page in my search. [ISO catalogue](https://www.iso.org/standard/50805.html) came up for ISO 15008-related results and I did not confirm it is ISO 15005. | **Unverified.** Do not cite until checked. |
| In-vehicle warning makes drivers yield earlier and further away | Sweden, driving simulator, 90 drivers, FM-radio "Emergency Vehicle Approaching" messages: [Frontiers in Sustainable Cities 2020](https://www.frontiersin.org/articles/10.3389/frsc.2020.00019). A US DOT summary reports yielding distance 2.64 times further with EVA messages: [ITS JPO record](https://www.itskrs.its.dot.gov/2025-b01963). Gothenburg thesis: warning lowered speed and yielding time in a repeat event; a brochure alone changed nothing: [GUPEA](https://gupea.ub.gu.se/handle/2077/77614). | Seen (abstracts). Simulator, not field. |
| Warning range matters | Australian simulator study of an in-vehicle advance warning at a 300-400 m radius with visual and auditory cues: [SWOV record](https://swov.nl/en/publicatie/detection-emergency-vehicles-driver-responses-advance-warning-driving-simulator). | Seen (abstract). |
| US connected-vehicle alerts help drivers yield | FHWA simulator study: [FHWA media 49166](https://highways.dot.gov/media/49166). | Seen (search result only). |
| Speech or multimodal over tones for riders | US DOT connected-motorcycle warning study (2016) found combined modes preferred and suggested simple speech for direction: [ROSA P](https://rosap.ntl.bts.gov/view/dot/30671/dot_30671_DS1.pdf). A 2026 helmet HMI simulator study (N=13) found no significant reaction-time effect: [preprint](https://bazilinskyy.github.io/publications/vanheuvelen2026second). TU Dresden auditory alert work: [portal](https://fis.tu-dresden.de/portal/en/publications/enhanced-motorcycle-safety-through-the-development-and-evaluation-of-auditory-alert-system(be22cd90-c1c8-4754-a5c0-eeb3a5c24441).html). | Seen (abstracts). **No study I found shows a robust benefit of audio-only warnings for riders.** Treat audio-only as a design choice to test, not as proven. |
| Waze today | Waze alerts users to emergency vehicles on route, but only for reported vehicles, and not on Android Auto or CarPlay: [Waze Help](https://support.google.com/waze/answer/14716475?hl=en). | Read directly. |

What the evidence does not show: any field result that alerts shorten ambulance trips, any test in Indian mixed traffic, or any test of left-lane geometry in India. Those are the research gaps in [paper_plan.md](paper_plan.md).

## 8. Usability test plan (20 participants)

Participants: 10 two-wheeler riders (including 5 delivery or ride-hail riders) and 10 car, auto or cab drivers; mixed Telugu, Hindi, Urdu and English speakers. **Needs ethics-committee approval before recruitment** (see paper plan). Pay a small fixed amount (**ESTIMATE** ₹300 each).

1. **Lab mock-up (week 1-2, seated, no vehicle).**
   1. Play each case with a recorded siren and a simulated road video. Measure time from alert start to the participant stating the action ("left", "stay", "nothing").
   2. Pass: at least 90% correct, median under 2 s, in each language.
   3. Check comprehension of banner icons with sound off, and colour-blind and deaf modes.
2. **Driving simulator or video-based task (week 3).** If no simulator, use a screen-based hazard-perception task. Compare voice only, voice plus banner, banner only, voice plus map with side band (4b), and a full-red screen as a negative control.
3. **Roadside test with no real ambulance (week 4-6).**
   1. Closed or low-traffic road with permission from the institute and local police. A decoy vehicle with no siren or flasher, and no claim to be an ambulance.
   2. The alert is triggered by a scripted vehicle on a test route, using a **test voice prefix** ("Test.") so riders never treat it as real.
   3. Observer notes lane position, speed change, and any near-miss. Stop the test on any near-miss.
   4. Gate: no near-miss; at least 50% of riders shift left or slow within 10 s.
4. **Do not** run any test with a real ambulance until the operator and police approve in writing.

Open: whether to test audio only for riders against a vibration backup. Record both.
