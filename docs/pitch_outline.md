# Pitch outline: 10 slides + one-page operator pitch

Status: draft, 27 Nov 2026. Labels: **FACT** (linked), **ESTIMATE**, **OPINION**, **UNVERIFIED**.
Source for every claim: [business_plan.md](business_plan.md). Do not add numbers, customers, quotes or logos that are not in that file. Placeholders such as `[to fill]` stay until real data exists.
**No novelty or patent claims on any slide.** Not legal advice.

## Part A: 10-slide pitch (for an incubator, grant panel or angel)

Audience notes: for a grant panel, stress slides 2, 6, 8 and 10 (public good, research, honest plan). For an angel, stress 4, 5, 7 and 9 (buyer, money, traction). Do not pitch angels until at least one operator pays (**OPINION**).

| # | Title | What goes on it | Label check |
|---|---|---|---|
| 1 | **Title** | Product name `[to fill]`. One line: "No-hardware operations software for private ambulance operators, with a give-way alert built in." Founder name, M.Tech, institute, Hyderabad. | — |
| 2 | **Problem** | (a) Drivers must give way by law: MV Act s.194E, reg. 27(5) "drive to the left" ([links in business_plan §1.1](business_plan.md#11-facts)). (b) Hypothesis: small operators dispatch on phone calls and WhatsApp and cannot prove response times to clients. Mark (b) "what we are testing" until interviews confirm it, then replace with "X of Y operators said…" `[to fill]`. | Law = FACT. Operator pain = hypothesis |
| 3 | **Solution** | Three screens: crew app (one big "Start emergency run" button), dispatch map, monthly response-time report. Fourth, smaller: the alert on a dash-mounted phone, blue left band and arrow, "Ambulance behind: move left if safe". Never "move right". Two-wheeler and gig riders: voice and vibration; a reduced handlebar screen only if the legal check passes. Languages: English, Telugu, Hindi. | Screenshots only once built |
| 4 | **Who pays** | Buyer map table: small and mid private operators first, hospital fleets second; big aggregators as partners; 108 and gig platforms "not now" and why. | OPINION |
| 5 | **Why we pivoted** | One honest slide: the original driver network has no payer, no platform SDK and no moat. The alert becomes a feature and a research pilot; the operator pays for software. Panels tend to trust a founder who shows this (**OPINION**). | FACT/OPINION from [business_plan §1.3](business_plan.md#13-where-the-original-idea-is-weak-honest-verdict) |
| 6 | **Why now** | DPDP Rules phase-in (main duties about May 2027, secondary source); funded private operators in Hyderabad; open routing makes a no-hardware product cheap. | FACT with links |
| 7 | **Business model** | ₹1,000-2,000 per ambulance per month (ESTIMATE, untested); free 90-day pilot; gross margin about 70-85% (ESTIMATE). Three-scenario Y3 revenue: ₹12.6 lakh / ₹49.5 lakh / ₹1.44 crore, labelled "ESTIMATE, assumptions in plan". | Every number labelled ESTIMATE |
| 8 | **Competition** | Table: RED.Health, Medulance, eSahai, Drlogy, Ziqitza, Mappls, GPS vendors; alert prior art (HAAS Alert, Waze). Our difference: no hardware, small-operator price, reports for client conversations, privacy by design. Say plainly: "none of this is a moat; relationships and service are". | FACT links + OPINION |
| 9 | **Traction and plan** | Traction: `[to fill]` (interviews done, pilot signed). If none: say "0 customers; no existing contacts; 10+ cold-outreach interviews planned by 25 Jan 2027". Then the 90-day pilot and gates G1-G4 from [project_plan.md §3](project_plan.md#3-decision-gates-and-kill-criteria). | Never invent traction |
| 10 | **Team and ask** | Founder (M.Tech, CBIT Hyderabad; builds web apps with AI help); gaps (EMS domain adviser, sales, Android, legal); backing: CBIT, if the paper is strong. The ask: CBIT startup cell support first `[to confirm]`, then about ₹10 lakh prototype grant plus incubation (ESTIMATE; fit to scheme limits). Own money: ₹0. Use of funds: hosting, borrowed-phone gaps, study participants, legal and insurance, stipend. Research output: a paper on alert latency and message design. | ESTIMATE |

Backup slides (only if asked): privacy design (on-device matching, no patient data), risk table, financial assumptions, alert message spec, paper plan.

### Questions a panel will likely ask (prepare answers)
1. "Why would an operator pay when GPS trackers are cheap?" → interview evidence `[to fill]`; the report, not the dot on the map, is the product.
2. "Why won't RED.Health just build this?" → it probably can; we target operators it does not serve, and offer it the alert as a research partnership.
3. "Who is liable if a driver crashes after an alert?" → "if safe" wording, fail silent, no "move right", lawyer review pending, insurance `[to fill]`.
4. "Can a student finish an M.Tech and do this?" → 3rd semester with mostly project work; the 10-12 hours a week plan with kill criteria.
5. "Is it legal to use a phone while driving for this?" → open question (legal check L1, due week 7); audio first; screen on fixed car phones, and on two-wheeler handlebars only if L1 passes; lawyer question 7 in [privacy_design.md §8](privacy_design.md#8-questions-for-a-lawyer).
6. "You have no Android experience. How will you build it?" → web crew app first for the business pilot; native driver app later with AI help and a peer review; slip already planned ([mvp_architecture.md §6](mvp_architecture.md#6-build-plan-ai-assisted-no-prior-android-experience)).

---

## Part B: one-page operator pitch (print or WhatsApp PDF)

> **[Product name] — know where every ambulance is, and prove your response times**
>
> **What it does**
> 1. **Crew app** that opens in the browser of any Android phone already in the ambulance (keep it mounted and charging). One button: "Start emergency run". No hardware to fit.
> 2. **Dispatch map** for your control room: every ambulance live, which ones are free, which are on a run.
> 3. **Live ETA link** you can send to the receiving hospital so the emergency team is ready.
> 4. **Monthly response-time report** (call to dispatch, dispatch to scene, scene to hospital) that you can show to hospitals and corporate clients.
> 5. **Optional give-way alert (later):** drivers ahead who have opted in hear "Ambulance behind you. Move left if safe." (English, Telugu, Hindi). It never says "move right". Off unless you switch it on.
>
> **What it never does**
> No patient names, diagnoses or caller numbers are collected. Your data is yours; we process it only for you under a written agreement. Servers in India.
>
> **What it costs**
> - **90-day pilot: free**, for 5-10 ambulances.
> - After the pilot: **₹[1,000-2,000] per ambulance per month** + GST (price to be agreed; this range is our starting estimate).
> - No setup fee, no hardware, cancel any month.
>
> **What the pilot proves (we agree these numbers with you on day 1)**
> | By day | We will show you |
> |---|---|
> | 30 | At least 80% of your emergency runs tracked; dispatcher using the map most days |
> | 60 | Your first response-time report, ready to share with a client |
> | 90 | Whether it saved your team time and helped a client conversation. You decide to pay or stop. No lock-in. |
>
> **What we need from you**
> One contact person, 1 hour to train the crews, an Android phone per ambulance (or tell us and we will discuss), and a 15-minute call each week.
>
> **Who we are**
> `[Founder name]`, M.Tech, `[institute]`, Hyderabad. `[Incubator, if any]`. Contact: `[phone / email]`.

Rules for using the one-pager: fill every `[ ]` before sending; if the alert feature is not ready or approvals are missing, delete item 5 instead of promising it.
