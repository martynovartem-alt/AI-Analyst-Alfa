# CLAUDE.md

This file provides product and team context for AI-assisted hypothesis discovery work. It is not a code project — it is a product strategy document. Read it to understand who the user is, what they've already validated, and what they're trying to figure out next.

---

## Product context

**Product:** AI Augmentation Platform for bank IT teams
**What it does:** Identifies high-friction roles inside banks and ships AI tools that reduce manual time waste in those roles — without replacing people, augmenting their output.
**Stage:** Post-MVP on two shipped products; entering next hypothesis discovery cycle.
**Domain:** Russian/CIS bank IT departments — analytics, chatbot/IVR, product management, and design teams.

### Who I am

Product builder doing AI transformation inside banks. I find roles with measurable time waste, validate the pain, and ship lightweight AI tools (chatbots, agents, multiagent pipelines). Current focus: discovering the next role to augment after two proven cases.

**My technical profile:** Low-code / prompt engineering. I design solutions, write prompts, and configure tools — I don't write production code. Developers handle implementation.
**Tenure:** Less than a year embedded — still building trust. Interview access to new teams is not free; requires relationship effort or a warm intro.

### Target customer

**Role:** Team leads and heads of IT sub-departments inside the bank (support ops, analytics, chatbot/IVR teams).
**Context:** Teams of 5–30 people, sprint-based delivery, clear velocity metrics. Decision to try a tool is made at team lead level; budget approval goes to department head.
**Pain pattern:** Repetitive, rule-based, or lookup-heavy subtasks that consume 15–30% of sprint capacity — tasks the role considers "not real work" but has no time to automate.

### Engagement model

- **Internal team** — embedded inside one bank, not an external vendor
- **Funding:** Internal IT budget / cost center — no sales cycle, no external pricing
- **Access:** <1 year tenure — access to new teams requires trust-building; not all interview slots are easy to get
- **Team:** Product owner (me, prompt/low-code) + 1–2 developers (dedicated full-time)
- **AI stack:** Dual — external APIs (OpenAI / Anthropic) for prototyping; self-hosted open-source LLM (LLaMA / Mistral family) for production. Quality gap is real and significant. Always validate the hypothesis on the internal model before committing — structured tasks (RegExp, SQL) degrade less than reasoning-heavy or long-context tasks.

### How hypotheses are discovered

1. Market research — track how AI tools are changing specific role workflows externally (e.g. new tooling releases, role-specific AI adoption)
2. Interviews — go to the team, map their workflow, find where time is actually spent

### Hard constraints

- **No sensitive personal data** — don't build on PII, transaction data, or credit history
- **Augment, don't replace** — tools must make existing people more productive; headcount-reduction framing is off the table (see DL-2 for why this also fails technically)

---

## Shipped products (already validated, not hypotheses)

### DL-0 — RegExp Auto-Generator for chatbot scenario writers
- **Who:** Scenario writers building NLU training data for bank chatbots/IVR
- **Pain:** Writing RegExp patterns for intent matching consumed ~30% of sprint time
- **Solution:** LLM-assisted RegExp generation from natural language intent description
- **Result:** 30% sprint time recovered for scenario writers
- **Status:** Shipped ✓

### DL-1 — Text→SQL multiagent system for data analysts
- **Who:** Bank data analysts running ad-hoc queries for business stakeholders
- **Pain:** Ad-hoc SQL requests consumed ~20% of sprint time; analysts are bottleneck for business
- **Solution:** Plan-Execute multiagent pipeline — LLM writes SQL from natural language, validates, executes
- **Result:** Analytics team capacity expanded by ~20% per sprint
- **Status:** Shipped ✓

---

## Current objective

**Hypothesis discovery phase.** Find the next bank IT role where:
- There is a repetitive, measurable subtask consuming ≥15% of sprint time
- The subtask is rule-based or lookup-heavy (good AI fit)
- The team lead has pain awareness and can approve a pilot

**Validation timeline:** 2–4 weeks per hypothesis — 1–2 synthetic CustDev sessions first, then 3–5 real interviews to confirm or kill.

**Candidate roles — ranked by evidence × access (market scan done June 2026):**

