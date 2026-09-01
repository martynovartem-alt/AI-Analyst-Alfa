# Candidate roles — ranked by evidence × access

> Источник: `CLAUDE.md`, раздел «Candidate roles» (updated 19.08.2026, live БА-строка обновлена 28.08.2026). Скопировано как есть, без изменений содержания.

| Role | Access | Evidence status (see Decision Log Index for verdicts) | Rank |
|---|---|---|---|
| Data analysts / Аналитики данных (DL-1 team + 2 more teams) | **Have access**, incl. live тимлид contact (Соколова, ЧБ-1) since 23.07 | 3 live interviews done (Вахрушева 09.07, Миниахматова 14.07, Плеханова 22.07) + live talk with тимлид ЧБ-1 (Соколова 23.07) → cycles DL-5…DL-20. Strongest surviving: DL-19, DL-18 (Jira automation), DL-17 + its untested narrowing DL-20 (clustering). Most narrative/report hypotheses killed. DL-5 open but weakened. OST built 07.08 (`OST_DataAnalysts_28_26.md`) | **#1** |
| Chatbot scenario writers / Сценаристы чат-ботов | **Have access** | DL-3/DL-4 stalled at synthetic stage (deadline 14.06 passed, no live interviews yet; guides ready). Product-data track: 12-case registry → H-SW-17…25 (23.07) + revised H-SW-26…52 (27.07, Григоренко: dedup vs in-flight case initiatives, augment-framing enforced). Cursor pilot (May–June, 5 scriptwriters) has no recorded results | **#2** |
| Product designers / Продуктовые дизайнеры | **Have access (via developer contact Николай Шубич, since 14.07.2026)** | H-PD-3/5 confirmed & in development by the developer; H-PD-4 pain confirmed but already covered by an existing tool (Clade) — not being built. Zero live interviews with a designer themselves; round-2 guide ready | **#3** |
| Product managers / Продакт-менеджеры | **Live contact established** — 4 live interviews done: Валентин Шмаков 18.08, Ксения Долгова 23.08, Анастасия Дубкова + Алексей Лаврищенко 26.08 (interviewer Арман Урбисинов) | 11 live-evidence cycles DL-21…DL-31: H-PM-4 → wrong role (PRD written by бизнес-аналитик, confirmed independently **three** times), H-PM-12 killed for respondent (reinforced 26.08), H-PM-9 partial (BI config, not LLM), **H-PM-2 (was top-ranked, ICE 216) weakening on 3 of 4 live respondents** (near-total BI self-service / no clarification-round friction), H-PM-17 strengthened, H-PM-8 narrowed to a status-notification artifact. **26.08: H-PM-1 (VOK diagnosis) reopened** — 2 new respondents personally burn major time on it, internal LLM already tried and failed on this exact task; **H-PM-19 (impact estimation) gets its first live data and jumps to new #1 by ICE (252)** — named the single hardest part of master-plan work by both new respondents; **2 new hypotheses registered** (H-PM-22 self-serve data access reusing shipped DL-1, H-PM-23 service/contact catalog echoing DL-12) | **#4** |
| *Business analyst / Бизнес-аналитик (spawn из DL-21, 19.08; readdressed 27.08)* | **Live contact established 28.08.2026** — 1st live interview (Ольга Серегина, БА команды CRM SFA; interviewer Арман Урбисинов) | Hypotheses reused from the PM registry (`Hypotheses_BusinessAnalysts_35_26.md`, 27.08.2026 — see note below for why); readdressed set now H-BA-1 (was H-PM-4/H-PM-17) + H-BA-2 (was H-PM-1). Synthetic CustDev 27–28.08 (personas «Наталья»/«Алексей», `SKILL/BusinessAnalysts`) → H-BA-3…5. **28.08, 1st live interview → DL-32…35:** 3rd independent confirmation of BA→system-analyst handoff, now first-person (H-BA-1/H-BA-5, ICE 144 — narrowed toward BPMN auto-draft + internal context, since BRD-text drafting is already DIY-solved by the respondent with generic external AI); H-BA-2 gets a 3rd straight first-person 🔴 (team-specific, not role-wide, ICE 24); H-PM-23 (service/contact catalog) gets a 4th independent cross-role source, now from BA itself (ICE 210); **new hypothesis H-BA-6** (internal-knowledge RAG agent over Confluence/Jira/АБУК) registered as the respondent's loudest, most-repeated self-named pain — missed by both synthetic personas (ICE 126) | — |

> **Note:** "Chatbot scriptwriters" and "scenario writers" are the same role — one person writes both JS scripts and NLU training data (intents, utterances, RegExp). DL-3 and DL-4 both target this role.

