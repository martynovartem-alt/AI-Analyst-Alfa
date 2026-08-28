# AI-Analyst-Alfa — hypothesis discovery для AI-инструментов в банке

Рабочее пространство продуктовых гипотез: какие роли в IT банка аугментировать AI-инструментами следующим шагом. Это не кодовый проект — набор стратегических документов, скиллов-промптов и записей исследований.

## С чего начать

1. **`CLAUDE.md`** — контекст продукта, стратегия, ранжирование ролей и **Decision Log Index** (одна строка на цикл).
2. **`decision-log.md`** — канонический лог всех циклов проверки гипотез: полные записи DL-0…DL-31 с цитатами. Принцип: «если решение не записано — его не было».

## Текущее состояние (28.08.2026)

- **Аналитики данных (#1):** 3 живых интервью + живой контакт с тимлидом ЧБ-1 (Соколова). Выжившие гипотезы — DL-19/DL-18 (Jira-автоматизация), DL-17/DL-20 (классификация/кластеризация). Дев-планы готовы в `MVP_DevPlans_30_26.md`, OST — в `OST_DataAnalysts_28_26.md`.
- **Сценаристы чат-ботов (#2):** синтетика + реестр кейсов от продакт-оунера (H-SW-17…52); живых интервью нет, гайды готовы, DL-3/DL-4 застряли.
- **Продуктовые дизайнеры (#3):** подтверждения только через разработчика (Шубич); живых интервью с дизайнером нет.
- **Продакт-менеджеры (#4):** 4 живых интервью (Шмаков, Долгова, Дубкова, Лаврищенко; интервьюер — Арман Урбисинов) → циклы DL-21…DL-31. Лидер по ICE — H-PM-19 (оценка эффекта, 252); H-PM-1 (диагностика VOK) переоткрыта; бывший топ H-PM-2 слабеет на живых данных.
- **Бизнес-аналитик (новый трек):** порождён живыми PM-интервью — PRD/CJM/BPMN в этом банке пишет БА, а не PM. Реестр `Hypotheses_BusinessAnalysts_35_26.md` переадресует PM-гипотезы (H-BA-1/H-BA-2); первый синтетический CustDev проведён 27.08, гайд живого интервью готов, живых БА-интервью пока ноль.

## Воркфлоу одного цикла (~3 часа)

0. Сгенерировать кандидатов — `skill-hypothesis-generating.md` (источники: Рынок / CustDev / Product data)
1. Структурировать топ-кандидата — `skill-hypothesis-check.md` (гипотеза + ICE I·C·A + критерии go/pivot/stop)
2. Синтетический CustDev — `skill-synthetic-custdev.md` (готовые персоны по ролям — в `SKILL/`)
3. Целевой market scan — `skill-market-scan.md` (нужен инструмент с web-поиском, иначе цифры будут галлюцинацией)
4. Записать полный `DL-N` в `decision-log.md` по шаблону `skill-decision-log.md`
5. Обновить строку этого `DL-N` в `CLAUDE.md → Decision Log Index` — петля замкнулась

## Структура файлов

Материалы по ролям с 19.08.2026 живут в `roles/<Role>/`; гайды и транскрипты живых интервью с 28.08.2026 — в `Live_interview/<Role>/`. Канонические имена ролей (EN/RU и токены `SKILL/`) закреплены в `CLAUDE.md`.

| Группа | Файлы |
|---|---|
| Ядро | `CLAUDE.md`, `decision-log.md`, `CLAUDE_template.md`, `README.md` |
| Скиллы (промпты) | `skill-hypothesis-generating.md`, `skill-hypothesis-check.md`, `skill-synthetic-custdev.md`, `skill-market-scan.md`, `skill-decision-log.md` — с 28.08 двуязычные (RU + EN); EN-версии промптов точнее следуют инструкциям, ответы модель даёт по-русски |
| Персоны для синтетического CustDev | `SKILL/DataAnalysts` («Катя», на базе 3 живых интервью) · `SKILL/ScenarioWriters` · `SKILL/ProductDesigners` · `SKILL/ProductManagers` · `SKILL/InternalCustomer` (заказчик, demand-side) · `SKILL/BusinessAnalysts` («Наталья» + «Алексей») |
| Описания ролей | `roles_description/` — карточки ролей + `all_roles_description.md` (копия ранжирования из `CLAUDE.md`) |
| Build-фаза (аналитики) | `MVP_DevPlans_30_26.md` (дев-планы DL-19/DL-18/DL-17) · `OST_DataAnalysts_28_26.md` (Opportunity Solution Tree) · `tasks_dl19/` (разбиение задач DL-19) |
| Кросс-ролевой скорборд | `HypothesisBacklog.md` / `HypothesisBacklog_v2.md` — плоский ICE-обзор поверх всех реестров; канон остаётся в `decision-log.md` |
| **Живые интервью** | `Live_interview/<Role>/` — гайды (сценарии) и транскрипты живых интервью, все роли в одном месте. Транскрипты: `DataAnalysts/` — Вахрушева 09.07, Миниахматова 14.07, Плеханова 22.07; `ProductManagers/` — Шмаков 18.08, Долгова 23.08, Дубкова и Лаврищенко 26.08. Гайды: `Live_interview/ProductManagers/Interview_ProductManagers_28_26_H2_PM_round2.md` (актуальный, v4; v1–v3 рядом как superseded), `ScenarioWriters/` H1/H2, `ProductDesigners/` H1/H2, `BusinessAnalysts/` H1 — не проведены |
| Аналитики данных | `roles/DataAnalysts/`: реестр `Hypotheses_DataAnalysts_28_26.md` |
| Сценаристы | `roles/ScenarioWriters/`: реестры `Hypotheses_Scriptwriters_28_26.md` (H-SW-1…16, 26…52) и `Hypotheses_Scriptwriters_FromCases_28_26.md` (H-SW-17…25) · product data `Cases_Scriptwriters_28_26.md` |
| Дизайнеры | `roles/ProductDesigners/`: реестр `Hypotheses_ProductDesigners_28_26.md` (вкл. Developer Status Report) |
| Продакт-менеджеры | `roles/ProductManagers/`: канонический реестр `roles/ProductManagers/Hypotheses/Hypotheses_ProductManagers_28_26.md` (H-PM-1…23) · market scan `market_reserch_pm/` (13.08, с источниками) · мультиагентный чекаут `checkout_hyphothesis_12.08_managers/` · синтетика `synthetic_custdev_19_08/` (PM «Игорь», заказчик «Марина») |
| Бизнес-аналитики | `roles/BusinessAnalysts/`: реестр `roles/BusinessAnalysts/Hypotheses/Hypotheses_BusinessAnalysts_35_26.md` (переадресация PM-реестра + новые H-BA-3…5 от 28.08) · синтетика в `roles/BusinessAnalysts/synthetic_custdev_business_analyst/` — «Наталья» (27.08) и «Алексей» (28.08); прогнозы обеих вшиты в сценарий v2 (`Live_interview/BusinessAnalysts/Interview_BusinessAnalysts_35_26_H1_BA_v2_synt.md`) как `SYNT PERSONA ANSWER:` |
| Гипотезы (июнь 2026) | `roles/Hypotheses_AllRoles_23_26.md` — статусы заморожены на 09.06; актуальные вердикты в `decision-log.md` |
| Архив | `archive/` — ранние прогоны (`Hypotheses_23_26.md`, `Hypotheses_23_26_2.md`), поглощённые каноническими файлами |

## Что НЕ делает этот набор

- Не заменяет реальный CustDev — синтетика только готовит к нему. В этом проекте правило подтверждено практикой дважды: живые интервью июля закрыли большинство «очевидных» гипотез аналитиков (DL-7…DL-15), а живые PM-интервью августа развернули синтетический топ (H-PM-2 слабеет, H-PM-4 оказался не той ролью → трек БА)
- Не принимает решения за вас — даёт draft, вы корректируете
- Не работает без вашего суждения — AI не валидирует свои ответы