| Role | Access | External evidence | Key metric | Rank |
|---|---|---|---|---|
| Data analysts (same team as DL-1) | **Have access** | DL-1 already shipped here | DL-5 in progress (dashboard/vitrina generation, now 2 respondents); DL-7…DL-19 opened across 3 respondents (Вахрушева, Миниахматова, Плеханова) — 5 killed, 5 yellow/pivot, 2 mixed/team-specific — see Decision Log | **#1** |
| Chatbot scenario writers | **Have access** | None external — DL-2b internal signal | 20% sprint waste on script fixes confirmed; utterance writing ~5-10% sprint additional | **#2** |
| Product designers | **Have access (via developer contact, since 14.07.2026)** | 2 of 10 initial hypotheses already confirmed & in development (H-PD-3/5, H-PD-4) — see `Hypotheses_ProductDesigners_28_26.md` | Shared blocker (role existence/reachability) resolved; still zero live interview with the designer themselves — only synthetic CustDev + a developer's status report | **#3** |
| Product managers | Access unknown — market-scanned (3 rounds), but no live contact secured yet | None gathered yet — synthetic CustDev only | TBD — needs a warm intro before any live signal exists | **#4** |

> **Note:** "Chatbot scriptwriters" and "scenario writers" are the same role — one person writes both JS scripts and NLU training data (intents, utterances, RegExp). DL-3 and DL-4 both target this role.

> **Note (updated 14.07.2026):** Product designer access is resolved — reached through a developer (Николай Шубич) who is already building AI tools for that role; two hypotheses are already validated this way. Product manager access is still unresolved despite three rounds of market-sourced hypothesis generation — market research alone doesn't substitute for a live contact.

*Ranking logic: access is the binding constraint at <1 year tenure. Data analysts and scriptwriters have existing relationships and can be interviewed now. Product designers moved above product managers (14.07.2026) — designer access resolved and two hypotheses already confirmed via a developer contact, while product manager access remains at zero live contact despite equal or greater market-research effort.*

**Note on Scrum Masters:** Removed — they don't exist as a distinct role in this bank. Team leads double as SMs. The sprint reporting pain (30–120 min/sprint) is real but falls on team leads, not a separate role. Could surface as a secondary pain during team lead interviews.

**Note on security approval (ИБ) as a cross-role blocker — partially contradicted (14.07.2026, see Developer Status Report in `Hypotheses_ProductDesigners_28_26.md`: at least two designer-facing tools already passed this stage):** Surfaced independently in two synthetic CustDev sessions for two different roles — designer persona Ирина ("даже обычного Figma AI нет — IT не одобрил") and PM persona Сергей ("если нужен доступ к системам — тогда уже с ИБ"). Not yet confirmed in a live interview, but the pattern repeating across unrelated synthetic personas is worth tracking: any future AI tool requiring system/data access may face a security review gate independent of team-lead buy-in. Ask about typical ИБ approval turnaround time in the next live interview for any role, not just designers/PM. **Update:** the Developer Status Report shows two designer-facing tools (H-PD-3/5, H-PD-4) already past this stage - either the gate isn't uniformly slow, or Irina's synthetic persona described a different part of the org than the developer's contact works with. Ask directly in the next live designer interview (see `Interview_ProductDesigners_28_26_H2_PD.md`) rather than assuming either signal is right.

**Market scan findings (June 2026):**
- Data analysts (DL-1 team): "Business analyst" in this bank = analytics role (SQL, dashboards, Excel) — NOT a requirements-writing BA. Same team as DL-1. SQL pain is already solved. Remaining pain is dashboard creation, Excel report generation, analysis commentary writing. This is an extension hypothesis, not a fresh role.
- Chatbot scriptwriter augmentation has zero published case studies externally. Either untapped or not yet done publicly.
- Roles out of scope: Data engineers (context-heavy, same failure mode as DL-2), Security/Antifraud (different department).
- Killed after synthetic CustDev: Intent coverage gap detection (needs conversation logs → PII constraint, hard blocker).
- Product managers, product designers (added July 2026): no market scan run yet — needs a dedicated pass before these can be prioritized against data analysts / scriptwriters.

**→ Next actions:**
- **Done:** Market signal scan (June 2026)
- **Done:** DL-5 opened for data analysts (July 10, 2026) — dashboard/vitrina generation from requirements
- **Next:** 3–5 live interviews with DL-1 team (scoped: "draft survives changing requirements", not "generate after finalization") + technical PoC on self-hosted LLM. See DL-5 for full criteria.
- **Next:** Continue scriptwriter tracks (DL-3, DL-4) in parallel
- **Blocked on access:** Product managers, designers — need trust-building/warm intro before a hypothesis cycle can start; no market scan run yet for either

**Out of scope:** DevOps/SRE/infrastructure roles; Security/Antifraud — separate department, no access.

See `## Decision Log` below for DL-2 (killed) and DL-2b (parked residual signal).

---

## Workflow (the core loop)

**One-time setup** *(already done for this product):*
- Fill in `CLAUDE_template.md` for a specific product → save as `CLAUDE.md`