> **Note (updated 14.07.2026):** Product designer access is resolved — reached through a developer (Николай Шубич) who is already building AI tools for that role. ~~Product manager access is still unresolved~~ — **superseded 18.08.2026:** PM access resolved — Арман Урбисинов conducted the first live PM interview (Валентин Шмаков) → DL-21…DL-24.

*Ranking logic: access is the binding constraint at <1 year tenure. Data analysts and scriptwriters have existing relationships and can be interviewed now. **⚠️ The #3-vs-#4 ordering premise is now obsolete (19.08.2026):** designers ranked above PMs because PM access was zero — but PMs now have a live interview while designers still have none. Revisit the order on the next ranking pass: PM evidence is live but mostly disconfirming (DL-22 killed, DL-21/24 point to adjacent roles), while designer evidence is confirmed-but-secondhand.*

> **Note (27.08.2026) — Business Analyst track reuses the PM hypothesis registry, not a fresh generation:** `Hypotheses_BusinessAnalysts_35_26.md` readdresses the existing PM registry (`Hypotheses_ProductManagers_28_26.md`, H-PM-1…23) instead of generating candidates from scratch. Reason: bank-specific role mapping. Across three independent live PM interviews (Шмаков DL-21, Долгова DL-26, Лаврищенко 26.08) ownership of detailed requirements — PRD, CJM, BPMN — consistently landed on the **бизнес-аналитик**, not the PM. In this bank, the БА role is functionally closer to the *original* candidate-role thesis behind the PM hypotheses (owns requirements, CJM, task framing) than the PM role turned out to be in practice — PM reads more as a coordination/prioritization role (see DL-21/DL-26/DL-28 and the #3-vs-#4 ordering note above). First synthetic CustDev for this track ran 27.08.2026 (`roles/BusinessAnalysts/synthetic_custdev_business_analyst/session_natalya_business_analyst_syntetic_custdev.md`); interview guide for the first live BA respondent is ready (`Live_interview/BusinessAnalysts/Interview_BusinessAnalysts_35_26_H1_BA.md`).

> **Note (28.08.2026) — first live BA interview closes the access gap:** Ольга Серегина (БА команды доработки CRM SFA) interviewed 28.08.2026 → DL-32…DL-35. Confirms the BA→system-analyst handoff from the respondent's own perspective for the first time (was previously only reported secondhand by PMs); narrows H-BA-1/H-BA-5 toward BPMN auto-drafting and internal-context access, since BRD-text drafting is already DIY-solved with a generic external AI; kills H-BA-2 as a role-wide hypothesis (3rd straight first-person 🔴); strengthens H-PM-23 to a 4th independent cross-role source (ICE 210); registers new hypothesis H-BA-6 (internal-knowledge RAG agent), the respondent's loudest self-named pain, missed by both synthetic personas. Full сверка: `Live_interview/BusinessAnalysts/Interview_BusinessAnalysts_35_26_H1_BA_v2_synt.md`.

---

## Per-role files

- [DataAnalysts.md](DataAnalysts.md)
- [ScenarioWriters.md](ScenarioWriters.md)
- [ProductDesigners.md](ProductDesigners.md)
- [ProductManagers.md](ProductManagers.md)
- [BusinessAnalysts.md](BusinessAnalysts.md)

## Synthetic personas (SKILL/)

> Единый токен роли (CamelCase) используется во всех именах: `SKILL/<Token>`, `roles/<Token>/`, `roles_description/<Token>.md`. Подробная сводка по каждой персоне — в per-role файле выше.

| Роль | SKILL-файл | Персона | База калибровки | Годится для вердиктов? |
|---|---|---|---|---|
| Data analysts | `SKILL/DataAnalysts` | «Катя» | 3 живых июльских интервью (DL-5…DL-20) | Да — единственная first-person персона |
| Chatbot scenario writers | `SKILL/ScenarioWriters` | «Дима» | Product data: реестр кейсов команды (23.07) | Осторожно — проценты не подтверждены от первого лица |
| Product designers | `SKILL/ProductDesigners` | «Лена» | Secondhand: Developer Status Report (Шубич) | Нет — только для оттачивания вопросов гайда |
| Product managers | `SKILL/ProductManagers` | «Игорь» | Живое интервью Шмакова (DL-21…24); ⚠️ не рекалиброван на Долгову/Дубкову/Лаврищенко | Частично — до рекалибровки |
| Business analyst | `SKILL/BusinessAnalysts` | «Наталья» + «Алексей» | Вакансия Альфа-Банка + кросс-ролевые PM-сигналы; рекалибровано 28.08.2026 на 1-м живом интервью (Серегина, DL-32…35) | Частично — n=1 живой, ни одна персона не выиграла чисто (обе пропустили топ-боль H-BA-6) |
| Internal customer | `SKILL/InternalCustomer` | «Марина» | Кросс-ролевой паттерн 3/3 аналитиков + DL-21 | Нет — demand-side разогрев |
