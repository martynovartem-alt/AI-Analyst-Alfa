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
- **Team:** Product owner (me, prompt/low-code) + 1–2 developers (dedicated full-time)
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

**Candidate roles — ranked by evidence × access (updated 23.07.2026):**

| Role | Access | Evidence status (see Decision Log Index for verdicts) | Rank |
|---|---|---|---|
| Data analysts (DL-1 team + 2 more teams) | **Have access**, incl. live тимлид contact (Соколова, ЧБ-1) since 23.07 | 3 live interviews done (Вахрушева 09.07, Миниахматова 14.07, Плеханова 22.07) + live talk with тимлид ЧБ-1 (Соколова 23.07) → cycles DL-5…DL-19. Strongest surviving: DL-19, DL-18 (Jira automation), DL-17, DL-11 (incident/anomaly investigation). Most narrative/report hypotheses killed. DL-5 open but weakened (low frequency, 2/2 respondents) | **#1** |
| Chatbot scenario writers | **Have access** | DL-3/DL-4 stalled at synthetic stage (deadline 14.06 passed, no live interviews yet; guides ready). New product-data track 23.07: 12-case registry → H-SW-17…25. Cursor pilot (May–June, 5 scriptwriters) has no recorded results | **#2** |
| Product designers | **Have access (via developer contact Николай Шубич, since 14.07.2026)** | H-PD-3/5 confirmed & in development by the developer; H-PD-4 pain confirmed but already covered by an existing tool (Clade) — not being built. Zero live interviews with a designer themselves; round-2 guide ready | **#3** |
| Product managers | No live contact secured | Synthetic CustDev + market-scan rounds (10.07, 20.07) only; H1 interview guide ready; blocked on a warm intro | **#4** |

> **Note:** "Chatbot scriptwriters" and "scenario writers" are the same role — one person writes both JS scripts and NLU training data (intents, utterances, RegExp). DL-3 and DL-4 both target this role.

> **Note (updated 14.07.2026):** Product designer access is resolved — reached through a developer (Николай Шубич) who is already building AI tools for that role. Product manager access is still unresolved despite repeated market-sourced hypothesis-generation rounds — market research alone doesn't substitute for a live contact.

*Ranking logic: access is the binding constraint at <1 year tenure. Data analysts and scriptwriters have existing relationships and can be interviewed now. Product designers sit above product managers (14.07.2026) — designer access resolved via a developer contact, while product manager access remains at zero live contact despite equal or greater market-research effort.*

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