**Per hypothesis cycle:**
0. **Generate candidates** using `skill-hypothesis-generating.md` — pull signals from market, CustDev, and product data → get a ranked list of 5–10 candidate hypotheses
1. Run the top candidate through `skill-hypothesis-check.md` → get a structured hypothesis + ICE score
2. Run a synthetic CustDev session using `skill-synthetic-custdev.md` → surface objections before real interviews
3. **Targeted market scan** using `skill-market-scan.md` → deep report on the specific hypothesis: TAM, players, trends, gaps — all with sources (different from step 0 — this is narrow, not broad)
4. Record the outcome in `skill-decision-log.md` → one `DL-N` entry per hypothesis cycle
5. Paste the DL-N entry into the `## Decision Log` section of `CLAUDE.md` → so the next session inherits context

One full cycle is ~3 hours. The loop is closed when the DL entry lives in `CLAUDE.md`.

## Files and their roles

| File | Role |
|---|---|
| `CLAUDE_template.md` | Product context template — fill this in per product and rename to `CLAUDE.md` |
| `skill-hypothesis-generating.md` | Generates hypothesis candidates from 3 sources (market, CustDev, product data) → prioritized list ready for hypothesis-check |
| `Hypotheses_WW_YY.md` | Cross-role hypothesis runs — one file per run (e.g. `Hypotheses_23_26.md`, `Hypotheses_23_26_2.md`). Latest: `Hypotheses_23_26_2.md` |
| `Hypotheses_AllRoles_23_26.md` | **Canonical** combined & skill-corrected hypotheses for data analysts and scenario writers (20 total), in Russian. Replaced the per-role files (`Hypotheses_DataAnalysts/ScenarioWriters_23_26.md`), now deleted. |
| `skill-hypothesis-check.md` | Structures a raw idea into a testable hypothesis + ICE (1–10) + go/pivot/stop criteria |
| `skill-synthetic-custdev.md` | Turns Claude into a specific ICP persona for a practice interview session |
| `skill-market-scan.md` | Produces a structured market report: TAM, players, trends, gaps — all with sources |
| `skill-decision-log.md` | Template for recording what was tested, what was learned, and what the next step is |

## Using the skill files

