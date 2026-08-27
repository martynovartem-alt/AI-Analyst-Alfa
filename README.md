# AI-Analyst-Alfa — hypothesis discovery для AI-инструментов в банке

Рабочее пространство продуктовых гипотез: какие роли в IT банка аугментировать AI-инструментами следующим шагом. Это не кодовый проект — набор стратегических документов, скиллов-промптов и записей исследований.

## С чего начать

1. **`CLAUDE.md`** — контекст продукта, стратегия, ранжирование ролей и **Decision Log Index** (одна строка на цикл).
2. **`decision-log.md`** — канонический лог всех циклов проверки гипотез: полные записи DL-0…DL-19 с цитатами. Принцип: «если решение не записано — его не было».

## Воркфлоу одного цикла (~3 часа)

0. Сгенерировать кандидатов — `skill-hypothesis-generating.md` (источники: Рынок / CustDev / Product data)
1. Структурировать топ-кандидата — `skill-hypothesis-check.md` (гипотеза + ICE I·C·A + критерии go/pivot/stop)
2. Синтетический CustDev — `skill-synthetic-custdev.md` (готовые персоны по ролям — в `SKILL/`)
3. Целевой market scan — `skill-market-scan.md` (нужен инструмент с web-поиском, иначе цифры будут галлюцинацией)
4. Записать полный `DL-N` в `decision-log.md` по шаблону `skill-decision-log.md`
5. Обновить строку этого `DL-N` в `CLAUDE.md → Decision Log Index` — петля замкнулась

## Структура файлов

| Группа                             | Файлы                                                                                                                                                                                                                     |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ядро                               | `CLAUDE.md`, `decision-log.md`, `CLAUDE_template.md`, `README.md`                                                                                                                                                         |
| Скиллы (промпты)                   | `skill-hypothesis-generating.md`, `skill-hypothesis-check.md`, `skill-synthetic-custdev.md`, `skill-market-scan.md`, `skill-decision-log.md`                                                                              |
| Персоны для синтетического CustDev | `SKILL/analyst`, `SKILL/Scenario writer`, `SKILL/Product designer`, `SKILL/Product manager`, `SKILL/zakazchik`, `SKILL/business_analyst`                                                                                                                                                            |
| Гипотезы по ролям (июль 2026)      | `Hypotheses_DataAnalysts_28_26.md`, `Hypotheses_Scriptwriters_28_26.md`, `Hypotheses_Scriptwriters_FromCases_28_26.md`, `Hypotheses_ProductDesigners_28_26.md`, `Hypotheses_ProductManagers_28_26.md`                     |
| Гипотезы (июнь 2026)               | `Hypotheses_AllRoles_23_26.md` — статусы заморожены на 09.06; актуальные вердикты в `decision-log.md`                                                                                                                     |
| Product data                       | `Cases_Scriptwriters_28_26.md` — реестр кейсов команды сценаристов (12 кейсов + метрики + план пилота Cursor)                                                                                                             |
| Живые интервью (транскрипты)       | `Interview_DataAnalysts_28_26_Transcript1.md` (Вахрушева, 09.07) · `Interview_DataAnalysts_28_26_Transcript2_Miniakhmatova.md` (Миниахматова, 14.07) · `Interview_DataAnalysts_28_26_H2_Plekhanova.md` (Плеханова, 22.07) |
| Гайды интервью (ещё не проведены)  | `Interview_ProductDesigners_28_26_H1_PD.md` / `_H2_PD.md` · `Interview_ProductManagers_28_26_H1_PM.md` · `Interview_Scriptwriters_28_26_H1_SW.md` / `_H2_SW.md`                                                           |
| Архив                              | `archive/` — ранние прогоны (`Hypotheses_23_26.md`, `Hypotheses_23_26_2.md`), поглощённые каноническими файлами                                                                                                           |

## Что НЕ делает этот набор

- Не заменяет реальный CustDev — синтетика только готовит к нему. В этом проекте правило подтверждено практикой: живые интервью июля закрыли большинство «очевидных» гипотез (см. DL-7…DL-15), которые синтетика не отсеяла
- Не принимает решения за вас — даёт draft, вы корректируете
- Не работает без вашего суждения — AI не валидирует свои ответы
