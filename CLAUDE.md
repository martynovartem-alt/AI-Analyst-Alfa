# CLAUDE.md

This file provides product and team context for AI-assisted hypothesis discovery work. It is not a code project — it is a product strategy document. Read it to understand who the user is, what they've already validated, and what they're trying to figure out next.

**Full decision-log entries live in `decision-log.md` (canonical). This file carries strategy, context, and a one-line-per-entry Decision Log Index.**

---

## Product context

**Product:** AI Augmentation Platform for bank IT teams
**What it does:** Identifies high-friction roles inside banks and ships AI tools that reduce manual time waste in those roles — without replacing people, augmenting their output.
**Stage:** Post-MVP on two shipped products; in an active hypothesis discovery cycle (15 cycles recorded in July 2026 alone).
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
- **Team:** Product owner (me, prompt/low-code) + 1–2 developers (dedicated full-time). Active collaborators since Aug 2026: Арман Урбисинов (PM interviews — Шмаков 18.08, Долгова 23.08; DL-19 planning notes + OST) and Ольга Григоренко (analyst interviews, DL-20, scriptwriter hypothesis revision H-SW-26…52)
- **AI stack:** Dual — external APIs (OpenAI / Anthropic) for prototyping; self-hosted open-source LLM (LLaMA / Mistral family) for production. Quality gap is real and significant. Always validate the hypothesis on the internal model before committing — structured tasks (RegExp, SQL) degrade less than reasoning-heavy or long-context tasks.

### How hypotheses are discovered

1. Market research — track how AI tools are changing specific role workflows externally (e.g. new tooling releases, role-specific AI adoption)
2. Interviews — go to the team, map their workflow, find where time is actually spent
3. Product data — internal case registries handed over by team product owners (e.g. `Cases_Scriptwriters_28_26.md`)

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

**Candidate roles — ranked by evidence × access (updated 19.08.2026):**

| Role | Access | Evidence status (see Decision Log Index for verdicts) | Rank |
|---|---|---|---|
| Data analysts / Аналитики данных (DL-1 team + 2 more teams) | **Have access**, incl. live тимлид contact (Соколова, ЧБ-1) since 23.07 | 3 live interviews done (Вахрушева 09.07, Миниахматова 14.07, Плеханова 22.07) + live talk with тимлид ЧБ-1 (Соколова 23.07) → cycles DL-5…DL-20. Strongest surviving: DL-19, DL-18 (Jira automation), DL-17 + its untested narrowing DL-20 (clustering). Most narrative/report hypotheses killed. DL-5 open but weakened. OST built 07.08 (`OST_DataAnalysts_28_26.md`). **10.09.2026 — the track entered build: DL-19 «Отчёт-бот» is in pilot with a live team** | **#1** |
| Chatbot scenario writers / Сценаристы чат-ботов | **Have access** | DL-3/DL-4 stalled at synthetic stage (deadline 14.06 passed, no live interviews yet; guides ready). Product-data track: 12-case registry → H-SW-17…25 (23.07) + revised H-SW-26…52 (27.07, Григоренко: dedup vs in-flight case initiatives, augment-framing enforced). Cursor pilot (May–June, 5 scriptwriters) has no recorded results | **#2** |
| Product designers / Продуктовые дизайнеры | **Have access (via developer contact Николай Шубич, since 14.07.2026)** | H-PD-3/5 confirmed & in development by the developer; H-PD-4 pain confirmed but already covered by an existing tool (Clade) — not being built. Zero live interviews with a designer themselves; round-2 guide ready | **#3** |
| Product managers / Продакт-менеджеры | **Live contact established** — 4 live interviews done: Валентин Шмаков 18.08, Ксения Долгова 23.08, Анастасия Дубкова + Алексей Лаврищенко 26.08 (interviewer Арман Урбисинов) | 11 live-evidence cycles DL-21…DL-31: H-PM-4 → wrong role (PRD written by бизнес-аналитик, confirmed independently **three** times), H-PM-12 killed for respondent (reinforced 26.08), H-PM-9 partial (BI config, not LLM), **H-PM-2 (was top-ranked, ICE 216) weakening on 3 of 4 live respondents** (near-total BI self-service / no clarification-round friction), H-PM-17 strengthened, H-PM-8 narrowed to a status-notification artifact. **26.08: H-PM-1 (VOK diagnosis) reopened** — 2 new respondents personally burn major time on it, internal LLM already tried and failed on this exact task; **H-PM-19 (impact estimation) gets its first live data and jumps to new #1 by ICE (252)** — named the single hardest part of master-plan work by both new respondents; **2 new hypotheses registered** (H-PM-22 self-serve data access reusing shipped DL-1, H-PM-23 service/contact catalog echoing DL-12) | **#4** |
| *Business analyst / Бизнес-аналитик (spawn из DL-21, 19.08; readdressed 27.08)* | **2 live respondents (28.08, 02.09)** — Ольга Серегина (dedicated BA, CRM/SFA) via Урбисинов; Алексей Трифонов (product owner doing the BA job, import-substitution СФА «Юрлиц») interviewed by Чукреева. Still needed: a BA-function respondent on a product that actually owns a client metric | Hypotheses reused from the PM registry (`Hypotheses_BusinessAnalysts_35_26.md`, 27.08.2026 — see note below for why); readdressed set now H-BA-1 (was H-PM-4/H-PM-17) + H-BA-2 (was H-PM-1). First synthetic CustDev run 27.08.2026 (persona «Наталья», `SKILL/BusinessAnalysts`) — narrows H-BA-1 to a linear pilot step + source-traceability requirement, weakens H-BA-2 for this persona's process (lead-transfer, not a regular VOK-style metric), gets first BA-side echoes for H-PM-11 (spec verification) and H-PM-23 (contact catalog). **28.08:** second synthetic run (contrast persona «Алексей») + 3 new hypotheses H-BA-3…5 (late-surfacing-contradiction detection is his top pain; H-BA-2 weak twice in a row; H-BA-4 predictions diverge between personas). Current scenario: v2 with both personas' predictions embedded as `SYNT PERSONA ANSWER:` for live comparison (`Live_interview/BusinessAnalysts/Interview_BusinessAnalysts_35_26_H1_BA_v2_synt.md`); zero live BA interviews still. **28.08 (live):** first live БА-интервью — Ольга Серегина (CRM/SFA-команда) → DL-32…DL-35. H-BA-1 confirmed live, ICE 315 (respondent already drafts BRD/user story/prototypes daily via external LLMs; internal Альфаген tried and found insufficient on this task). H-BA-5 confirmed live as her self-named top pain, ICE 320 (cross-source context gathering — Confluence/Jira/Abuk). H-BA-2 disconfirmed for this respondent — different product, no client-facing metrics — team-specific, not role-wide. H-BA-3 not confirmed in the stated form (respondent describes consolidation, not contradiction-detection). H-BA-4 untested. `SKILL/BusinessAnalysts` recalibrated with a new live-based persona «Оксана»; «Наталья»/«Алексей» kept as synthetic reference angles for the untested profile (multi-department conflict, BRD from scratch). **02.09 (live, 2nd respondent — Алексей Трифонов, PO doing the BA job): 9 cycles DL-36…DL-44.** Role mapping changed: import-substitution teams have no dedicated BA at all, so the track ICP is now defined by function, not job title (DL-36). H-BA-1 confirmed a 2nd time, ICE 315→432 — and an **internal AI agent for system analysts already integrated with Confluence + Git** was found, the project's first live precedent of a passed integration/ИБ gate (DL-37). H-BA-5 confirmed a 2nd time with the first quantitative anchor (business-analysis phase ≈ месяц-полтора), ICE 320→360, but with a ceiling: much of the context exists in no document at all (DL-38). H-BA-3 unconfirmed twice → pivoted into **new H-BA-11 (AI-generated clarifying questions + uncovered-area detection), ICE 504 — new track leader, 2 of 2 live respondents, zero integrations needed** (DL-39). H-BA-4 confirmed live for the first time (ICE 90) but blocked by never-updated BRDs (DL-40); H-BA-6 segmented to from-scratch projects with a negative tech baseline (ICE 90, DL-41); H-BA-7 pivoted from «ИБ-safe» to «integrated», H-BA-8 promoted to a mandatory MVP element (DL-42); 2 new hypotheses registered — H-BA-10 (incremental BRD updating, ICE 210, DL-43) and H-BA-9 (metric-anomaly alerts, ICE 125, DL-44); H-BA-2 disconfirmed in first person for the 2nd time in a row | — |

