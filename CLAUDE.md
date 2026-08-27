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
| Data analysts (DL-1 team + 2 more teams) | **Have access**, incl. live тимлид contact (Соколова, ЧБ-1) since 23.07 | 3 live interviews done (Вахрушева 09.07, Миниахматова 14.07, Плеханова 22.07) + live talk with тимлид ЧБ-1 (Соколова 23.07) → cycles DL-5…DL-20. Strongest surviving: DL-19, DL-18 (Jira automation), DL-17 + its untested narrowing DL-20 (clustering). Most narrative/report hypotheses killed. DL-5 open but weakened. OST built 07.08 (`OST_DataAnalysts_28_26.md`) | **#1** |
| Chatbot scenario writers | **Have access** | DL-3/DL-4 stalled at synthetic stage (deadline 14.06 passed, no live interviews yet; guides ready). Product-data track: 12-case registry → H-SW-17…25 (23.07) + revised H-SW-26…52 (27.07, Григоренко: dedup vs in-flight case initiatives, augment-framing enforced). Cursor pilot (May–June, 5 scriptwriters) has no recorded results | **#2** |
| Product designers | **Have access (via developer contact Николай Шубич, since 14.07.2026)** | H-PD-3/5 confirmed & in development by the developer; H-PD-4 pain confirmed but already covered by an existing tool (Clade) — not being built. Zero live interviews with a designer themselves; round-2 guide ready | **#3** |
| Product managers | **Live contact established** — 4 live interviews done: Валентин Шмаков 18.08, Ксения Долгова 23.08, Анастасия Дубкова + Алексей Лаврищенко 26.08 (interviewer Арман Урбисинов) | 11 live-evidence cycles DL-21…DL-31: H-PM-4 → wrong role (PRD written by бизнес-аналитик, confirmed independently **three** times), H-PM-12 killed for respondent (reinforced 26.08), H-PM-9 partial (BI config, not LLM), **H-PM-2 (was top-ranked, ICE 216) weakening on 3 of 4 live respondents** (near-total BI self-service / no clarification-round friction), H-PM-17 strengthened, H-PM-8 narrowed to a status-notification artifact. **26.08: H-PM-1 (VOK diagnosis) reopened** — 2 new respondents personally burn major time on it, internal LLM already tried and failed on this exact task; **H-PM-19 (impact estimation) gets its first live data and jumps to new #1 by ICE (252)** — named the single hardest part of master-plan work by both new respondents; **2 new hypotheses registered** (H-PM-22 self-serve data access reusing shipped DL-1, H-PM-23 service/contact catalog echoing DL-12) | **#4** |
| *Бизнес-аналитик (spawn из DL-21, 19.08; readdressed 27.08)* | No live contact yet — snowball via Шмаков/Долгова planned | Hypotheses reused from the PM registry (`Hypotheses_BusinessAnalysts_35_26.md`, 27.08.2026 — see note below for why); readdressed set now H-BA-1 (was H-PM-4/H-PM-17) + H-BA-2 (was H-PM-1). First synthetic CustDev run 27.08.2026 (persona «Наталья», `SKILL/business_analyst`) — narrows H-BA-1 to a linear pilot step + source-traceability requirement, weakens H-BA-2 for this persona's process (lead-transfer, not a regular VOK-style metric), gets first BA-side echoes for H-PM-11 (spec verification) and H-PM-23 (contact catalog). Interview guide ready; zero live BA interviews still | — |

> **Note:** "Chatbot scriptwriters" and "scenario writers" are the same role — one person writes both JS scripts and NLU training data (intents, utterances, RegExp). DL-3 and DL-4 both target this role.

> **Note (updated 14.07.2026):** Product designer access is resolved — reached through a developer (Николай Шубич) who is already building AI tools for that role. ~~Product manager access is still unresolved~~ — **superseded 18.08.2026:** PM access resolved — Арман Урбисинов conducted the first live PM interview (Валентин Шмаков) → DL-21…DL-24.

