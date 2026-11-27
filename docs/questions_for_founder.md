# Questions for the founder, and cheapest first steps

Status: 27 Nov 2026. Ranked by how much the answer would change [business_plan.md](business_plan.md) and [project_plan.md](project_plan.md). Labels: **FACT**, **ESTIMATE**, **OPINION**, **UNVERIFIED**.
Where a question is unanswered, the plans use the stated assumption.

## 1. Ranked questions

| Rank | Question | Assumption used now | What changes if the answer differs |
|---|---|---|---|
| 1 | Do you know anyone at a Hyderabad ambulance operator (owner, dispatcher, crew), RED.Health included? Names and how warm? | No contacts; cold outreach | A warm contact can bring gate G2 (pilot signed) forward by 4-6 weeks; no contacts at all makes the interview target hard |
| 2 | Is your goal mainly **revenue**, mainly **the paper/M.Tech thesis**, or both equally? | Both, with the business first | If the paper comes first, the plan drops the operator software and focuses on RQ1-RQ2; if revenue comes first, the alert study is cut to the benchmark |
| 3 | How many hours a week can you really give, and what are your semester, exam and thesis dates? | 10-12 h, 4-6 h in exam weeks; exams in late Dec and late Apr-May | Every week in the project plan shifts; under 8 h a week means doing either the business or the paper, not both |
| 4 | Will your supervisor back this (paper, ethics application, maybe the thesis topic)? Which ethics committee covers you? | Yes, institute IEC | Without a supervisor, the paper and the human-participant study are at risk; the ethics timeline is unknown |
| 5 | What money can you spend in the next 6 months from your own pocket? | About ₹1.2 lakh, or a grant | Under ₹50,000: no rider incentives, no phone purchases; benchmark on borrowed phones only |
| 6 | Are you willing to incorporate a company (private limited or LLP) in the next 3-6 months? | Yes, around week 12 | SISFS and DPIIT need a company ([myScheme SISFS](https://myscheme.gov.in/schemes/sisfs-fs)); PRAYAS can fund individuals; no company limits the grant path to PRAYAS |
| 7 | Do your institute's rules (scholarship, stipend, IP policy) allow a startup or outside income during the M.Tech? Who owns IP built with institute resources? | Allowed, founder owns IP | An institute IP claim changes the funding and angel story; check before incorporating |
| 8 | Have you or anyone you know ever sold software to a business? | No sales experience | With experience, the 12-month target can be raised; without, add a sales mentor |
| 9 | Are you, or is the institute, already in CIE, i-TIC or ASPIRE? Which is nearest to you in practice? | Not yet | Being on campus at one of them makes it the first application |
| 10 | Which languages do you speak and write well enough to review Telugu, Hindi and Urdu alerts? | English plus one Indian language `[to fill]` | Sets the native-review budget |
| 11 | Do you have Android development experience (Kotlin, foreground services, maps)? | Some | If none, the 8-week build takes about twice as long (ESTIMATE); find an intern early |
| 12 | Would you accept a co-founder (sales/operations or EMS domain)? On what terms? | Solo for 6 months | A co-founder changes the team slide and the speed of the pilot |
| 13 | Is the alert for **two-wheeler riders** a must for you, or are car drivers enough at first? | Cars first (dash-mounted phone), two-wheelers voice and vibration only and later | If two-wheelers must come first, the legal question on phone use (reg. 37(1) proviso, unverified) becomes blocking |
| 14 | Any personal tie to the gig platforms (Rapido, Uber, Ola, Blinkit, Zomato, Swiggy) or to a riders' union? | None | A union or platform contact makes a small consented rider study more feasible |
| 15 | Product name and contact details for the one-pager | `[to fill]` | Cosmetic |

## 2. Questions the founder should take to others (not answerable by the founder)
1. Lawyer: the 10 questions in [privacy_design.md §8](privacy_design.md#8-questions-for-a-lawyer), plus: is a basic patent or prior-art search needed before selling (freedom to operate)? No patent claim is made in any document.
2. CA: GST registration threshold and rate for software sold as a service; whether a student stipend from a grant affects scholarship rules. **UNVERIFIED**.
3. Incubator: which PRAYAS version is open now (PRAYAS 1.0 lists up to ₹10 lakh; DST's newer pages mention up to ₹20 lakh; [DST PRAYAS 2.0](https://nidhi.dst.gov.in/prayas2-0/)); next call dates; whether a solo student is eligible.
4. Operators: the interview script in [project_plan.md §5](project_plan.md#5-operator-interview-script-30-minutes).
5. Still-open research items: [research_gaps.md §7](research_gaps.md#7-still-open-ranked).

## 3. What can be done to achieve this: cheapest first steps

Ordered from cheapest to most expensive. Costs are **ESTIMATES**.

| # | Step | Cost | Time | Why first |
|---|---|---|---|---|
| 1 | Answer questions 1-5 above (reply in this file or a chat) | ₹0 | 1 hour | Each answer changes the plan |
| 2 | Build a 30-name list of Hyderabad private operators and hospital fleets from Google Maps, JustDial and hospital websites | ₹0 | 3-4 hours | Needed for every later step |
| 3 | Ask your supervisor about the ethics committee and whether they will co-author | ₹0 | 1 meeting | The ethics clock is the slowest item |
| 4 | Do 5 operator interviews by phone with the script in [project_plan.md §5](project_plan.md#5-operator-interview-script-30-minutes) | ₹0-500 (calls, tea) | 1-2 weeks | Tests the whole business before any code |
| 5 | Visit CIE (IIIT-H) and i-TIC (IIT-H) PRAYAS pages and email the programme managers: "Is a call open, and is a solo M.Tech student eligible?" ([CIE](https://cie.iiit.ac.in/dst-nidhi/), [i-TIC](https://itic.iith.ac.in/nidhi-prayas.html)) | ₹0 | 1 hour | Funding has long lead times |
| 6 | Make a clickable mock-up (Figma or slides) of the crew app, dispatch map and report to show at the end of interviews | ₹0 | 1 day | Demo without building |
| 7 | Get OSRM running on a Telangana extract on your laptop | ₹0 | 1-2 days | First technical proof; reused by both product and paper |
| 8 | Borrow 5 Android phones of different brands from friends for the latency test | ₹0 | ongoing | Saves about ₹30,000 of phone purchases |
| 9 | Send the lawyer questions through an incubator legal clinic or a law-school clinic | ₹0-5,000 | 2-4 weeks | Liability is the top non-market risk |
| 10 | Incorporate (only after gate G1 passes) | `[to fill quote]` | 2-4 weeks | Needed for SISFS and DPIIT; wasteful if K1 fires |