> **Canonical role names (EN / RU) — use the same pair in every file (`CLAUDE.md`, `SKILL/`, `roles/`, decision log):** Data analysts / Аналитики данных (`SKILL/DataAnalysts`) · Chatbot scenario writers / Сценаристы чат-ботов (`SKILL/ScenarioWriters`) · Product designers / Продуктовые дизайнеры (`SKILL/ProductDesigners`) · Product managers / Продакт-менеджеры (`SKILL/ProductManagers`) · Internal customer / Заказчик — demand-side counterpart, not an IT role (`SKILL/InternalCustomer`) · Business analyst / Бизнес-аналитик (`SKILL/BusinessAnalysts`).

> **Note:** "Chatbot scriptwriters" and "scenario writers" are the same role — one person writes both JS scripts and NLU training data (intents, utterances, RegExp). DL-3 and DL-4 both target this role.

> **Note (updated 14.07.2026):** Product designer access is resolved — reached through a developer (Николай Шубич) who is already building AI tools for that role. ~~Product manager access is still unresolved~~ — **superseded 18.08.2026:** PM access resolved — Арман Урбисинов conducted the first live PM interview (Валентин Шмаков) → DL-21…DL-24.

*Ranking logic: access is the binding constraint at <1 year tenure. Data analysts and scriptwriters have existing relationships and can be interviewed now. **⚠️ The #3-vs-#4 ordering premise is now obsolete (19.08.2026):** designers ranked above PMs because PM access was zero — but PMs now have a live interview while designers still have none. Revisit the order on the next ranking pass: PM evidence is live but mostly disconfirming (DL-22 killed, DL-21/24 point to adjacent roles), while designer evidence is confirmed-but-secondhand.*

