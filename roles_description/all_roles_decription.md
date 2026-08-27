# Candidate roles — ranked by evidence × access

> Источник: `CLAUDE.md`, раздел «Candidate roles» (updated 19.08.2026). Скопировано как есть, без изменений содержания.

| Role | Access | Evidence status (see Decision Log Index for verdicts) | Rank |
|---|---|---|---|
| Data analysts (DL-1 team + 2 more teams) | **Have access**, incl. live тимлид contact (Соколова, ЧБ-1) since 23.07 | 3 live interviews done (Вахрушева 09.07, Миниахматова 14.07, Плеханова 22.07) + live talk with тимлид ЧБ-1 (Соколова 23.07) → cycles DL-5…DL-20. Strongest surviving: DL-19, DL-18 (Jira automation), DL-17 + its untested narrowing DL-20 (clustering). Most narrative/report hypotheses killed. DL-5 open but weakened. OST built 07.08 (`OST_DataAnalysts_28_26.md`) | **#1** |
| Chatbot scenario writers | **Have access** | DL-3/DL-4 stalled at synthetic stage (deadline 14.06 passed, no live interviews yet; guides ready). Product-data track: 12-case registry → H-SW-17…25 (23.07) + revised H-SW-26…52 (27.07, Григоренко: dedup vs in-flight case initiatives, augment-framing enforced). Cursor pilot (May–June, 5 scriptwriters) has no recorded results | **#2** |
| Product designers | **Have access (via developer contact Николай Шубич, since 14.07.2026)** | H-PD-3/5 confirmed & in development by the developer; H-PD-4 pain confirmed but already covered by an existing tool (Clade) — not being built. Zero live interviews with a designer themselves; round-2 guide ready | **#3** |
| Product managers | **Live contact established** — 4 live interviews done: Валентин Шмаков 18.08, Ксения Долгова 23.08, Анастасия Дубкова + Алексей Лаврищенко 26.08 (interviewer Арман Урбисинов) | 11 live-evidence cycles DL-21…DL-31: H-PM-4 → wrong role (PRD written by бизнес-аналитик, confirmed independently **three** times), H-PM-12 killed for respondent (reinforced 26.08), H-PM-9 partial (BI config, not LLM), **H-PM-2 (was top-ranked, ICE 216) weakening on 3 of 4 live respondents** (near-total BI self-service / no clarification-round friction), H-PM-17 strengthened, H-PM-8 narrowed to a status-notification artifact. **26.08: H-PM-1 (VOK diagnosis) reopened** — 2 new respondents personally burn major time on it, internal LLM already tried and failed on this exact task; **H-PM-19 (impact estimation) gets its first live data and jumps to new #1 by ICE (252)** — named the single hardest part of master-plan work by both new respondents; **2 new hypotheses registered** (H-PM-22 self-serve data access reusing shipped DL-1, H-PM-23 service/contact catalog echoing DL-12) | **#4** |
| *Бизнес-аналитик (spawn из DL-21, 19.08)* | No contact yet — snowball via Шмаков planned | Parked until live contact: inherits readdressed H-PM-4 + H-PM-11; market/academic support is the strongest of any candidate (requirements tooling maturity 3/4 — IBM Epic Evaluator, MARE) | — |

> **Note:** "Chatbot scriptwriters" and "scenario writers" are the same role — one person writes both JS scripts and NLU training data (intents, utterances, RegExp). DL-3 and DL-4 both target this role.

> **Note (updated 14.07.2026):** Product designer access is resolved — reached through a developer (Николай Шубич) who is already building AI tools for that role. ~~Product manager access is still unresolved~~ — **superseded 18.08.2026:** PM access resolved — Арман Урбисинов conducted the first live PM interview (Валентин Шмаков) → DL-21…DL-24.

*Ranking logic: access is the binding constraint at <1 year tenure. Data analysts and scriptwriters have existing relationships and can be interviewed now. **⚠️ The #3-vs-#4 ordering premise is now obsolete (19.08.2026):** designers ranked above PMs because PM access was zero — but PMs now have a live interview while designers still have none. Revisit the order on the next ranking pass: PM evidence is live but mostly disconfirming (DL-22 killed, DL-21/24 point to adjacent roles), while designer evidence is confirmed-but-secondhand.*

---

## Per-role files

- [Data_Analysts.md](Data_Analysts.md)
- [Chatbot_Scenario_Writers.md](Chatbot_Scenario_Writers.md)
- [Product_Designers.md](Product_Designers.md)
- [Product_Managers.md](Product_Managers.md)
- [Business_Analyst.md](Business_Analyst.md)