Each `skill-*.md` contains a ready-made prompt block (marked with ` ``` `). Copy the prompt, fill in the `{placeholders}`, and paste into Claude. No installation required.

`skill-synthetic-custdev.md` works best when you give the persona 3–5 concrete personal details and an explicit pain. If the persona agrees with everything, the role is underspecified — add more friction.

`skill-market-scan.md` requires a tool with web search (Perplexity, Claude with web search, EXA, or Tavily). Without live search, AI will hallucinate market figures.

## Decision Log convention

Entries follow the format `DL-{N}`. Each entry must include a citation (quote or data point) — entries without evidence are not valid. **Exception:** parked hypotheses (not yet tested) may appear without evidence but must be labeled as untested. After each cycle, paste the new `DL-N` entry into the `## Decision Log` section below so future sessions see what was already tested.

---

## Decision Log

### DL-0 — RegExp Auto-Generator for chatbot scenario writers (Shipped)
**Hypothesis:** Scenario writers will recover ≥15% sprint capacity if given LLM-assisted RegExp generation from natural language intent descriptions.
**Test method:** Production deployment + sprint velocity measurement with full scenario-writing team.
**Evidence:** "30% sprint time recovered for scenario writers" — team lead estimate post-ship, not formally tracked. Directionally reliable, not independently verified.
**Decision:** Green — shipped and running. ✓

### DL-1 — Text→SQL multiagent system for data analysts (Shipped)
**Hypothesis:** Data analysts will expand sprint capacity if ad-hoc SQL requests are handled by a Plan-Execute LLM pipeline instead of manual query writing.
**Test method:** Production deployment + capacity measurement with full analytics team.
**Evidence:** "Analytics team capacity expanded by ~20% per sprint" — team lead estimate post-ship, not formally tracked. Directionally reliable, not independently verified.
**Decision:** Green — shipped and running. ✓

### DL-2 — Vibe coding tool for chatbot scriptwriters (Killed)
**Hypothesis:** Giving scriptwriters a vibe coding tool (Kilo Code) lets them stop writing code manually → non-technical hires replace expensive code-savvy people.
**Test method:** Several in-depth interviews + live pilot with one scriptwriter on Kilo Code.
**What we learned:**
1. Vibe coding tools perform poorly on context-heavy codebases, writing new functions, and consistent output quality.
2. Catching tool mistakes still requires understanding code — the skill requirement doesn't disappear.
3. Core assumption (non-technical person can own the output) is false with current tooling.
**Evidence:** "Catching tool mistakes still requires understanding code" — confirmed in live pilot.
**Decision:** Red — killed. Headcount-replacement angle is invalid with current AI tooling.

### DL-2b — Augment scriptwriters on script fixes (Parked — superseded by DL-3)
**Hypothesis (untested):** Existing scriptwriters can recover the confirmed 20% sprint waste on script fixes if given AI augmentation tools adapted to their codebase context — without requiring non-technical replacement hires.
**Why parked:** Superseded by DL-3, which tests a specific narrower angle (diagnosis-only) from the same residual signal.

---

### DL-3 — AI script defect diagnosis for chatbot scriptwriters (In Progress — opened June 4, 2026)

**Hypothesis:**
> Chatbot scriptwriters will reduce script-fix time by ≥50% if AI correctly identifies the root cause of a broken script from script + error log in ≥70% of cases — without writing or modifying code.

**Origin:** Residual signal from DL-2 interviews (20% sprint on fixes confirmed). Key insight: majority of fix time is diagnosis, not the fix itself (1h diagnosis / 15min fix ratio). Diagnosis-only scope avoids DL-2 failure mode (no code generation required → lower LLM quality bar).

**What we tested so far:**
- Method: Synthetic CustDev (persona simulation, June 4, 2026)
- Method: Market scan (June 2026) — no external case studies found for diagnosis-only tools in chatbot teams; angle appears untested publicly
- Method: Hypothesis-check + ICE scoring (June 4, 2026)

**What we learned so far:**
1. Pain confirmed real from DL-2 interviews — not an assumption
2. Synthetic CustDev confirmed: diagnosis time >> fix time ratio holds under pressure
3. Acceptance criterion handed by persona: test on already-fixed scripts — if AI diagnosis matches real root cause ≥70% of the time, trust is established
4. Key technical risk: self-hosted open-source LLM (LLaMA/Mistral) on large interconnected JS scripts — must scope to single-script input, not full codebase
5. Critical objection: "If wrong diagnosis >20-30% of the time, I stop trusting it and go back to manual"

**Evidence so far:**
> "Reading code and logs takes about an hour. The fix itself is usually 15 minutes." — Synthetic CustDev persona (grounded in DL-2 interview pattern)
> "20% sprint time on script fixes" — confirmed in real DL-2 interviews (not estimate)

**ICE:** I=8, C=7, A=8 → **448** (standardized to I·C·A per `skill-hypothesis-generating.md`; prior record was I=8,C=7,E=7→392 on the Effort axis)

**Validation still needed:**
- [ ] 3–5 live interviews with scriptwriters: confirm diagnosis/fix time split in real numbers
- [ ] Technical PoC: collect 10 already-fixed scripts + error logs, run LLM diagnosis, measure accuracy vs. real root causes

**Criteria:**
- **Green:** 3+ of 5 confirm diagnosis time >50% of fix time AND PoC accuracy ≥70% → build
- **Yellow:** Pain confirmed but PoC accuracy 50–70%, OR only 2/5 confirm → pivot: narrow to specific JS error types where LLM performs best
- **Red:** Fix time > diagnosis time for majority, OR PoC accuracy <50% → stop

**What to do next:**
- Next step: Schedule 3–5 interviews with scriptwriter team (warm contact from DL-2)
- Responsible: Product owner

**Related:**
- Previous: DL-2 (killed), DL-2b (parked, superseded by this entry)
- Hypothesis born from: DL-2 residual signal (20% sprint on fixes)

---

### DL-4 — AI utterance generation for NLU training (In Progress — opened June 4, 2026)

**Hypothesis:**
> Scenario writers will recover ≥10% sprint capacity if AI generates diverse NLU training utterances from intent descriptions, reducing utterance-writing time from 1.5–2h per intent to under 30 minutes.

**Origin:** Adjacent unsolved pain on DL-0 team. DL-0 solved RegExp generation — utterance writing was always the next bottleneck. Pattern: every shipped product leaves 2–3 adjacent pains on the same team. Confirmed by synthetic CustDev that utterances take 1.5–2h per intent with 2–4 intents per sprint.

**What we tested so far:**
- Method: Synthetic CustDev (persona simulation, June 4, 2026)
- Method: Hypothesis-check + ICE scoring (June 4, 2026)
- Method: Run 2 hypothesis generation — confirmed as top candidate from 10 new hypotheses

**What we learned so far:**
1. Pain: 1.5–2h per intent × 2–4 intents/sprint = 3–8h/sprint on utterances alone (~5–10% sprint)
2. DL-0 trust transfers directly — same team, same "describe → generate → review" pattern
3. Key risk #1: Output diversity — repetitive utterances harm NLU model quality more than none
4. Key risk #2: Domain-specific intents (mortgages, payments) — AI may lack bank-specific terminology
5. Key risk #3: Russian language quality — unnatural phrasing is worse than manually written utterances
6. Acceptance bar is low: "I describe the intent, it gives examples, I review" — same workflow as DL-0

**Evidence so far:**
> "Every sprint we have 2–4 new intents. Utterances are still fully manual — the boring part of the job." — Synthetic CustDev persona (grounded in DL-0 team context)
> "RegExp generator saved a lot — but utterances are still fully manual." — Synthetic CustDev persona

**ICE:** I=7, C=7, E=8 → **392**

**Validation still needed:**
- [ ] 3–5 live interviews with DL-0 scenario writers: confirm utterance time and sprint frequency
- [ ] Language quality test: generate 50 utterances for a real bank intent, have a scenario writer grade diversity + naturalness
- [ ] Domain test: pick a bank-specific intent (e.g. "early mortgage repayment"), check if LLM output is usable

**Criteria:**
- **Green:** 3+ of 5 confirm utterance writing >1h per intent AND language quality test passes writer review ≥70%
- **Yellow:** Pain confirmed but Russian quality or diversity below threshold → pivot: human-in-the-loop editing step, generate 30 drafts → writer selects + edits best 20
- **Red:** Utterance writing <30 min per intent (pain too small) OR output quality unacceptable after editing → stop

**What to do next:**
- Next step: Interview DL-0 team — warm contact, same team as RegExp generator pilot
- Parallel: Run a quick language quality test with 1 real intent before interviews (2h dev work)
- Responsible: Product owner

**Related:**
- Previous: DL-0 (shipped — RegExp generation for same team)
- Born from: DL-0 adjacent pain, Hypotheses_23_26_2.md run 2 top candidate
- Running in parallel with: DL-3 (same scriptwriter team, different pain)

---

### DL-5 — AI-assisted dashboard/vitrina draft generation for data analysts (In Progress — opened July 10, 2026)

**Hypothesis:**
> Data analysts (DL-1 team) will cut dashboard/vitrina build time by ≥50% on the step after the first requirements draft exists, if an AI agent generates a draft vitrina structure and SQL from stated requirements — with error-prone spots (joins, aggregations) explicitly flagged for fast analyst review. Scope excludes the requirements-gathering/iteration step itself.

**Origin:** Residual signal from a live DL-1 team interview (`Interview_DataAnalysts_28_26_Transcript1.md`, Вахрушева Т.И., July 9, 2026). Raw idea (H-DA-11 from that session's hypothesis-priority pass) originally assumed requirements get "finalized" before generation starts — reframed after synthetic CustDev exposed that assumption as false.

**What we tested so far:**
- Method: Live interview (n=1 — Вахрушева Т.И., DL-1 team, July 9, 2026)
- Method: Hypothesis-check + ICE scoring (July 10, 2026)
- Method: Synthetic CustDev (persona "Дмитрий," senior analyst, same team, July 10, 2026)
- Method: Market scan (July 10, 2026) — global + RU BI / text-to-SQL landscape

**What we learned so far:**
1. Biggest reported time sink is dashboard/vitrina building from scratch — up to a month of cumulative time per instance, but low frequency (~1x/1–2 months; Power BI specifically ~3x/quarter)
2. Real interview corrected the original framing: the bottleneck is **not** SQL/script writing, it's "множество итераций от заказчика" (repeated requirement-clarification cycles with the requester) — "сам запрос — это не самое трудоёмкое"
3. Synthetic CustDev sharpened this further: "finalized requirements" don't really exist — they keep changing after development starts. Hypothesis pivoted from "generate after finalization" to "generate a draft that's expected to survive iteration"
4. Synthetic CustDev's core objection — silent logic errors (e.g., duplicated rows from a bad JOIN) going unnoticed until a stakeholder call — is independently corroborated by the market scan, not just a local fear
5. Market scan found no vendor selling specifically "draft that survives changing requirements" — the reframed angle may be genuine white space, not just this team's blind spot
6. RU BI vendors (e.g., Visiology Cortex) already constrain AI answers to "approved" dashboards/vitrinas to manage exactly this silent-error risk — worth evaluating as a build-vs-reuse option before committing to custom build
7. **Second respondent (Миниахматова, different team, 14.07.2026) independently confirms both pillars of the hypothesis** — low build frequency ("не так часто их создаю... было бы актуально, но опять-таки с периодичностью какой-то") and the requirements-interpretation bottleneck, echoed even outside BI work: "заказчик приходит, и мы понимаем, что на самом деле ему нужно не то, что он просит, а немножко другое." A third analyst (Плеханова, DL-16) shows the same root pattern in a Jira-adjacent context — three independent respondents now converge on "requirement interpretation, not execution, is the narrow point."

**Evidence so far:**
> "Самое трудоёмкое — это... множество итераций от заказчика... а сам запрос, сам скрипт — это нет, не самое трудоёмкое." — Вахрушева Т.И., live interview, 09.07.2026
> "Если ваш агент ждёт, пока требования зафиксируются — он будет ждать вечно." — Synthetic CustDev persona ("Дмитрий")
> "A silent logic error in AI-generated SQL went undetected for 3 weeks and skewed Q3 revenue numbers by 11.7%." — Market scan finding (independent of this team, confirms the CustDev objection is a known industry pattern)
> "Ну, я их обычно один раз сделаю, и потом пишу скрипт по обновлению этих данных, и они уже отрабатывают автоматически... я не так часто их создаю." — Алия Миниахматова, live interview, 14.07.2026

**ICE:** I=7, C=4, A=9 → **252** (I·C·A per `skill-hypothesis-generating.md`). Confidence was capped at 4 for n=1 — now n=2 live interviews confirm the core pattern independently; revisit the Confidence score on the next hypothesis-check pass rather than carrying it forward unexamined.

**Validation still needed:**
- [ ] 3–5 more live interviews with DL-1 team analysts (scoped to "draft survives changing requirements," not "generate after finalization") — confirm the requirements-iteration pattern generalizes beyond one respondent
- [ ] Technical PoC on the self-hosted LLM: generate SQL/vitrina structure from 2–3 historical requirement sets, compare to what the analyst actually built — measure not just % match but **error types and how detectable they are**
- [ ] Evaluate Visiology Cortex or a similar RU tool as a build-vs-buy alternative before committing dev time

**Criteria:**
- **Green:** 3+ of 5 confirm the "draft + expected edits" workflow is acceptable AND PoC shows logic errors (joins/aggregation) are either rare or easily detectable (not silent) → build
- **Yellow:** Pain confirmed but PoC produces silent/hard-to-catch errors more often than acceptable → pivot: narrow to generating only the vitrina schema draft (no SQL) and leave SQL fully to the analyst
- **Red:** 3+ of 5 say draft-vs-final doesn't help (still easier from scratch) OR PoC shows frequent undetectable logic errors → stop, evaluate adopting Visiology Cortex or similar instead of building in-house

**What to do next:**
- Next step: 3–5 interviews with DL-1 team, updated scope ("draft, not final")
- Parallel: collect 2–3 historical requirement sets + actual analyst output for the PoC
- Responsible: Product owner

**Related:**
- Previous: DL-1 (shipped, same team) — this is a DL-1 extension hypothesis, not a fresh role
- Methodologically similar to: DL-3 (narrowed scope after a broader vibe-coding attempt failed in DL-2)
- Born from: `Interview_DataAnalysts_28_26_Transcript1.md` (Вахрушева Т.И., 09.07.2026), H-DA-11 from that session's hypothesis-priority pass (10.07.2026)
- Running in parallel with: DL-3, DL-4 (scriptwriter team, different pain)

---

### DL-7 — AI narrative summary for stakeholder reports, H-DA-3 (Killed — 09.07.2026)
**Hypothesis:** Analysts will save time on report narratives if AI generates textual explanations of metric changes.
**Test method:** Live interview — Вахрушева Т.И., DL-1 team, 09.07.2026.
**Evidence:** «Обычно не тратим, потому что нас просят присылать просто числа.» / «Мне кажется, это бы могло улучшить, но сейчас не требуется. Ну, активно не требуется.» — Вахрушева Т.И., 09.07.2026.
**Decision:** Red — killed. No stakeholder demand for narrative text; respondent explicitly says it isn't needed. Revisit only if stakeholders themselves request it.

### DL-8 — AI brief for anomaly investigation, narrow scope, H-DA-2 partial test (Killed for tested scope — 09.07.2026)
**Hypothesis:** Analysts will save 30–60 min per alert if AI investigates root causes of anomalies.
**Test method:** Live interview — Вахрушева Т.И., 09.07.2026. Only data-quality anomalies (missing values, mismatched columns) were tested — metric-threshold alerts (the original H-DA-2 scope) weren't covered.
**Evidence:** «Редко-редко, я бы сказала, единичный случай.» / «Ну, этап предобработки, это не очень долго» — Вахрушева Т.И., 09.07.2026.
**Decision:** Red for the tested narrow case (data-quality anomalies — rare, self-handled, no tool needed). Original H-DA-2 scope (metric-drop alerts) remained untested here → re-opened and confirmed as real pain in DL-11, different scope.

### DL-9 — Auto-refresh of recurring reports, H-DA-1 (Killed — 09.07.2026, confirmed by 2nd respondent 14.07.2026)
**Hypothesis:** Analysts will save 3–5h/week if AI auto-refreshes recurring reports.
**Test method:** Live interviews — Вахрушева Т.И. (09.07.2026) + Миниахматова (14.07.2026, independent confirmation, different team).
**Evidence:** «Нет, они все, на самом деле, автоматически. Мы пишем скрипт, ставим по времени...» — Вахрушева Т.И. «Но у нас скрипты написаны. Мы тоже вручную это не считаем.» — Миниахматова.
**Decision:** Red — killed, confirmed by two independent respondents from different teams. Recurring-report refresh is already fully automated by existing scripts; no manual analyst time spent here.

### DL-10 — Knowledge base for onboarding / shared SQL library, H-DA-12 (consolidated, 3 respondents; merges DL-6) (Mixed — 09.07–22.07.2026)
**Hypothesis:** Onboarding time will drop and/or experienced analysts will save time with a shared knowledge base (SQL query library, glossary, metric definitions).
**Test method:** Live interviews — Вахрушева Т.И. (09.07.2026), Миниахматова (14.07.2026), Плеханова (22.07.2026) — 3 respondents, 3 different teams.
**Evidence:** «У нас таких, к сожалению, нет. Вот в этом большая проблема.» — Вахрушева Т.И. But: «Я очень люблю писать оптимизированные SQL-запросы, поэтому, наверное, я в этом даже как будто не нуждаюсь.» — Миниахматова. «...было бы полезно... но сейчас необходимости нет.» — Плеханова.
**Decision:** Red for "shared library for experienced analysts" — 3/3 respondents show no personal need, informal script-sharing already covers it. Onboarding-specific pain (for an actual new hire) remains untested — all 3 respondents were experienced, not new. Spun off: data-source catalog idea (see DL-12).

### DL-11 — AI agent for metric-drop root-cause investigation, H-DA-2 retest on a different team (Yellow — pivot, 14.07.2026, updated 22.07.2026)
**Hypothesis:** Analysts will save time if an agent has knowledge of all anomalies and data sources to help investigate metric drops.
**Test method:** Live interview — Миниахматова (14.07.2026), corroborated by Вахрушева's own example the same day and directly by Плеханова (22.07.2026, see DL-17).
**Evidence:** «Частая история, потому что Маша делает овервью каждый день. ...может тратить минимум час, но иногда может целый день.» — Миниахматова. «Я иногда могу потратить 30 минут в день, а иногда могу потратить всю неделю.» — Плеханова, 22.07.2026.
**Decision:** Yellow — pivot. Pain is real and daily (contrasts with DL-8's "rare" verdict — different scope). "Agent with knowledge of the whole bank" is an aspirational scope, not directly testable → narrowed into DL-17 (incident classification, a concrete sub-task).

### DL-12 — AI catalog of data sources across bank warehouses/vitrinas (Mixed, team-specific — 14.07.2026, updated 22.07.2026)
**Hypothesis:** Analysts will save time if an agent knows table/field structures across bank data warehouses and points to where data lives.
**Test method:** Live interviews — Миниахматова (14.07.2026), Плеханова (22.07.2026, independent second team).
**Evidence:** «Нет, у нас ничего нет. Мы узнаем только как-то сами. ...часто бывает, что можно целый вечер провести... чтобы что-то найти.» — Миниахматова. Contradicted by Плеханова: «Мы, как правило, используем определенный набор таблиц, которые мы уже знаем... Это большая редкость.»
**Decision:** Red for Плеханова's team (stable, well-known table set — not a pain there). Pain confirmed substantively for Миниахматова's team. Likely team/product-specific rather than role-wide — not prioritized as a standalone hypothesis without narrowing to teams with frequent novel queries.

### DL-13 — AI narrative for presentation slides, H-DA-9, 2nd respondent + primary source (Killed — 14.07.2026, closed 22.07.2026)
**Hypothesis:** Analysts will save 30–45 min per presentation if AI writes the slide narrative text.
**Test method:** Live interviews — Миниахматова (14.07.2026, describes it as someone else's work) + Плеханова (22.07.2026, the actual person doing this work, first-hand).
**Evidence:** «На саму презентацию мало... на само заполнение на самом деле немного. У нас еще есть Ира Чуб, которая занимается... сбором инфы.» — Плеханова, 22.07.2026.
**Decision:** Red — killed, three respondents in a row including the primary source. Slide text itself takes little time; the real time sink is upstream requirement negotiation and impact calculations, not narrative writing.

### DL-15 — AI summary of anomaly root causes after investigation (Killed — 14.07.2026, closed 22.07.2026)
**Hypothesis:** Analysts will save time if AI automates writing the post-investigation summary (incident → intent → metric impact).
**Test method:** Live interviews — Миниахматова (14.07.2026, describes Плеханова's practice) + Плеханова (22.07.2026, first-hand).
**Evidence:** «Написать отчет у меня занимает, не знаю, 5-7 минут... я не готовлю там прям огромные какие-то расписные истории.» — Плеханова, 22.07.2026. «Основное мое время именно уходит на анализ.»
**Decision:** Red — killed. Writing the summary text is already fast (5–7 min); the real bottleneck is upstream analysis, not text generation. Closes H-DA-3/DL-7 for a second team with the same verdict.

### DL-16 — Jira automation: task creation + status collection, H-DA (consolidated, 2 respondents; merges DL-14) (Split into DL-18/DL-19 — 14.07–23.07.2026)
**Hypothesis:** Analyst/team lead will save time if an AI agent auto-creates Jira tasks from unstructured customer requests and auto-collects task statuses for a weekly report.
**Test method:** Live interviews — Миниахматова (14.07.2026), Плеханова (22.07.2026, independent 2nd team, 2nd facet of the pain).
**Evidence:** «Я практически весь день только тем и занималась, что заводила их в джиро.» — Миниахматова. «Меня на это уходит на весь отдел вся пятница... я эксельку выгружаю, собираю, просто раскрашиваю.» — Плеханова.
**Decision:** Yellow — pivot. Pain confirmed by 2 independent respondents, 2 different facets (task creation vs. status rollup). Split into two separately testable hypotheses — see DL-18 (task creation) and DL-19 (status collection).

### DL-17 — AI classification of customer messages against incidents (Yellow — pivot, 22.07.2026)
**Hypothesis:** A ЧБ-1 analyst will cut time confirming incident impact if an AI classifier can match incoming message text to a registered incident, replacing manual intent review + scriptwriter consultation.
**Test method:** Live interview — Плеханова, 22.07.2026.
**Evidence:** «Сэкономило бы колоссальное количество времени, но есть одна проблема. На текущий момент аварии никак не размечаются. И обращения по этим авариям никак не размечаются... Даже не только в БД. В целом данные в компании такие отсутствуют.»
**Decision:** Yellow — pivot. Pain is real and daily, but no labeled training/matching data exists anywhere in the company — can't be tested as a straight classifier. Narrow to zero/few-shot classification against incident description text, validated on historical known-incident examples, before any PoC.

### DL-18 — Auto-create Jira tasks from customer requests, split from DL-16 (component A) (Yellow/In Progress — opened 23.07.2026)
**Hypothesis:** Analysts will save ~3h/week entering Jira tasks if AI auto-creates tasks from customer requests.
**Test method:** Reused live-interview data (Миниахматова, Плеханова) + synthetic CustDev with a team-lead persona, 23.07.2026.
**Evidence:** «Не факт. ...если ИИ создаст задачу, но неправильно поймёт, что заказчик хотел, я всё равно буду это разгребать, только на другом этапе. Мне не нужно, чтобы задачи появлялись быстрее — мне нужно, чтобы они появлялись правильно.» — synthetic team-lead persona, 23.07.2026.
**Decision:** Yellow — pivot. Pain is real but the target audience may be wrong (team leads don't create tasks personally — rank-and-file analysts do), and the real bottleneck may be requirement clarification with the requester, not task creation itself. Test on individual analysts next; split "time to create" from "time waiting on a clarifying answer."

### DL-19 — Auto-collect statuses/deadlines for weekly team report, split from DL-16 (component B) (Yellow/In Progress — opened 23.07.2026)
**Hypothesis:** A team lead will save time preparing the weekly status report if an agent finds stale/overdue Jira tasks, pings analysts for status/deadline/reason confirmation, and compiles the report.
**Test method:** Reused live-interview data (Плеханова) + synthetic CustDev with a team-lead persona, 23.07.2026.
**Evidence:** «Меня на это уходит на весь отдел вся пятница... основное время именно уходит на то, чтобы сбиться с каждым аналитиком и спросить, ты обновил?» — Плеханова, 22.07.2026. «Вот это уже интереснее. ...Но тогда мне нужно доверять, что он ничего не напутал в том, что есть в системе.» — synthetic team-lead persona, 23.07.2026.
**Decision:** Yellow — pivot. Pain confirmed and mechanism validated (active polling, not passive aggregation), but the single time figure is n=1/unmeasured, and analyst responsiveness to an automated ping (vs. a human team lead) is untested. Pilot for 1 sprint: draft report with flagged gaps, team lead fills in, measure analyst response rate/speed.