> **Note (27.08.2026) — Business Analyst track reuses the PM hypothesis registry, not a fresh generation:** `Hypotheses_BusinessAnalysts_35_26.md` readdresses the existing PM registry (`Hypotheses_ProductManagers_28_26.md`, H-PM-1…23) instead of generating candidates from scratch. Reason: bank-specific role mapping. Across three independent live PM interviews (Шмаков DL-21, Долгова DL-26, Лаврищенко 26.08) ownership of detailed requirements — PRD, CJM, BPMN — consistently landed on the **бизнес-аналитик**, not the PM. In this bank, the БА role is functionally closer to the *original* candidate-role thesis behind the PM hypotheses (owns requirements, CJM, task framing) than the PM role turned out to be in practice — PM reads more as a coordination/prioritization role (see DL-21/DL-26/DL-28 and the #3-vs-#4 ordering note above). First synthetic CustDev for this track ran 27.08.2026 (`roles/BusinessAnalysts/synthetic_custdev_business_analyst/session_natalya_business_analyst_syntetic_custdev.md`); interview guide for the first live BA respondent is ready (`Live_interview/BusinessAnalysts/Interview_BusinessAnalysts_35_26_H1_BA.md`).

> **Note (25.07.2026) — key team-lead contact:** Ирина Соколова is the **тимлид ЧБ-1 — Плеханова's team lead**. Live contact since 23.07.2026 (see DL-18/DL-19 correction notes): she confirmed the «черновик + дозаполнение пробелов» scenario for DL-19 and the ЦА signal for DL-18 ("team leads don't create tasks personally"). This also resolves the role question in `MVP_DevPlans_30_26.md` (MVP-1 §6 «Роль и санкция»): Плеханова is the analyst responsible for the weekly report, not the formal team lead — Соколова is the natural pilot approver and announcement sender for MVP-1/MVP-2, matching the ICP («decision to try a tool is made at team lead level»).

**Cross-interview pattern (July 2026) — shapes how new hypotheses should be framed:** 3 of 3 interviewed analysts independently converge on the same bottleneck — **interpreting customer requirements, not technical execution** («сам запрос — это не самое трудоёмкое»; newcomers «плохо понимают язык заказчиков»; incomplete briefs from requesters). This explains why narrative/report-generation hypotheses died (DL-7, DL-9, DL-13, DL-15) and why the survivors (DL-17, DL-18, DL-19, reframed DL-5) all sit at the requirements/communication step, not the execution step. Source: DL-5 item 8 in `decision-log.md`.

**Note on Scrum Masters:** Removed — they don't exist as a distinct role in this bank. Team leads double as SMs. The sprint reporting pain (30–120 min/sprint) is real but falls on team leads, not a separate role. DL-19 (weekly status collection, «вся пятница») is exactly this class of team-lead pain surfacing again — from a live respondent this time.

**Note on security approval (ИБ) as a cross-role blocker — partially contradicted (14.07.2026, see Developer Status Report in `Hypotheses_ProductDesigners_28_26.md`: at least two designer-facing tools already passed this stage):** Surfaced independently in two synthetic CustDev sessions for two different roles — designer persona Ирина ("даже обычного Figma AI нет — IT не одобрил") and PM persona Сергей ("если нужен доступ к системам — тогда уже с ИБ"). Not yet confirmed in a live interview, but the pattern repeating across unrelated synthetic personas is worth tracking: any future AI tool requiring system/data access may face a security review gate independent of team-lead buy-in. Ask about typical ИБ approval turnaround time in the next live interview for any role, not just designers/PM. **Update:** the Developer Status Report shows two designer-facing tools (H-PD-3/5, H-PD-4) already past this stage — either the gate isn't uniformly slow, or Irina's synthetic persona described a different part of the org than the developer's contact works with. Ask directly in the next live designer interview (see `Interview_ProductDesigners_28_26_H2_PD.md`) rather than assuming either signal is right.

**Market scan findings (June 2026):**
- Data analysts (DL-1 team): "Business analyst" in this bank = analytics role (SQL, dashboards, Excel) — NOT a requirements-writing BA. Same team as DL-1. SQL pain is already solved. Remaining pain is dashboard creation, Excel report generation, analysis commentary writing. This is an extension hypothesis, not a fresh role. *(July interviews later killed the commentary/report angles — see DL-7/9/13/15 — and weakened dashboards — DL-5.)*
- Chatbot scriptwriter augmentation has zero published case studies externally. Either untapped or not yet done publicly.
- Roles out of scope: Data engineers (context-heavy, same failure mode as DL-2), Security/Antifraud (different department).
- Killed after synthetic CustDev: Intent coverage gap detection (needs conversation logs → PII constraint, hard blocker).
- ~~Product managers, product designers: no market scan run yet~~ — superseded: dedicated hypothesis packs + market-scan rounds ran 10–21.07.2026 (`Hypotheses_ProductManagers_28_26.md`, `Hypotheses_ProductDesigners_28_26.md`).

**→ Next actions (updated 19.08.2026; full criteria per entry in `decision-log.md`):**
- **Build phase (updated 10.09.2026): DL-19 is no longer a plan — the MVP is built and in pilot with a live team.** This is the project's first MVP to reach pilot since DL-0/DL-1, and the whole portfolio order in `MVP_Candidates_36_26.md` shifts accordingly: the single development stream is now occupied. What still has to be closed on this pilot: (a) confirm whether the ≈8 h/wk baseline was measured BEFORE switch-on — unconfirmed as of 10.09, and without it the pilot cannot verdict on time saved; (b) confirm 🟢/🟡/🔴 criteria are pre-committed into the DL-19 entry; (c) measure ping-response rate and latency — the hypothesis's main unretired risk. Dev plans for DL-18/DL-17 remain ready in `MVP_DevPlans_30_26.md` but are not started; DL-18 has the wider dependency set (mail relay, Exchange admins), DL-17 is gated on the ИБ decision for the PoC dataset.
- **DL-18/DL-19 (Jira automation, analysts):** interviews with rank-and-file analysts with split time questions (creation vs clarification); quantitative Jira checks (delay between request and task creation; status staleness); 1-sprint draft-report pilot for DL-19.
- **DL-17 (incident classification):** narrow to zero/few-shot classification on historical incidents (no labeled data exists); ask scriptwriters their side of the consultation load.
- **DL-5 (dashboards):** 2–4 more DL-1-team interviews in "draft, not final" scope + fix the sprint-share question; PoC on historical requirement sets; evaluate Visiology Cortex as build-vs-buy.
- **DL-3/DL-4 (scriptwriters):** execute the ready interview guides (`Interview_Scriptwriters_28_26_H1_SW.md` / `_H2_SW.md`); record Cursor pilot results if the pilot ran (`Cases_Scriptwriters_28_26.md`).
- **Designers:** live interview with an actual designer via Шубич (guide: `Interview_ProductDesigners_28_26_H2_PD.md`); clarify tool boundaries with Шубич (H-PD-11/H-PD-14 vs his H-PD-3/5).
- **Product managers (updated 26.08):** 3rd and 4th live interviews done (Дубкова + Лаврищенко, 26.08 → DL-28…31). H-PM-2 (former top-rank, ICE 216) keeps weakening — 3 of 4 live respondents show no PM-side clarification friction; H-PM-19 (impact estimation) finally gets live data and becomes the new ICE leader (252) — both new respondents independently call effect/volume estimation the hardest part of master-plan work; H-PM-1 (VOK diagnosis) reopens on 2 new respondents personally burning heavy time on a live VOK-drop crisis, with a first concrete tech-risk data point (internal LLM already tried on this exact task, failed — too generic); 2 new hypotheses registered (H-PM-22 self-serve data access reusing shipped DL-1; H-PM-23 service/contact catalog echoing DL-12, likely misaddressed to system analyst). Still open across all 4 live respondents: hours on «образ результата» (DL-21/H-PM-21); the cross-role ИБ-turnaround question, never asked live of any role in 4 interviews; whether Дубкова and Лаврищенко sit in the same reporting line (unconfirmed org link, see registry sverka). Next: technical fact-check with the DL-1 owner on H-PM-22 feasibility (cheap, no interview needed); ask VOK-crisis frequency outside the current peak in the next PM interview before trusting H-PM-1's new ICE. Use the round-2 guide (`Live_interview/ProductManagers/Interview_ProductManagers_28_26_H2_PM_round2.md`).
- **Business analysts (updated 02.09):** 2 live respondents done (DL-32…DL-44). Cheapest next steps need no interview: (a) run 3–5 real «context → list of questions» pairs through Альфаген — a direct test of the new leader **H-BA-11 (ICE 504)** and a 3rd attempt to characterise the internal model's failure class; (b) technical recon on the system-analyst agent that already integrates with Confluence/Git — who built it, how the ИБ approval went, is the contour reusable (removes the Ease risk from H-BA-1, H-BA-5, H-BA-8, H-BA-10 at once). 3rd interview must be **deliberately selected, not snowballed**: a BA-function respondent on a product that owns a client metric (last chance for H-BA-2 before closing it role-wide) and ideally on a from-scratch project (last chance for H-BA-3, only relevant segment for H-BA-6). Recruit by asking «who writes the business requirements and talks to the customer», not by job title (DL-36).
- **DL-20 (clustering, untested):** PoC on historical requests of ЧБ-1 (embeddings + clustering) → show clusters to Плеханова, ask if she recognizes real incidents; pre-commit an acceptable false-merge threshold.
- **DL-10 residual:** interview a real newcomer (≤2 months in role) — the only open part of the onboarding knowledge-base hypothesis.

**Out of scope:** DevOps/SRE/infrastructure roles; Security/Antifraud — separate department, no access.

---

## Workflow (the core loop)

**One-time setup** *(already done for this product):*
- Fill in `CLAUDE_template.md` for a specific product → save as `CLAUDE.md`

**Per hypothesis cycle:**
0. **Generate candidates** using `skill-hypothesis-generating.md` — pull signals from market, CustDev, and product data → get a ranked list of 5–10 candidate hypotheses
1. Run the top candidate through `skill-hypothesis-check.md` → get a structured hypothesis + ICE score
2. Run a synthetic CustDev session using `skill-synthetic-custdev.md` → surface objections before real interviews
3. **Targeted market scan** using `skill-market-scan.md` → deep report on the specific hypothesis: TAM, players, trends, gaps — all with sources (different from step 0 — this is narrow, not broad)
4. Record the outcome per `skill-decision-log.md` as a full `DL-N` entry in **`decision-log.md`** (canonical)
5. Add/update the one-line row for that `DL-N` in the `## Decision Log Index` below → so the next session inherits current state without loading the full log
6. **Update the cross-role backlog** — `HypothesisBacklog.md` (full scoreboard) **and** `HypothesisBacklog_v2.md` (compact ID+ICE view), both together. Added 04.09.2026: the backlog went stale twice in a row (13.08→26.08 and 26.08→04.09, the second time across two live interviews and 13 DL entries) precisely because this step was missing from the list — see `HypothesisBacklog.md` → «Проблемы данных», п.5

One full cycle is ~3 hours. The loop is closed when the full entry lives in `decision-log.md`, its index row lives here, **and both backlog files reflect the new/changed ICE**.

## Files and their roles

| File | Role |
|---|---|
| `CLAUDE.md` | This file — product context, strategy, Decision Log Index |
| `decision-log.md` | **Canonical Decision Log** — full DL-0…DL-44 entries with evidence |
| `MVP_DevPlans_30_26.md` | **MVP-1 (DL-19) is in pilot since 10.09.2026; MVP-2/MVP-3 not started.** Dev plans for the three build candidates (25.07.2026): Отчёт-бот (DL-19), Задача-бот (DL-18), offline classification PoC (DL-17); updated 12.08 with DL-19 working notes |
| `OST_DataAnalysts_28_26.md` | Opportunity Solution Tree (07.08.2026) for the data-analyst hypothesis family — DL-19/DL-18/DL-17/DL-5 under one business goal, with rejected solution alternatives per branch |
| `tasks_dl19/` | DL-19 build-task breakdown (12.08, Урбисинов) |
| `HypothesisBacklog.md` / `HypothesisBacklog_v2.md` | Cross-role ICE scoreboard (13–14.08.2026) — flat non-canonical view over all `Hypotheses_*` files + decision log; canon stays in `decision-log.md` |
| `CLAUDE_template.md` | Product context template — fill in per product, rename to `CLAUDE.md` |
| `skill-hypothesis-generating.md` | Generates hypothesis candidates from 3 sources (market, CustDev, product data) |
| `skill-hypothesis-check.md` | Structures a raw idea into a testable hypothesis + ICE (I·C·A, 1–10) + go/pivot/stop criteria |
| `skill-synthetic-custdev.md` | Turns Claude into a specific ICP persona for a practice interview session |
| `skill-market-scan.md` | Produces a structured market report: TAM, players, trends, gaps — all with sources |
| `skill-decision-log.md` | Template for recording what was tested, what was learned, and the next step |
| `SKILL/` (`DataAnalysts`, `ScenarioWriters`, `ProductDesigners`, `ProductManagers`, `InternalCustomer`, `BusinessAnalysts`) | Pre-filled synthetic-CustDev persona prompts per role (file names = canonical CamelCase role tokens, unified 28.08): `DataAnalysts` = Data analysts / Аналитики данных (rebuilt 26.08 on the 3 live July transcripts — persona «Катя», placeholder gap closed), `ScenarioWriters` = Chatbot scenario writers / Сценаристы чат-ботов (rebuilt 26.08 on the case registry — product data, no live interview yet), `ProductDesigners` = Product designers / Продуктовые дизайнеры (rebuilt 26.08 on the Developer Status Report — secondhand, no live interview yet), `ProductManagers` = Product managers / Продакт-менеджеры (re-calibrated 19.08 on live DL-21…24 facts, cost-center framing), `InternalCustomer` = Internal customer / Заказчик (first demand-side persona, 19.08 — synthetic-only), `BusinessAnalysts` = Business analyst / Бизнес-аналитик (created 26.08; recalibrated 28.08 on the first live BA interview — new primary persona «Оксана», live-calibrated; «Наталья»/«Алексей» kept as synthetic reference angles for the untested multi-department-conflict profile) |
| `roles/ProductManagers/synthetic_custdev_19_08/` | Synthetic-CustDev session transcripts 19.08 (PM «Игорь», заказчик «Марина») testing H-PM-17…21 — first synthetic sessions persisted to the repo |
| `roles/` | **Per-role workspaces (restructured 19.08.2026)** — hypothesis packs, market scans, and synthetic-CustDev transcripts live under `roles/<Role>/` |
| `Live_interview/` | **Live-interview workspace (28.08.2026)** — interview guides (scenarios) and live-interview transcripts for all roles, one subdirectory per canonical role token: `Live_interview/<Role>/`. Moved here from `roles/<Role>/` on 28.08; save future transcripts here |
| `roles_description/` | Role cards per canonical role + `all_roles_description.md` (verbatim copy of the candidate-roles ranking from this file — update both together) |
| `roles/Hypotheses_AllRoles_23_26.md` | June canonical run — data analysts + scenario writers, 20 hypotheses. ⚠️ Statuses frozen at 09.06; current verdicts in `decision-log.md`. H-DA-3/H-DA-9 diverged from the July files — see its header note |
| `roles/DataAnalysts/Hypotheses_DataAnalysts_28_26.md` | July hypothesis-check pass for analysts (H-DA-11…14 line; updated 23.07 with DL-7/10/13 verdicts) |
| `roles/ScenarioWriters/Hypotheses_Scriptwriters_28_26.md` | July pass, H-SW-1…16 (market + vision + synthetic CustDev) + revised H-SW-26…52 addendum (27.07, Григоренко) |
| `roles/ScenarioWriters/Cases_Scriptwriters_28_26.md` | Raw product-data case registry from the team's product owner (12 cases + effort metrics + Cursor pilot plan), 23.07 |
| `roles/ScenarioWriters/Hypotheses_Scriptwriters_FromCases_28_26.md` | H-SW-17…25 derived from the case registry (pre-ICE, metrics pending) |
| `roles/ProductDesigners/Hypotheses_ProductDesigners_28_26.md` | July pass, H-PD-1…15; includes the Developer Status Report (Шубич, 14.07) |
| `roles/ProductManagers/Hypotheses/Hypotheses_ProductManagers_28_26.md` | **Canonical PM hypothesis registry.** July pass H-PM-1…13 (synthetic + market) + сверка с живым интервью 18.08 (DL-21…24) + регистрация арены H-PM-14…16 + новая генерация H-PM-17…21 и повестка второго интервью (19.08) + сверка со 2-м живым интервью 23.08 (DL-25…27, ICE recalculated for H-PM-2/H-PM-17) + сверка с 3-м и 4-м живыми интервью 26.08 (DL-28…31, H-PM-1 reopened, H-PM-19 new ICE leader, H-PM-22/23 registered) |
| `Live_interview/DataAnalysts/Interview_DataAnalysts_28_26_Transcript1.md` | **Live transcript** — Вахрушева Т.И., 09.07.2026 |
| `Live_interview/DataAnalysts/Interview_DataAnalysts_28_26_Transcript2_Miniakhmatova.md` | **Live transcript** — Алия Миниахматова, 14.07.2026 |
| `Live_interview/DataAnalysts/Interview_DataAnalysts_28_26_H2_Plekhanova.md` | **Live transcript** — Мария Плеханова, 22.07.2026 *(naming caveat: "H2" here is a transcript; in PD/SW files "H1/H2" means an unexecuted interview guide)* |
| `Live_interview/ProductManagers/Interview_PM_valentin_shmakov.md` | **Live transcript** — Валентин Шмаков, 18.08.2026 (interviewer: Арман Урбисинов) → DL-21…DL-24 |
| `Live_interview/ProductManagers/Interview_PM_dolgova_ksenia_transcript.md` | **Live transcript** — Ксения Долгова, 23.08.2026 (interviewer: Арман Урбисинов) → DL-25…DL-27, 2nd live PM respondent |
| `Live_interview/ProductManagers/Interview_PM_dubkova_nastya.md` | **Live transcript** — Анастасия Дубкова, 26.08.2026 (interviewer: Арман Урбисинов) → DL-28…DL-31, 3rd live PM respondent; portfolio-level Product Owner (two products, 24-person team), not a single-team tactical PM |
| `Live_interview/ProductManagers/Interview_PM_lavrishko_alex.md` | **Live transcript** — Алексей Лаврищенко, 26.08.2026 (interviewer: Арман Урбисинов) → DL-28…DL-31, 4th live PM respondent; tactical PM, legal-entities chat-bot (service track) |
| `Live_interview/ProductManagers/Interview_ProductManagers_28_26_H2_PM_round2.md` | **Current PM interview guide (v4, round 2, 19.08)** — covers both planned interviews: role-mapping block feeding `SKILL/ProductManagers` persona + H-PM-2/H-PM-19 checks + DL-21…24 quantitative gap-fills + short Шмаков follow-up scenario |
| `Live_interview/ProductManagers/Interview_ProductManagers_28_26_H1_PM_final.md` | Superseded PM guide (v3) — replaced by v4 round-2 guide on 19.08 |
| `Live_interview/ProductManagers/Interview_ProductManagers_28_26_H1_PM.md` | Superseded PM guide (v1) — kept for history; executed in adapted form 18.08 |
| `Live_interview/ProductManagers/Interview_ProductManagers_28_26_H1_PM_v2.md` / `_v2_draft.md` | Superseded intermediate guide versions (v2) — current is v3 (`_final`) |
| `roles/ProductManagers/market_reserch_pm/` | **Targeted PM market scan (13.08.2026)** — AI agents across 5 PM functions, RU focus, + `file-references.csv` with sources (closes the "uncited PM market data" gap) |
| `roles/ProductManagers/checkout_hyphothesis_12.08_managers/` | Multi-agent hypothesis checkout for the PM portfolio (12–13.08): independent Claude & Codex passes, cross-reviews, `final_synthesis_pm_12_08.md` verdict |
| `roles/BusinessAnalysts/Hypotheses/Hypotheses_BusinessAnalysts_35_26.md` | **Canonical BA hypothesis registry — consolidated 04.09.2026** (the separate pain-hunt file was merged in, nothing dropped). Opens with a summary table of all 11 hypotheses (status · ICE · live respondents · where the card is); Часть 1/1b = readdressing pass 27.08, Часть 1b2 = Промпт-2 pain hunt 28.08 (H-BA-6…8), Часть 1c = 2nd live interview 02.09 (H-BA-9…11), Часть 2/3 = adjacent and unconfirmed, Часть 4 = weak signals deliberately not turned into hypotheses, Часть 5 = cross-role signals. Original header (27.08.2026) — readdressing pass over the PM registry (H-PM-1…23), not a from-scratch generation: H-BA-1 (draft PRD/CJM/BPMN, was H-PM-4/H-PM-17) + H-BA-2 (VOK/metric-expertise interpretation, was H-PM-1), plus a Part 2 of adjacent unresolved items (H-PM-11, H-PM-23, H-PM-21) and a Part 3 of PM hypotheses with no BA signal. Zero live BA interviews yet — see readdressing-rationale note above |
| `roles/BusinessAnalysts/synthetic_custdev_business_analyst/session_natalya_business_analyst_syntetic_custdev.md` | **Synthetic CustDev, 27.08.2026** — persona «Наталья» (`SKILL/BusinessAnalysts`), first run of this persona. Narrows H-BA-1 (linear pilot step, source-traceability requirement), weakens H-BA-2 for this respondent's process, first BA-side echoes for H-PM-11/H-PM-23 |
| `roles/BusinessAnalysts/synthetic_custdev_business_analyst/session_alexey_business_analyst_syntetic_custdev.md` | **Synthetic CustDev, 28.08.2026** — persona «Алексей» (contrast persona, first run), tests H-BA-1…5. Diverges from «Наталья» on top pain (late-surfacing contradictions → new H-BA-3, not BPMN drawing) and on H-BA-4 (QA does full acceptance); confirms H-BA-2 weak (2nd first-person 🔴 in a row); adds negative baseline: corporate AI assistant already tried on a BRD and failed on contradictions. Both personas' answers embedded in the v2 interview scenario as `SYNT PERSONA ANSWER:` |
| `Live_interview/BusinessAnalysts/Interview_BusinessAnalysts_35_26_Transcript.md` | **Live transcript** — Ольга Серегина, 28.08.2026 (interviewer: Арман Урбисинов) → DL-32…DL-35, 1st live BA respondent; dedicated BA in a CRM/SFA team |
| `Live_interview/BusinessAnalysts/Interview_BusinessAnalysts_35_26_Transcript_2.md` | **Live transcript** — Алексей Трифонов, 02.09.2026 (interviewer: Елизавета Чукреева; Арман Урбисинов also asked) → DL-36…DL-44, 2nd live BA-function respondent; product owner doing the BA job (import-substitution СФА «Юрлиц»), no dedicated BA in his team |
| `roles/BusinessAnalysts/Hypotheses/Hypotheses_BusinessAnalysts_FromLiveInterview_35_26.md` | **Superseded 04.09.2026** — merged into the canonical BA registry above; kept as a stub with a "what moved where" map so existing links keep working. Full pre-merge text is in git history |
| `Live_interview/BusinessAnalysts/Interview_BusinessAnalysts_36_26_H2_BA_round2.md` | **Current BA interview guide (v3, round 2, 04.09.2026)** — 90-min scenario for a deliberately selected 3rd respondent (BA-function on a product that owns a client metric, ideally a from-scratch project). Under every question sit the two live baselines — what Серегина and Трифонов actually answered, with timecodes — instead of synthetic predictions; synthetic personas appear only where no live data exists. Blocks are priority-tagged П1/П2/П3, opens with a screening rule and the two interviewing mistakes to avoid (leading questions that contaminated H-BA-7; letting "nice to have" pass as pain), closes with the post-interview cycle and a table of which hypothesis each answer decides |
| `Live_interview/BusinessAnalysts/Interview_BusinessAnalysts_35_26_H1_BA_v2_synt.md` | **Superseded BA guide (v2, 28.08)** — ran on both live respondents (Серегина 28.08, Трифонов 02.09); kept for history as the record of what the synthetic personas predicted before live data. Original note: — not executed yet; v1 structure + new hypotheses H-BA-3…5 + embedded synthetic predictions from both personas (`SYNT PERSONA ANSWER:` under every question, empty `LIVE ANSWER:` slots) for post-interview comparison; target respondent via snowball (Шмаков or Долгова's team) |
| `Live_interview/BusinessAnalysts/Interview_BusinessAnalysts_35_26_H1_BA.md` | Superseded BA guide (v1, 27.08) — replaced by v2 `_v2_synt` scenario on 28.08; kept for history |
| `Live_interview/ProductDesigners/Interview_ProductDesigners_28_26_H1_PD.md` / `_H2_PD.md` | Interview **guides** for designers (round 1 / round 2) — not executed yet |
| `Live_interview/ScenarioWriters/Interview_Scriptwriters_28_26_H1_SW.md` / `_H2_SW.md` | Interview **guides** for scriptwriters (H-SW-1…16 / H-SW-17…25) — not executed yet |
| `archive/` | Superseded early runs (`Hypotheses_23_26.md`, `Hypotheses_23_26_2.md` — ~85% absorbed into `roles/Hypotheses_AllRoles_23_26.md`) |
| `README.md` | Quick orientation for the repo |

## Using the skill files

Each `skill-*.md` contains a ready-made prompt block (marked with ` ``` `). Copy the prompt, fill in the `{placeholders}`, and paste into Claude. No installation required.

**Bilingual since 28.08.2026:** every skill file carries each section and prompt in both RU and EN. The EN prompt versions follow instructions more precisely — prefer them; they explicitly instruct the model to answer in Russian, so all output (hypothesis wording, personas, DL entries) stays compatible with the Russian-language project files.

`skill-synthetic-custdev.md` works best when you give the persona 3–5 concrete personal details and an explicit pain. If the persona agrees with everything, the role is underspecified — add more friction.

`skill-market-scan.md` requires a tool with web search (Perplexity, Claude with web search, EXA, or Tavily). Without live search, AI will hallucinate market figures.

## Decision Log convention

Entries follow the format `DL-{N}`. Each full entry must include a citation (quote or data point) — entries without evidence are not valid. **Exception:** parked hypotheses (not yet tested) may appear without evidence but must be labeled as untested. Full entries live in `decision-log.md`; after each cycle add/update the one-line row below. Merged entries keep a stub under their old number (e.g. DL-6 → DL-10) so cross-references don't break.

---

## Decision Log Index

*(one line per cycle; full entries with evidence → `decision-log.md`)*

| DL | Hypothesis (short) | Role | Status | Outcome / next step |
|---|---|---|---|---|
| DL-0 | RegExp auto-generation | Scenario writers / Сценаристы чат-ботов | ✅ Shipped | ~30% sprint time recovered (team-lead estimate) |
| DL-1 | Text→SQL multiagent | Data analysts / Аналитики данных | ✅ Shipped | ~20% sprint capacity gained |
| DL-2 | Vibe coding (Kilo Code) → non-technical hires | Scenario writers / Сценаристы чат-ботов | 🔴 Killed | Replacement angle false: catching AI mistakes still requires code understanding |
| DL-2b | Augment (not replace) on script fixes | Scenario writers / Сценаристы чат-ботов | ⏸ Parked | Superseded by DL-3 (diagnosis-only angle) |
| DL-3 | AI script-defect diagnosis (no codegen) | Scenario writers / Сценаристы чат-ботов | 🟡 In progress — stalled | Synthetic-only; live interviews + PoC pending; deadline 14.06 passed; guides ready |
| DL-4 | AI utterance generation for NLU | Scenario writers / Сценаристы чат-ботов | 🟡 In progress — stalled | Synthetic-only; language-quality + domain tests pending; deadline 14.06 passed |
| DL-5 | Dashboard/vitrina draft from requirements | Data analysts / Аналитики данных | 🟡 Open, weakened | Pain real but infrequent (~1×/1–2 mo, 2/2 respondents); reframed "draft survives iteration"; open: sprint share |
| DL-6 | — | — | → DL-10 | Merged (same hypothesis, first respondent) |
| DL-7 | Narrative analysis of metric changes | Data analysts / Аналитики данных | 🔴 Stop (team-specific) | Stakeholders ask for "just numbers" (Вахрушева); other team differs — see DL-15 |
| DL-8 | AI anomaly brief (data-quality case) | Data analysts / Аналитики данных | 🔴 Stop (narrow case) | Rare, self-caught; original metric-alert framing of H-DA-2 still untested |
| DL-9 | Auto-update regular reports | Data analysts / Аналитики данных | 🔴 Stop | Already script-automated — independently confirmed in 2 teams |
| DL-10 | Onboarding knowledge base / SQL library | Data analysts / Аналитики данных | 🔴 Stop (for experienced) | 3/3 experienced analysts: no personal need. Open: real newcomer interview |
| DL-11 | Metric-drop investigation agent | Data analysts / Аналитики данных | 🟡 Pivot | Pain confirmed by 3 sources (1h–days, daily practice); "whole-bank agent" too broad → narrowed in DL-17 |
| DL-12 | AI data-source catalog ("where data lives") | Data analysts / Аналитики данных | 🟡 Team-specific | Миниахматова: «целый вечер» searching; Плеханова: not a pain. Narrow segment before ICE (→ H-DA-14) |
| DL-13 | AI narrative for presentation slides (H-DA-9) | Data analysts / Аналитики данных | 🔴 Stop | First-person disconfirmation (Плеханова): filling slides is fast; bottleneck = approvals + impact calc |
| DL-14 | — | — | → DL-16 | Merged (same hypothesis, first respondent) |
| DL-15 | AI summary after anomaly investigation | Data analysts / Аналитики данных | 🔴 Stop | Write-up takes 5–7 min; bottleneck is the analysis before it (→ DL-17) |
| DL-16 | Jira: task creation + status collection | Data analysts / Аналитики данных | ➗ Split | Split into DL-18 (creation) + DL-19 (statuses) on 23.07 |
| DL-17 | Incident↔request classification | Data analysts / Аналитики данных | 🟡 Pivot | Daily pain, huge volume; blocker: no labeled data → test zero/few-shot on historical incidents |
| DL-18 | Auto-create Jira tasks from customer requests | Data analysts / Аналитики данных | 🟡 Pivot | 3 live respondents (incl. real team lead 23.07 — initially mislogged as synthetic); ЦА likely rank-and-file analysts; split "creation" vs "clarification" time |
| DL-19 | Auto-collect statuses for weekly team report | Data analysts / Аналитики данных (team lead) | 🔨 **In build — MVP in pilot (10.09.2026)** | «Вся пятница» ≈ 8h/wk (n=1); "draft + gaps" scenario confirmed by a 2nd real team lead (Соколова, тимлид ЧБ-1 — Плеханова's team; 23.07, initially mislogged as synthetic); next: 1-sprint draft-report pilot + measure bot-ping response rate. PO working notes 07.08 (Урбисинов): new validation question — awareness vs time (do analysts know native Jira JQL/due-date notifications?). **10.09.2026: moved to build — MVP-1 «Отчёт-бот» built per `MVP_DevPlans_30_26.md` and running as a pilot with a live team; first MVP of the project to reach pilot since DL-0/DL-1. Open: whether the ≈8 h/wk baseline was measured BEFORE the tool was switched on — unconfirmed; without it the pilot can only verdict on workability and ping-response rate, not on time saved** |
| DL-20 | Auto-clustering of requests into incidents (narrowing of DL-17) | Data analysts / Аналитики данных | ⏸ Untested | Formulated 23.07 (Григоренко) to bypass the DL-17 no-labels blocker via unsupervised clustering; no interview/PoC yet. Next: PoC on historical requests → show clusters to Плеханова |
| DL-21 | AI draft of task requirements (H-PM-4) | Product managers / Продакт-менеджеры | 🟡 Pivot | 1st live PM interview (Шмаков, 18.08, via Урбисинов): PRD/CJM written by бизнес-аналитик, not PM → readdress to BA role or narrow to PM's «образ результата» step |
| DL-22 | AI backlog auto-triage (H-PM-12) | Product managers / Продакт-менеджеры | 🔴 Stop (for respondent) | Backlog work ≈ 2h/wk, sprint-rhythm disciplined, «задачи, как правило, не теряются»; don't close role-wide on n=1; open: incoming request volume |
| DL-23 | Proactive metric alerts (H-PM-9) | Product managers / Продакт-менеджеры | 🟡 Pivot | Alerting partially exists (threshold-based BI, not LLM); gap is coverage — next: fact-check % of key metrics covered + ask for a concrete delayed-detection case |
| DL-24 | Metric-drop diagnosis for PM (H-PM-1) | Product managers / Продакт-менеджеры | 🟡 Clarified | Live respondent localizes drops himself via dashboards, but root cause = team/analyst work — refines (doesn't reverse) the synthetic «не та роль» verdict; open: which product Шмаков PMs, time spent on localization |
| DL-25 | Ad-hoc analyst-query structuring (H-PM-2) | Product managers / Продакт-менеджеры | 🔴 Stop (for respondent) | 2nd live PM, first respondent to complete the "5 last requests" block: near-total self-service via existing BI (СС-Pulse), 0 clarification-round cases in 2 weeks; top-ranked PM hypothesis (ICE 216, synthetic-only) gets its first live disconfirmation — not closed role-wide on n=1 |
| DL-26 | Requirements written by BA, not PM; ambiguous business input (H-PM-4/H-PM-17/H-PM-21) | Product managers / Продакт-менеджеры | 🟡 Pivot (strengthened) | 2nd independent live confirmation that detailed requirements are a бизнес-аналитик task, not PM's (repeats DL-21 pattern on a different team); 3rd source overall for H-PM-17 (ambiguous customer/business input → PM requests clarification before sizing) |
| DL-27 | Cross-team status visibility (H-PM-8) | Product managers / Продакт-менеджеры | 🟡 Pivot | Respondent's self-named top pain is inability to influence vendor quality/timing (not AI-fixable); but she already hand-built a per-task Confluence tracker and wants auto stakeholder notifications on status/date slippage — narrows H-PM-8 to that concrete artifact |
| DL-28 | VOK/automation-metric diagnosis reopened (H-PM-1) | Product managers / Продакт-менеджеры | 🟡 Pivot (reopened) | 3rd & 4th live PM respondents both personally burn major time (30 min–half a sprint) interpreting a live VOK-satisfaction drop; internal LLM already tried on this exact task and failed (too generic) — first concrete tech-risk data point for the role. ICE 36→140. Caveat: may be crisis-timing confound, partially conflicts with DL-24 |
| DL-29 | Impact/effort estimation strengthened, master-plan reviewer weakened (H-PM-19 / H-PM-20) | Product managers / Продакт-менеджеры | 🟡 Pivot (strengthened) | First-ever live data for H-PM-19 (was 0 for 3 respondents straight): both new respondents independently name effect/volume estimation as the single hardest part of master-plan work. ICE 168→252. Neither names goal-wording as the bottleneck — H-PM-20 weakens further (4th signal against it) |
| DL-30 | New: self-serve data access for PM, reuse DL-1 (H-PM-22) | Product managers / Продакт-менеджеры | 🟡 New hypothesis | Portfolio-level PM's product analyst overloaded with ad-hoc requests (dashboards unupdated since February); PM explicitly asks to "self-serve" data cuts — cheapest candidate of the cycle since the solution (DL-1 Text-to-SQL) already exists and is validated |
| DL-31 | New: service/system/contact catalog for master-plan scoping (H-PM-23) | Product managers / Продакт-менеджеры | 🟡 New hypothesis | PM names finding the right service/system/contact person as the #2 hardest part of master-plan prep ("could cut prep time nearly in half"); echoes DL-12 (data-source catalog) cross-role, but likely misaddressed to PM — actual doer is the system analyst |
| DL-32 | AI draft PRD/CJM/BRD/user story | Business analyst / Бизнес-аналитик | 🟢 Confirmed (live) | First live BA respondent already does this daily via external LLMs (BRD, user story, clickable prototypes); internal Альфаген tried and found insufficient. ICE recalculated: 9×7×5 = 315 |
| DL-33 | ВОК/metric-expertise interpretation (H-BA-2) | Business analyst / Бизнес-аналитик | 🔴 Stop (for respondent) | Respondent's product (internal CRM/SFA) has no client-facing metrics — team/product-specific disconfirm, not role-wide; next BA respondent must be from a metric-owning product |
| DL-34 | Requirement-contradiction detection (H-BA-3) | Business analyst / Бизнес-аналитик | 🟡 Not confirmed in stated form | Respondent describes AI-assisted consolidation of requirements, not proactive contradiction-pair detection; may need a respondent closer to the «Наталья»/«Алексей» multi-department profile |
| DL-35 | Context-gathering map from disparate sources (H-BA-5) | Business analyst / Бизнес-аналитик | 🟢 Confirmed (live) | Respondent's own unprompted answer to "what hurts most" — manual context-gathering across Confluence/Jira/Abuk. ICE recalculated: 8×8×5 = 320 — top MVP candidate in the BA track by ICE |
| DL-36 | Role mapping: no dedicated BA in import-substitution teams — the PO does the BA job | Business analyst / Бизнес-аналитик | 🟡 Pivot | 2nd live BA-function respondent is a product owner («В команде у меня нет бизнес-аналитика. В командах импорта роль бизнес-аналитика выполняет product»). Track ICP redefined by function (owner of business requirements), not job title — changes how respondents are recruited |
| DL-37 | AI draft of requirements confirmed by a 2nd live respondent (H-BA-1) | Business analyst / Бизнес-аналитик | 🟢 Confirmed (live, n=2) | Independent 2nd confirmation on a different team/product; he generates parts, not the whole BRD template; bought a personal paid transcription subscription. **Key finding:** an internal AI agent for system analysts already integrates with Confluence + Git — first live precedent of a passed integration/ИБ gate in the project. ICE 315 → 432 (9×8×6) |
| DL-38 | Context gathering confirmed + first quantitative anchor (H-BA-5) | Business analyst / Бизнес-аналитик | 🟢 Confirmed (live, n=2) | 4 context sources named unprompted (Confluence → test env → stakeholders → Rocket.Chat publics); «месяц-полтора» for the whole business-analysis phase closes DL-35's open number. **Ceiling found:** a large share of context exists in no document at all — retrieval can't reach it. ICE 320 → 360 (8×9×5) |
| DL-39 | H-BA-3 unconfirmed twice → pivot to H-BA-11 (clarifying questions / gap detection) | Business analyst / Бизнес-аналитик | 🟡 Pivot → new hypothesis | Contradictions are resolved by negotiation, not text analysis; the late-conflict scenario is organisational, not textual. But 2 of 2 live respondents want (one already does) AI-generated clarifying questions and uncovered-area lists. **H-BA-11 ICE = 7×9×8 = 504 — new track leader and the only candidate needing no integrations.** H-BA-3 in its original form is a stop candidate |
| DL-40 | Business acceptance (H-BA-4) confirmed live for the first time | Business analyst / Бизнес-аналитик | 🟡 Pivot | BA-function does acceptance even with 2 dedicated QAs — «Алексей» synthetic moderator disproven, «Наталья» closer. Finds defects by fresh eye, not by spec comparison; asks for an agent that clicks through cases. **Blocker: the BRD is never updated — nothing to compare against (see DL-43).** First ICE 6×5×3 = 90 |
| DL-41 | BPMN auto-drawing (H-BA-6) segmented + negative tech baseline | Business analyst / Бизнес-аналитик | 🟡 Pivot | Needed only on from-scratch/new processes, not on rework; AI already tried on this task and fails («пока с [BPMN] нам [ИИ] не дружат. Либо какую-то фигню рисуют»). No compensatory behaviour → "nice to have". ICE 5×6×3 = 90; if ever scoped, generate machine-readable notation, not a picture |
| DL-42 | H-BA-7 pivot: the driver is integration, not security; H-BA-8 promoted | Business analyst / Бизнес-аналитик | 🟡 Pivot | No ИБ pain for this respondent (no confidential data) — diverging signal at n=2; but he names Confluence integration as the reason an internal tool would win. 2nd independent live evidence of Альфаген failing (3rd in the project). H-BA-8 (publish to Confluence) promoted from quick win to a mandatory MVP element. H-BA-7 ICE 5×4×4 = 80 |
| DL-43 | New: incremental BRD updating from the stream of clarifications (H-BA-10) | Business analyst / Бизнес-аналитик | 🟡 New hypothesis | Respondent admits he skips work he considers mandatory — «их надо обновлять. И я этого не делаю»; clarifications arrive «100%… постоянно». 2nd independent appearance of the "docs go stale" pattern in the BA track (1st: Серегина's system analyst, ~800 edits). Blocks H-BA-4. ICE 7×6×5 = 210 |
| DL-44 | H-BA-2 disconfirmed a 2nd time in first person; new H-BA-9 (anomaly alerts) | Business analyst / Бизнес-аналитик | 🔴 / 🟡 New hypothesis | 2 of 2 live BA-function respondents work on internal systems with no client metrics; H-BA-2 gets one last shot on a deliberately selected metric-owning respondent before closing role-wide. New H-BA-9 (proactive metric-anomaly alerts, ICE 5×5×5 = 125) — merge with H-PM-9 and DL-8 as one cross-role hypothesis rather than three cards |
