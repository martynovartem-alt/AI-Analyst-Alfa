# Skill — Hypothesis Check

> Структурирует сырую гипотезу + считает ICE.
> Structures a raw hypothesis + computes ICE.

**Двуязычный формат / Bilingual format:** каждый раздел продублирован RU → EN; промпт дан в двух версиях. EN-версия промпта обычно даёт более точное следование инструкциям — используйте её, ответ модель даст на русском. / Each section is duplicated RU → EN; the prompt comes in two versions. The EN prompt usually yields better instruction-following — use it; the model will still answer in Russian.

---

## Назначение / Purpose

Превращает «у меня есть идея» в проверяемую гипотезу с критериями успеха и приоритетом.

Turns "I have an idea" into a testable hypothesis with success criteria and a priority score.

## Промпт (RU)

```
Я хочу проверить продуктовую гипотезу. Помоги структурировать.

Сырая идея: {опишите идею своими словами}

Сделай следующее:

1. Переформулируй в формат:
   «{ЦА} {готова сделать что-то / готова заплатить за / переключится на} {решение}, если {условие}»

2. Найди скрытые допущения (минимум 3):
   - что мы предполагаем по поведению ЦА
   - что мы предполагаем по рынку
   - что мы предполагаем по технологии

3. Определи как проверить (минимум 2 способа):
   - синтетический CustDev → какие вопросы задать
   - живой CustDev → сколько респондентов и какие критерии
   - количественный → какой запрос к данным
   - рыночный → какие сигналы искать

4. Оцени по ICE (1–10), обоснуй каждую цифру в одну строку:
   - Impact: насколько изменит метрики, если подтвердится
   - Confidence: насколько уверен, что подтвердится
   - Ease: насколько легко проверить

5. Дай критерии:
   - Зелёный свет (продолжаем)
   - Жёлтый (pivot)
   - Красный (стоп)

6. Предложи дедлайн проверки (в днях).
```

## Prompt (EN)

```
I want to validate a product hypothesis. Help me structure it.
Answer in Russian — the hypothesis wording and all output will be used in Russian-language project files.

Raw idea: {describe the idea in your own words}

Do the following:

1. Reformulate into the format:
   "{Target audience} {is ready to do something / is ready to pay for / will switch to} {solution}, if {condition}"

2. Surface hidden assumptions (at least 3):
   - what we assume about the target audience's behavior
   - what we assume about the market
   - what we assume about the technology

3. Define how to test it (at least 2 methods):
   - synthetic CustDev → which questions to ask
   - live CustDev → how many respondents and what criteria
   - quantitative → what data query to run
   - market → what signals to look for

4. Score it with ICE (1–10), justifying each number in one line:
   - Impact: how much it moves the metrics if confirmed
   - Confidence: how sure we are it will be confirmed
   - Ease: how easy it is to test

5. Give decision criteria:
   - Green light (continue)
   - Yellow (pivot)
   - Red (stop)

6. Propose a validation deadline (in days).
```

## Что НЕ делать / What NOT to do

- Не запускайте проверку без чёткого критерия успеха
- Не доверяйте ICE от AI без своей корректировки — это draft, не вердикт
- Не сравнивайте ICE между гипотезами разного масштаба

<!-- EN -->
- Don't start validation without a clear success criterion
- Don't trust AI-produced ICE without your own adjustment — it's a draft, not a verdict
- Don't compare ICE scores across hypotheses of different scale

## Пример заполнения / Worked example

| Поле | Значение |
|---|---|
| Сырая идея | Команды разметки готовы платить за ускорение постановки задач |
| Структура | Head of Annotation в командах ≥5 человек готов платить ₽30k/мес за инструмент, который сократит постановку задач с 40 мин до 10 мин, если результат сопоставим по качеству |
| Допущение 1 | Постановка задач — реальный bottleneck (не выдуманный) |
| Допущение 2 | Качество автогенерируемой инструкции достаточно для разметчика |
| Допущение 3 | 30k/мес — порог, до которого решают без CFO |
| Проверка качественная | 5 интервью с Head of Annotation за неделю |
| Проверка количественная | SQL по нашим теплым лидам: сколько уже отвечали что тратят >2ч/нед |
| ICE | I=8, C=5, E=7 → 280 |
| Зелёный | 3 из 5 респондентов: «да, готов платить ≥20k» |
| Жёлтый | 1-2 из 5: пересобрать УТП |
| Красный | 0 из 5 или возражения по качеству |
| Дедлайн | 10 дней |

| Field | Value |
|---|---|
| Raw idea | Annotation teams are ready to pay for faster task briefing |
| Structured | Head of Annotation in teams ≥5 people is ready to pay ₽30k/mo for a tool that cuts task briefing from 40 min to 10 min, if output quality is comparable |
| Assumption 1 | Task briefing is a real bottleneck (not an imagined one) |
| Assumption 2 | Auto-generated instruction quality is sufficient for an annotator |
| Assumption 3 | 30k/mo is below the threshold that requires CFO sign-off |
| Qualitative test | 5 interviews with Heads of Annotation within a week |
| Quantitative test | SQL over our warm leads: how many already reported spending >2h/week |
| ICE | I=8, C=5, E=7 → 280 |
| Green | 3 of 5 respondents: "yes, ready to pay ≥20k" |
| Yellow | 1–2 of 5: rebuild the value proposition |
| Red | 0 of 5, or quality objections |
| Deadline | 10 days |
