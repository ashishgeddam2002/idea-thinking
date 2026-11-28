# Questions for the founder, and cheapest first steps

Status: updated 28 Nov 2026. The founder answered the first round; answers were passed on by another planning session in the founder's words, lightly tidied. They are treated as facts about the founder, **not verified**.
Labels: **FACT**, **ESTIMATE**, **OPINION**, **UNVERIFIED**, `[to confirm]` (answer was vague).

## 1. Answered (first round)

| # | Question (short) | Founder's answer | Effect on the plans |
|---|---|---|---|
| 1 | Operator contacts? | **None.** No connection to any ambulance driver or operator | All outreach is cold; mentor step added; G2 moved to week 15 ([project_plan.md §3](project_plan.md#3-decision-gates-and-kill-criteria)) |
| 2 | Revenue or paper? | **Both, equally** | Shared-asset table and cut order ([project_plan.md §4](project_plan.md#4-keeping-the-paper-and-the-business-in-step)) |
| 3 | Hours and dates? | "No problem in time"; 3rd semester, mostly project work | 10-12 h/week kept as `[to confirm]`; 2 buffer weeks |
| 4 | Supervisor and ethics? | **CBIT (Hyderabad) backs us if the paper has enough strength** | Supervisor strength check at week 23; ethics body still `[to confirm]` |
| 5 | Own money? | **None**, except the Claude Pro plan; only a grant can pay | ₹0 budget; grant-gated list ([project_plan.md §8](project_plan.md#8-what-cannot-be-done-without-a-grant), [mvp_architecture.md §5](mvp_architecture.md#5-costs-estimates-in-inr-not-quotes-updated-28-nov-2026-own-budget-is-0)) |
| 6 | Incorporate? | **Yes** | After gate G1; fees need a source |
| 8 | Sales experience? | **None** | Sales mentor; interview-first approach |
| 10 | Languages? | **English, Hindi, Telugu** | Pilot in these three; Urdu moved to later ([alert_message_spec.md §3](alert_message_spec.md#3-wording-by-language-draft-native-speaker-review-needed)) |
| 11 | Android experience? | **None**; deployed a website with AI-assisted coding | Web crew app first; native driver app later; 1.5-2× slip assumed ([mvp_architecture.md §6](mvp_architecture.md#6-build-plan-ai-assisted-no-prior-android-experience)) |
| 13 | Two-wheelers? | Wants **screen and audio for both car drivers and gig workers** | Audio first; reduced handlebar screen only if legal check L1 passes ([alert_message_spec.md §4c](alert_message_spec.md#4c-blocking-legal-check-l1-phone-screens-while-riding-or-driving)) |
| 15 | Product name, contacts | None yet | Placeholders stay |

## 2. Still open, re-ranked

Ranked by how much the answer would change the plans now.

| Rank | Question | Assumption used now | What changes if the answer differs |
|---|---|---|---|
| 1 | **What is the name of CBIT's startup or seed cell, and what does it offer?** (grants, amounts, mentors, legal help, incubation, phones, lab space). Was Q9 | Exists; offer unknown `[to confirm]` | It is funding step 1. A CBIT grant could pay for phones, participant fees and hosting and unlock grant-gated steps months earlier; nothing from it means waiting for PRAYAS |
| 2 | **Which ethics committee covers you at CBIT, and when does it meet?** Was part of Q4 | Institute committee; approval weeks 12-16 | Sets when RQ2 and any alert test can start; a long wait pushes the paper into June-July 2027 |
| 3 | **Your cousin "works but temporary": for a gig platform (which one?) or an ambulance operator?** Was Q14 | No usable tie | If at an ambulance operator: a first interview and maybe a warm route to a pilot (G2 earlier). If at a gig platform: a source for rider interviews, not a partnership |
| 4 | **Who owns IP you build during the M.Tech?** Get CBIT's answer in writing. Was Q7 detail | Founder owns it ("no issue") | An institute claim changes incorporation, PRAYAS and any angel conversation |
| 5 | **Would you accept a co-founder** (sales/operations, EMS domain, or Android)? On what terms? Was Q12 | Solo | A co-founder with sales or Android skills removes the two largest team risks |
| 6 | Exact weekly hours and exam or thesis-submission dates | 10-12 h/week; buffer weeks 5 and 22 | Under 8 h/week means choosing between the business and the paper |
| 7 | Is the M.Tech thesis topic this project, or separate? | Separate but overlapping | If it is the thesis, the paper track gets more hours and the supervisor's stake rises |
| 8 | Can you borrow 5 Android phones of different brands (who, which brands)? | Yes, from friends or a CBIT lab | If not, RQ1 waits for a grant |

## 3. Questions for others (not answerable by the founder)
1. Lawyer (via CBIT cell or a free law clinic): the 10 questions in [privacy_design.md §8](privacy_design.md#8-questions-for-a-lawyer), with **question 7 first** (it is legal check L1); plus whether a basic prior-art or patent search is needed before selling. No patent claim is made in any document.
2. CA: GST registration threshold and rate for software sold as a service; incorporation cost. **UNVERIFIED**.
3. CBIT cell and incubators: which PRAYAS version is open now (PRAYAS 1.0 lists up to ₹10 lakh; DST's newer pages mention up to ₹20 lakh: [DST PRAYAS 2.0](https://nidhi.dst.gov.in/prayas2-0/)); next call dates; whether a solo student can apply.
4. Operators: the interview script in [project_plan.md §6](project_plan.md#6-operator-interview-script-30-minutes).
5. Still-open research items: [research_gaps.md §7](research_gaps.md#7-still-open-ranked).

## 4. What can be done to achieve this: cheapest first steps
All steps below cost **₹0** unless marked **[G]** (needs a grant).

| # | Step | Time | Why first |
|---|---|---|---|
| 1 | Visit CBIT's startup cell: ask its name, grants, mentors, legal help, ethics contacts; ask in writing about IP | 1-2 hours | Funding step 1; answers open questions 1, 2 and 4 |
| 2 | Ask your cousin what they do and whether they know any ambulance driver or owner | 10 minutes | Could be the only warm lead |
| 3 | Build a 30-name list of Hyderabad private operators and hospital fleets (Google Maps, JustDial, hospital websites) | 3-4 hours | Needed for all outreach |
| 4 | Ask the CBIT cell and alumni office for a sales or healthcare mentor | 1 email | You have no sales experience; a mentor shortens G2 |
| 5 | Start 20 cold contacts and aim for 5 interviews with the script in [project_plan.md §6](project_plan.md#6-operator-interview-script-30-minutes) | 2 weeks | Tests the business before code |
| 6 | Legal check L1: find the 2020 gazette notification on phone use (reg. 37(1) proviso) from a CBIT or home network | 2-3 hours | Blocks the two-wheeler screen you want |
| 7 | Make a clickable mock-up of the crew app, dispatch map and report (Figma free tier or slides) | 1 day | Demo without building |
| 8 | Set up OSRM on a Telangana extract on your laptop with AI help | 1-2 days | First technical proof for both product and paper |
| 9 | Line up 5 borrowed Android phones of different brands | ongoing | Replaces about ₹30,000 of purchases |
| 10 | Incorporate, after gate G1 passes **[G or CBIT help]** | 2-4 weeks | Needed for SISFS and DPIIT |