**→ Next actions (updated 25.07.2026; full criteria per entry in `decision-log.md`):**
- **Build phase:** dev plans for DL-19/DL-18/DL-17 are ready in `MVP_DevPlans_30_26.md` — start with week-0 tasks: pre-commit 🟢/🟡/🔴 criteria into the DL entries, reuse checks (Jira Automation / Mail Handler / АльфаГен), ИБ pre-consultation via Шубич's precedent, first baseline Friday.
- **DL-18/DL-19 (Jira automation, analysts):** interviews with rank-and-file analysts with split time questions (creation vs clarification); quantitative Jira checks (delay between request and task creation; status staleness); 1-sprint draft-report pilot for DL-19.
- **DL-17 (incident classification):** narrow to zero/few-shot classification on historical incidents (no labeled data exists); ask scriptwriters their side of the consultation load.
- **DL-5 (dashboards):** 2–4 more DL-1-team interviews in "draft, not final" scope + fix the sprint-share question; PoC on historical requirement sets; evaluate Visiology Cortex as build-vs-buy.
- **DL-3/DL-4 (scriptwriters):** execute the ready interview guides (`Interview_Scriptwriters_28_26_H1_SW.md` / `_H2_SW.md`); record Cursor pilot results if the pilot ran (`Cases_Scriptwriters_28_26.md`).
- **Designers:** live interview with an actual designer via Шубич (guide: `Interview_ProductDesigners_28_26_H2_PD.md`); clarify tool boundaries with Шубич (H-PD-11/H-PD-14 vs his H-PD-3/5).
- **Product managers:** still blocked on a warm intro before any live signal (guide ready: `Interview_ProductManagers_28_26_H1_PM.md`).
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
| `decision-log.md` | **Canonical Decision Log** — full DL-0…DL-19 entries with evidence |
| `MVP_DevPlans_30_26.md` | Dev plans for the three build candidates (25.07.2026): Отчёт-бот (DL-19), Задача-бот (DL-18), offline classification PoC (DL-17) |
| `CLAUDE_template.md` | Product context template — fill in per product, rename to `CLAUDE.md` |
| `skill-hypothesis-generating.md` | Generates hypothesis candidates from 3 sources (market, CustDev, product data) |
| `skill-hypothesis-check.md` | Structures a raw idea into a testable hypothesis + ICE (I·C·A, 1–10) + go/pivot/stop criteria |
| `skill-synthetic-custdev.md` | Turns Claude into a specific ICP persona for a practice interview session |
| `skill-market-scan.md` | Produces a structured market report: TAM, players, trends, gaps — all with sources |
| `skill-decision-log.md` | Template for recording what was tested, what was learned, and the next step |
| `SKILL/` (`analyst`, `scriptwriters`, `PD`, `PM`) | Pre-filled synthetic-CustDev persona prompts per role |
| `Hypotheses_AllRoles_23_26.md` | June canonical run — data analysts + scenario writers, 20 hypotheses. ⚠️ Statuses frozen at 09.06; current verdicts in `decision-log.md`. H-DA-3/H-DA-9 diverged from the July files — see its header note |
| `Hypotheses_DataAnalysts_28_26.md` | July hypothesis-check pass for analysts (H-DA-11…14 line; updated 23.07 with DL-7/10/13 verdicts) |
| `Hypotheses_Scriptwriters_28_26.md` | July pass for scriptwriters, H-SW-1…16 (market + vision + synthetic CustDev) |
| `Cases_Scriptwriters_28_26.md` | Raw product-data case registry from the team's product owner (12 cases + effort metrics + Cursor pilot plan), 23.07 |
| `Hypotheses_Scriptwriters_FromCases_28_26.md` | H-SW-17…25 derived from the case registry (pre-ICE, metrics pending) |
| `Hypotheses_ProductDesigners_28_26.md` | July pass, H-PD-1…15; includes the Developer Status Report (Шубич, 14.07) |
| `Hypotheses_ProductManagers_28_26.md` | July pass, H-PM-1…13; synthetic + market only, zero live interviews |
| `Interview_DataAnalysts_28_26_Transcript1.md` | **Live transcript** — Вахрушева Т.И., 09.07.2026 |
| `Interview_DataAnalysts_28_26_Transcript2_Miniakhmatova.md` | **Live transcript** — Алия Миниахматова, 14.07.2026 |
| `Interview_DataAnalysts_28_26_H2_Plekhanova.md` | **Live transcript** — Мария Плеханова, 22.07.2026 *(naming caveat: "H2" here is a transcript; in PD/PM/SW files "H1/H2" means an unexecuted interview guide)* |
| `Interview_ProductDesigners_28_26_H1_PD.md` / `_H2_PD.md` | Interview **guides** for designers (round 1 / round 2) — not executed yet |
| `Interview_ProductManagers_28_26_H1_PM.md` | Interview **guide** for PMs — not executed yet |
| `Interview_Scriptwriters_28_26_H1_SW.md` / `_H2_SW.md` | Interview **guides** for scriptwriters (H-SW-1…16 / H-SW-17…25) — not executed yet |
| `archive/` | Superseded early runs (`Hypotheses_23_26.md`, `Hypotheses_23_26_2.md` — ~85% absorbed into `Hypotheses_AllRoles_23_26.md`) |
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
| DL-19 | Auto-collect statuses for weekly team report | Data analysts (team lead) | 🟡 Pivot | «Вся пятница» ≈ 8h/wk (n=1); "draft + gaps" scenario confirmed by a 2nd real team lead (Соколова, тимлид ЧБ-1 — Плеханова's team; 23.07, initially mislogged as synthetic); next: 1-sprint draft-report pilot + measure bot-ping response rate |