*Ranking logic: access is the binding constraint at <1 year tenure. Data analysts and scriptwriters have existing relationships and can be interviewed now. **⚠️ The #3-vs-#4 ordering premise is now obsolete (19.08.2026):** designers ranked above PMs because PM access was zero — but PMs now have a live interview while designers still have none. Revisit the order on the next ranking pass: PM evidence is live but mostly disconfirming (DL-22 killed, DL-21/24 point to adjacent roles), while designer evidence is confirmed-but-secondhand.*

> **Note (27.08.2026) — Business Analyst track reuses the PM hypothesis registry, not a fresh generation:** `Hypotheses_BusinessAnalysts_35_26.md` readdresses the existing PM registry (`Hypotheses_ProductManagers_28_26.md`, H-PM-1…23) instead of generating candidates from scratch. Reason: bank-specific role mapping. Across three independent live PM interviews (Шмаков DL-21, Долгова DL-26, Лаврищенко 26.08) ownership of detailed requirements — PRD, CJM, BPMN — consistently landed on the **бизнес-аналитик**, not the PM. In this bank, the БА role is functionally closer to the *original* candidate-role thesis behind the PM hypotheses (owns requirements, CJM, task framing) than the PM role turned out to be in practice — PM reads more as a coordination/prioritization role (see DL-21/DL-26/DL-28 and the #3-vs-#4 ordering note above). First synthetic CustDev for this track ran 27.08.2026 (`roles/business_analyst/synthetic_custdev_buisnessanalyst/session_natalya_business_analyst_syntetic_custdev.md`); interview guide for the first live BA respondent is ready (`roles/business_analyst/Interview_BusinessAnalysts_35_26_H1_BA.md`).

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
- **Build phase:** dev plans for DL-19/DL-18/DL-17 are ready in `MVP_DevPlans_30_26.md` — start with week-0 tasks: pre-commit 🟢/🟡/🔴 criteria into the DL entries, reuse checks (Jira Automation / Mail Handler / АльфаГен), ИБ pre-consultation via Шубич's precedent, first baseline Friday.
- **DL-18/DL-19 (Jira automation, analysts):** interviews with rank-and-file analysts with split time questions (creation vs clarification); quantitative Jira checks (delay between request and task creation; status staleness); 1-sprint draft-report pilot for DL-19.
- **DL-17 (incident classification):** narrow to zero/few-shot classification on historical incidents (no labeled data exists); ask scriptwriters their side of the consultation load.
- **DL-5 (dashboards):** 2–4 more DL-1-team interviews in "draft, not final" scope + fix the sprint-share question; PoC on historical requirement sets; evaluate Visiology Cortex as build-vs-buy.
- **DL-3/DL-4 (scriptwriters):** execute the ready interview guides (`Interview_Scriptwriters_28_26_H1_SW.md` / `_H2_SW.md`); record Cursor pilot results if the pilot ran (`Cases_Scriptwriters_28_26.md`).
- **Designers:** live interview with an actual designer via Шубич (guide: `Interview_ProductDesigners_28_26_H2_PD.md`); clarify tool boundaries with Шубич (H-PD-11/H-PD-14 vs his H-PD-3/5).
- **Product managers (updated 26.08):** 3rd and 4th live interviews done (Дубкова + Лаврищенко, 26.08 → DL-28…31). H-PM-2 (former top-rank, ICE 216) keeps weakening — 3 of 4 live respondents show no PM-side clarification friction; H-PM-19 (impact estimation) finally gets live data and becomes the new ICE leader (252) — both new respondents independently call effect/volume estimation the hardest part of master-plan work; H-PM-1 (VOK diagnosis) reopens on 2 new respondents personally burning heavy time on a live VOK-drop crisis, with a first concrete tech-risk data point (internal LLM already tried on this exact task, failed — too generic); 2 new hypotheses registered (H-PM-22 self-serve data access reusing shipped DL-1; H-PM-23 service/contact catalog echoing DL-12, likely misaddressed to system analyst). Still open across all 4 live respondents: hours on «образ результата» (DL-21/H-PM-21); the cross-role ИБ-turnaround question, never asked live of any role in 4 interviews; whether Дубкова and Лаврищенко sit in the same reporting line (unconfirmed org link, see registry sverka). Next: technical fact-check with the DL-1 owner on H-PM-22 feasibility (cheap, no interview needed); ask VOK-crisis frequency outside the current peak in the next PM interview before trusting H-PM-1's new ICE. Use the round-2 guide (`roles/ProductManagers/Hypotheses/Interview_ProductManagers_28_26_H2_PM_round2.md`).
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

One full cycle is ~3 hours. The loop is closed when the full entry lives in `decision-log.md` **and** its index row lives here.

## Files and their roles

| File | Role |
|---|---|
| `CLAUDE.md` | This file — product context, strategy, Decision Log Index |
| `decision-log.md` | **Canonical Decision Log** — full DL-0…DL-27 entries with evidence |
| `MVP_DevPlans_30_26.md` | Dev plans for the three build candidates (25.07.2026): Отчёт-бот (DL-19), Задача-бот (DL-18), offline classification PoC (DL-17); updated 12.08 with DL-19 working notes |
| `OST_DataAnalysts_28_26.md` | Opportunity Solution Tree (07.08.2026) for the data-analyst hypothesis family — DL-19/DL-18/DL-17/DL-5 under one business goal, with rejected solution alternatives per branch |
| `tasks_dl19/` | DL-19 build-task breakdown (12.08, Урбисинов) |
| `HypothesisBacklog.md` / `HypothesisBacklog_v2.md` | Cross-role ICE scoreboard (13–14.08.2026) — flat non-canonical view over all `Hypotheses_*` files + decision log; canon stays in `decision-log.md` |
| `CLAUDE_template.md` | Product context template — fill in per product, rename to `CLAUDE.md` |
| `skill-hypothesis-generating.md` | Generates hypothesis candidates from 3 sources (market, CustDev, product data) |
| `skill-hypothesis-check.md` | Structures a raw idea into a testable hypothesis + ICE (I·C·A, 1–10) + go/pivot/stop criteria |
| `skill-synthetic-custdev.md` | Turns Claude into a specific ICP persona for a practice interview session |
| `skill-market-scan.md` | Produces a structured market report: TAM, players, trends, gaps — all with sources |
| `skill-decision-log.md` | Template for recording what was tested, what was learned, and the next step |
| `SKILL/` (`analyst`, `scriptwriters`, `PD`, `PM`, `zakazchik`) | Pre-filled synthetic-CustDev persona prompts per role. `PM` re-calibrated 19.08 on live DL-21…24 facts (cost-center commitment questions, no purchase framing); `zakazchik` — first demand-side persona (19.08). ⚠️ `analyst` still has an unfilled placeholder |
| `roles/ProductManagers/synthetic_custdev_19_08/` | Synthetic-CustDev session transcripts 19.08 (PM «Игорь», заказчик «Марина») testing H-PM-17…21 — first synthetic sessions persisted to the repo |
| `roles/` | **Per-role workspaces (restructured 19.08.2026)** — hypothesis packs, guides, and transcripts now live under `roles/<Role>/` |
| `roles/Hypotheses_AllRoles_23_26.md` | June canonical run — data analysts + scenario writers, 20 hypotheses. ⚠️ Statuses frozen at 09.06; current verdicts in `decision-log.md`. H-DA-3/H-DA-9 diverged from the July files — see its header note |
| `roles/DataAnalysts/Hypotheses_DataAnalysts_28_26.md` | July hypothesis-check pass for analysts (H-DA-11…14 line; updated 23.07 with DL-7/10/13 verdicts) |
| `roles/scriptwriters/Hypotheses_Scriptwriters_28_26.md` | July pass, H-SW-1…16 (market + vision + synthetic CustDev) + revised H-SW-26…52 addendum (27.07, Григоренко) |
| `roles/scriptwriters/Cases_Scriptwriters_28_26.md` | Raw product-data case registry from the team's product owner (12 cases + effort metrics + Cursor pilot plan), 23.07 |
| `roles/scriptwriters/Hypotheses_Scriptwriters_FromCases_28_26.md` | H-SW-17…25 derived from the case registry (pre-ICE, metrics pending) |
| `roles/ProductDesigners/Hypotheses_ProductDesigners_28_26.md` | July pass, H-PD-1…15; includes the Developer Status Report (Шубич, 14.07) |
| `roles/ProductManagers/Hypotheses/Hypotheses_ProductManagers_28_26.md` | **Canonical PM hypothesis registry.** July pass H-PM-1…13 (synthetic + market) + сверка с живым интервью 18.08 (DL-21…24) + регистрация арены H-PM-14…16 + новая генерация H-PM-17…21 и повестка второго интервью (19.08) + сверка со 2-м живым интервью 23.08 (DL-25…27, ICE recalculated for H-PM-2/H-PM-17) + сверка с 3-м и 4-м живыми интервью 26.08 (DL-28…31, H-PM-1 reopened, H-PM-19 new ICE leader, H-PM-22/23 registered) |
| `roles/DataAnalysts/Interview_DataAnalysts_28_26_Transcript1.md` | **Live transcript** — Вахрушева Т.И., 09.07.2026 |
| `roles/DataAnalysts/Interview_DataAnalysts_28_26_Transcript2_Miniakhmatova.md` | **Live transcript** — Алия Миниахматова, 14.07.2026 |
| `roles/DataAnalysts/Interview_DataAnalysts_28_26_H2_Plekhanova.md` | **Live transcript** — Мария Плеханова, 22.07.2026 *(naming caveat: "H2" here is a transcript; in PD/SW files "H1/H2" means an unexecuted interview guide)* |
| `roles/ProductManagers/Hypotheses/Interview_PM_valentin_shmakov.md` | **Live transcript** — Валентин Шмаков, 18.08.2026 (interviewer: Арман Урбисинов) → DL-21…DL-24 |
| `roles/ProductManagers/Hypotheses/Interview_PM_dolgova_ksenia_transcript.md` | **Live transcript** — Ксения Долгова, 23.08.2026 (interviewer: Арман Урбисинов) → DL-25…DL-27, 2nd live PM respondent |
| `roles/ProductManagers/Hypotheses/Interview_PM_dubkova_nastya.md` | **Live transcript** — Анастасия Дубкова, 26.08.2026 (interviewer: Арман Урбисинов) → DL-28…DL-31, 3rd live PM respondent; portfolio-level Product Owner (two products, 24-person team), not a single-team tactical PM |
| `roles/ProductManagers/Hypotheses/Interview_PM_lavrishko_alex.md` | **Live transcript** — Алексей Лаврищенко, 26.08.2026 (interviewer: Арман Урбисинов) → DL-28…DL-31, 4th live PM respondent; tactical PM, legal-entities chat-bot (service track) |
| `roles/ProductManagers/Hypotheses/Interview_ProductManagers_28_26_H2_PM_round2.md` | **Current PM interview guide (v4, round 2, 19.08)** — covers both planned interviews: role-mapping block feeding `SKILL/PM` persona + H-PM-2/H-PM-19 checks + DL-21…24 quantitative gap-fills + short Шмаков follow-up scenario |
| `roles/ProductManagers/Hypotheses/Interview_ProductManagers_28_26_H1_PM_final.md` | Superseded PM guide (v3) — replaced by v4 round-2 guide on 19.08 |
| `roles/ProductManagers/Hypotheses/Interview_ProductManagers_28_26_H1_PM.md` | Superseded PM guide (v1) — kept for history; executed in adapted form 18.08 |
| `roles/ProductManagers/Hypotheses/Interview_ProductManagers_28_26_H1_PM_v2.md` / `_v2_draft.md` | Superseded intermediate guide versions (v2) — current is v3 (`_final`) |
| `roles/ProductManagers/market_reserch_pm/` | **Targeted PM market scan (13.08.2026)** — AI agents across 5 PM functions, RU focus, + `file-references.csv` with sources (closes the "uncited PM market data" gap) |
| `roles/ProductManagers/checkout_hyphothesis_12.08_managers/` | Multi-agent hypothesis checkout for the PM portfolio (12–13.08): independent Claude & Codex passes, cross-reviews, `final_synthesis_pm_12_08.md` verdict |
| `roles/business_analyst/hyphotheses/Hypotheses_BusinessAnalysts_35_26.md` | **BA hypothesis registry (27.08.2026)** — readdressing pass over the PM registry (H-PM-1…23), not a from-scratch generation: H-BA-1 (draft PRD/CJM/BPMN, was H-PM-4/H-PM-17) + H-BA-2 (VOK/metric-expertise interpretation, was H-PM-1), plus a Part 2 of adjacent unresolved items (H-PM-11, H-PM-23, H-PM-21) and a Part 3 of PM hypotheses with no BA signal. Zero live BA interviews yet — see readdressing-rationale note above |
| `roles/business_analyst/synthetic_custdev_buisnessanalyst/session_natalya_business_analyst_syntetic_custdev.md` | **Synthetic CustDev, 27.08.2026** — persona «Наталья» (`SKILL/business_analyst`), first run of this persona. Narrows H-BA-1 (linear pilot step, source-traceability requirement), weakens H-BA-2 for this respondent's process, first BA-side echoes for H-PM-11/H-PM-23 |
| `roles/business_analyst/Interview_BusinessAnalysts_35_26_H1_BA.md` | **BA interview guide (v1, 27.08.2026)** — not executed yet; role-mapping block + H-BA-1/H-BA-2 behavioral questions + adjacent Part-2 items + ИБ block; target respondent via snowball (Шмаков or Долгова's team) |
| `roles/ProductDesigners/Interview_ProductDesigners_28_26_H1_PD.md` / `_H2_PD.md` | Interview **guides** for designers (round 1 / round 2) — not executed yet |
| `roles/scriptwriters/Interview_Scriptwriters_28_26_H1_SW.md` / `_H2_SW.md` | Interview **guides** for scriptwriters (H-SW-1…16 / H-SW-17…25) — not executed yet |
| `archive/` | Superseded early runs (`Hypotheses_23_26.md`, `Hypotheses_23_26_2.md` — ~85% absorbed into `roles/Hypotheses_AllRoles_23_26.md`) |
| `README.md` | Quick orientation for the repo |

## Using the skill files

Each `skill-*.md` contains a ready-made prompt block (marked with ` ``` `). Copy the prompt, fill in the `{placeholders}`, and paste into Claude. No installation required.

`skill-synthetic-custdev.md` works best when you give the persona 3–5 concrete personal details and an explicit pain. If the persona agrees with everything, the role is underspecified — add more friction.

`skill-market-scan.md` requires a tool with web search (Perplexity, Claude with web search, EXA, or Tavily). Without live search, AI will hallucinate market figures.

## Decision Log convention

Entries follow the format `DL-{N}`. Each full entry must include a citation (quote or data point) — entries without evidence are not valid. **Exception:** parked hypotheses (not yet tested) may appear without evidence but must be labeled as untested. Full entries live in `decision-log.md`; after each cycle add/update the one-line row below. Merged entries keep a stub under their old number (e.g. DL-6 → DL-10) so cross-references don't break.

---

## Decision Log Index

*(one line per cycle; full entries with evidence → `decision-log.md`)*

| DL | Hypothesis (short) | Role | Status | Outcome / next step |
|---|---|---|---|---|
| DL-0 | RegExp auto-generation | Scenario writers | ✅ Shipped | ~30% sprint time recovered (team-lead estimate) |
| DL-1 | Text→SQL multiagent | Data analysts | ✅ Shipped | ~20% sprint capacity gained |
| DL-2 | Vibe coding (Kilo Code) → non-technical hires | Scriptwriters | 🔴 Killed | Replacement angle false: catching AI mistakes still requires code understanding |
| DL-2b | Augment (not replace) on script fixes | Scriptwriters | ⏸ Parked | Superseded by DL-3 (diagnosis-only angle) |
| DL-3 | AI script-defect diagnosis (no codegen) | Scriptwriters | 🟡 In progress — stalled | Synthetic-only; live interviews + PoC pending; deadline 14.06 passed; guides ready |
| DL-4 | AI utterance generation for NLU | Scriptwriters | 🟡 In progress — stalled | Synthetic-only; language-quality + domain tests pending; deadline 14.06 passed |
| DL-5 | Dashboard/vitrina draft from requirements | Data analysts | 🟡 Open, weakened | Pain real but infrequent (~1×/1–2 mo, 2/2 respondents); reframed "draft survives iteration"; open: sprint share |
| DL-6 | — | — | → DL-10 | Merged (same hypothesis, first respondent) |
| DL-7 | Narrative analysis of metric changes | Data analysts | 🔴 Stop (team-specific) | Stakeholders ask for "just numbers" (Вахрушева); other team differs — see DL-15 |
| DL-8 | AI anomaly brief (data-quality case) | Data analysts | 🔴 Stop (narrow case) | Rare, self-caught; original metric-alert framing of H-DA-2 still untested |
| DL-9 | Auto-update regular reports | Data analysts | 🔴 Stop | Already script-automated — independently confirmed in 2 teams |
| DL-10 | Onboarding knowledge base / SQL library | Data analysts | 🔴 Stop (for experienced) | 3/3 experienced analysts: no personal need. Open: real newcomer interview |
| DL-11 | Metric-drop investigation agent | Data analysts | 🟡 Pivot | Pain confirmed by 3 sources (1h–days, daily practice); "whole-bank agent" too broad → narrowed in DL-17 |
| DL-12 | AI data-source catalog ("where data lives") | Data analysts | 🟡 Team-specific | Миниахматова: «целый вечер» searching; Плеханова: not a pain. Narrow segment before ICE (→ H-DA-14) |
| DL-13 | AI narrative for presentation slides (H-DA-9) | Data analysts | 🔴 Stop | First-person disconfirmation (Плеханова): filling slides is fast; bottleneck = approvals + impact calc |
| DL-14 | — | — | → DL-16 | Merged (same hypothesis, first respondent) |
| DL-15 | AI summary after anomaly investigation | Data analysts | 🔴 Stop | Write-up takes 5–7 min; bottleneck is the analysis before it (→ DL-17) |
| DL-16 | Jira: task creation + status collection | Data analysts | ➗ Split | Split into DL-18 (creation) + DL-19 (statuses) on 23.07 |
| DL-17 | Incident↔request classification | Data analysts | 🟡 Pivot | Daily pain, huge volume; blocker: no labeled data → test zero/few-shot on historical incidents |
| DL-18 | Auto-create Jira tasks from customer requests | Data analysts | 🟡 Pivot | 3 live respondents (incl. real team lead 23.07 — initially mislogged as synthetic); ЦА likely rank-and-file analysts; split "creation" vs "clarification" time |
| DL-19 | Auto-collect statuses for weekly team report | Data analysts (team lead) | 🟡 Pivot | «Вся пятница» ≈ 8h/wk (n=1); "draft + gaps" scenario confirmed by a 2nd real team lead (Соколова, тимлид ЧБ-1 — Плеханова's team; 23.07, initially mislogged as synthetic); next: 1-sprint draft-report pilot + measure bot-ping response rate. PO working notes 07.08 (Урбисинов): new validation question — awareness vs time (do analysts know native Jira JQL/due-date notifications?) |
| DL-20 | Auto-clustering of requests into incidents (narrowing of DL-17) | Data analysts | ⏸ Untested | Formulated 23.07 (Григоренко) to bypass the DL-17 no-labels blocker via unsupervised clustering; no interview/PoC yet. Next: PoC on historical requests → show clusters to Плеханова |
| DL-21 | AI draft of task requirements (H-PM-4) | Product managers | 🟡 Pivot | 1st live PM interview (Шмаков, 18.08, via Урбисинов): PRD/CJM written by бизнес-аналитик, not PM → readdress to BA role or narrow to PM's «образ результата» step |
| DL-22 | AI backlog auto-triage (H-PM-12) | Product managers | 🔴 Stop (for respondent) | Backlog work ≈ 2h/wk, sprint-rhythm disciplined, «задачи, как правило, не теряются»; don't close role-wide on n=1; open: incoming request volume |
| DL-23 | Proactive metric alerts (H-PM-9) | Product managers | 🟡 Pivot | Alerting partially exists (threshold-based BI, not LLM); gap is coverage — next: fact-check % of key metrics covered + ask for a concrete delayed-detection case |
| DL-24 | Metric-drop diagnosis for PM (H-PM-1) | Product managers | 🟡 Clarified | Live respondent localizes drops himself via dashboards, but root cause = team/analyst work — refines (doesn't reverse) the synthetic «не та роль» verdict; open: which product Шмаков PMs, time spent on localization |
| DL-25 | Ad-hoc analyst-query structuring (H-PM-2) | Product managers | 🔴 Stop (for respondent) | 2nd live PM, first respondent to complete the "5 last requests" block: near-total self-service via existing BI (СС-Pulse), 0 clarification-round cases in 2 weeks; top-ranked PM hypothesis (ICE 216, synthetic-only) gets its first live disconfirmation — not closed role-wide on n=1 |
| DL-26 | Requirements written by BA, not PM; ambiguous business input (H-PM-4/H-PM-17/H-PM-21) | Product managers | 🟡 Pivot (strengthened) | 2nd independent live confirmation that detailed requirements are a бизнес-аналитик task, not PM's (repeats DL-21 pattern on a different team); 3rd source overall for H-PM-17 (ambiguous customer/business input → PM requests clarification before sizing) |
| DL-27 | Cross-team status visibility (H-PM-8) | Product managers | 🟡 Pivot | Respondent's self-named top pain is inability to influence vendor quality/timing (not AI-fixable); but she already hand-built a per-task Confluence tracker and wants auto stakeholder notifications on status/date slippage — narrows H-PM-8 to that concrete artifact |
| DL-28 | VOK/automation-metric diagnosis reopened (H-PM-1) | Product managers | 🟡 Pivot (reopened) | 3rd & 4th live PM respondents both personally burn major time (30 min–half a sprint) interpreting a live VOK-satisfaction drop; internal LLM already tried on this exact task and failed (too generic) — first concrete tech-risk data point for the role. ICE 36→140. Caveat: may be crisis-timing confound, partially conflicts with DL-24 |
| DL-29 | Impact/effort estimation strengthened, master-plan reviewer weakened (H-PM-19 / H-PM-20) | Product managers | 🟡 Pivot (strengthened) | First-ever live data for H-PM-19 (was 0 for 3 respondents straight): both new respondents independently name effect/volume estimation as the single hardest part of master-plan work. ICE 168→252. Neither names goal-wording as the bottleneck — H-PM-20 weakens further (4th signal against it) |
| DL-30 | New: self-serve data access for PM, reuse DL-1 (H-PM-22) | Product managers | 🟡 New hypothesis | Portfolio-level PM's product analyst overloaded with ad-hoc requests (dashboards unupdated since February); PM explicitly asks to "self-serve" data cuts — cheapest candidate of the cycle since the solution (DL-1 Text-to-SQL) already exists and is validated |
| DL-31 | New: service/system/contact catalog for master-plan scoping (H-PM-23) | Product managers | 🟡 New hypothesis | PM names finding the right service/system/contact person as the #2 hardest part of master-plan prep ("could cut prep time nearly in half"); echoes DL-12 (data-source catalog) cross-role, but likely misaddressed to PM — actual doer is the system analyst |
