# Skill — Hypothesis Generating

> Систематически добывает кандидаты в гипотезы из трёх источников и выдаёт приоритизированный список, готовый к проверке через `skill-hypothesis-check.md`.
> Systematically mines hypothesis candidates from three sources and produces a prioritized list ready for `skill-hypothesis-check.md`.

**Двуязычный формат / Bilingual format:** каждый раздел продублирован RU → EN; все четыре промпта даны в двух версиях. EN-версии обычно точнее следуют структуре задачи; формулировки гипотез модель выдаст на русском. / Each section is duplicated RU → EN; all four prompts come in two versions. The EN versions usually follow the task structure more precisely; hypothesis wording still comes back in Russian.

---

## Назначение / Purpose

Большинство гипотез не умирают при проверке — их просто никогда не записывают. Этот скилл решает задачу «откуда берутся гипотезы» и структурирует три принципиально разных сигнала в единый список кандидатов.

**Не заменяет `skill-hypothesis-check.md`.** Это воронка на входе: сырые кандидаты, не структурированные гипотезы.

Most hypotheses don't die in validation — they simply never get written down. This skill answers "where do hypotheses come from" and structures three fundamentally different signals into a single candidate list.

**Does not replace `skill-hypothesis-check.md`.** This is the intake funnel: raw candidates, not structured hypotheses.

## Три источника / Three sources

| Источник | Что даёт | Главный риск |
|---|---|---|
| **Рынок / конкуренты** | Боли и решения, уже подтверждённые чужими деньгами | Работает у них — не значит работает у вас |
| **CustDev** | Прямые цитаты и подтверждённые паттерны боли | Малая выборка, субъективность интерпретации |
| **Вижн / данные продукта** | Остаточные сигналы, паттерны использования, идеи команды | Слепое пятно — видите только то, что уже знаете |

| Source | What it gives | Main risk |
|---|---|---|
| **Market / competitors** | Pains and solutions already validated with someone else's money | Works for them ≠ works for you |
| **CustDev** | Direct quotes and confirmed pain patterns | Small sample, subjective interpretation |
| **Vision / product data** | Residual signals, usage patterns, team ideas | Blind spot — you only see what you already know |

**Правило двух источников:** если гипотеза появляется сразу из двух — это сильный сигнал. Из одного — требует дополнительной проверки перед запуском.

**The two-source rule:** if a hypothesis shows up in two sources at once — that's a strong signal. From one source only — it needs extra verification before launch.

## Когда использовать / When to use

- В начале нового цикла открытий — нужно понять, что проверять следующим
- После блока CustDev-интервью — конвертировать сырые записи в гипотезы
- После market scan — превратить рыночные сигналы в конкретные кандидаты
- Когда текущий продукт показал неожиданный паттерн — оформить в гипотезу
- Когда гипотеза была убита — найти остаточные сигналы для следующей

<!-- EN -->
- At the start of a new discovery cycle — to decide what to test next
- After a block of CustDev interviews — to convert raw notes into hypotheses
- After a market scan — to turn market signals into concrete candidates
- When the current product shows an unexpected pattern — to capture it as a hypothesis
- When a hypothesis was killed — to find residual signals for the next one

---

## Промпт 1 — Рынок / конкуренты (RU)

```
Я изучил рынок и хочу извлечь кандидатные гипотезы.

Контекст продукта:
{вставьте ключевые детали из CLAUDE.md — кто вы, что уже сделано, ограничения, стек}

Рыночные сигналы (заполните то, что есть):
- Кейсы конкурентов: {что конкурент X делает для роли Y, с каким результатом}
- Тренды: {что меняется в индустрии}
- Данные из market scan: {ключевые цифры и инсайты с источниками}
- Новые инструменты на рынке: {что появилось для этой роли}

Задача:

1. Для каждого сигнала сформулируй кандидатную гипотезу в формате:
   «{Роль} будет использовать {решение}, если {условие}»

2. Для каждой гипотезы укажи:
   - Источник (откуда сигнал)
   - Почему может работать в нашем контексте
   - Главный риск переноса (почему у них сработало, но у нас может не сработать)
   - Сила сигнала: Сильный (есть метрика) / Средний (есть кейс без метрики) / Слабый (тренд без кейса)

3. Выдели отдельно гипотезы, где конкурент уже реализовал решение с измеримым результатом — это наиболее валидированные кандидаты.

Не выдумывай данные. Если сигнал слабый — пометь как «требует проверки».
```

## Prompt 1 — Market / competitors (EN)

```
I've researched the market and want to extract candidate hypotheses.
Answer in Russian — hypothesis wording feeds Russian-language project files.

Product context:
{paste key details from CLAUDE.md — who you are, what's already shipped, constraints, stack}

Market signals (fill in what you have):
- Competitor cases: {what competitor X does for role Y, with what result}
- Trends: {what is changing in the industry}
- Market-scan data: {key figures and insights with sources}
- New tools on the market: {what has appeared for this role}

Task:

1. For each signal, formulate a candidate hypothesis in the format:
   "{Role} will use {solution}, if {condition}"

2. For each hypothesis, specify:
   - Source (where the signal comes from)
   - Why it could work in our context
   - Main transfer risk (why it worked for them but might not for us)
   - Signal strength: Strong (has a metric) / Medium (a case without a metric) / Weak (a trend without a case)

3. Separately highlight hypotheses where a competitor has already shipped the solution with a measurable result — these are the most validated candidates.

Do not invent data. If a signal is weak — mark it "requires verification".
```

---

## Промпт 2 — CustDev (RU)

```
У меня есть сырые записи из интервью или наблюдений. Помоги извлечь гипотезы.

Контекст продукта:
{вставьте ключевые детали из CLAUDE.md}

Записи CustDev (вставьте в любом формате — цитаты, тезисы, наблюдения):
{вставьте сырые записи}

Задача:

1. Найди боли трёх типов:
   - Явная: пользователь прямо сказал, что это проблема
   - Скрытая: описал поведение, которое указывает на боль, но не назвал её
   - Компенсаторная: делает что-то неудобное вместо нормального решения (Excel вместо системы, мессенджер вместо инструмента)

2. Для каждой боли сформулируй кандидатную гипотезу:
   «{Роль} будет использовать {решение}, если {условие}»

3. Для каждой гипотезы укажи:
   - Цитата или наблюдение, которое её породило
   - Сколько раз эта боль упоминалась (прямо или косвенно)
   - Эмоциональная интенсивность: Высокая / Средняя / Низкая (по тону в записях)
   - Это реальная боль или «было бы неплохо»? (реальная боль = человек уже пытается её решить сам)

4. ТОП-3 гипотезы с наибольшей доказательной базой по этим интервью.

Не интерпретируй слишком широко — держись близко к тому, что реально сказали или показали.
```

## Prompt 2 — CustDev (EN)

```
I have raw notes from interviews or observations. Help me extract hypotheses.
Answer in Russian; keep respondent quotes verbatim, untranslated.

Product context:
{paste key details from CLAUDE.md}

CustDev notes (paste in any format — quotes, bullet points, observations):
{paste raw notes}

Task:

1. Find pains of three types:
   - Explicit: the user directly said it's a problem
   - Hidden: described behavior that points to a pain without naming it
   - Compensatory: does something inconvenient instead of a proper solution (Excel instead of a system, a messenger instead of a tool)

2. For each pain, formulate a candidate hypothesis:
   "{Role} will use {solution}, if {condition}"

3. For each hypothesis, specify:
   - The quote or observation that produced it
   - How many times this pain was mentioned (directly or indirectly)
   - Emotional intensity: High / Medium / Low (by the tone in the notes)
   - Is it a real pain or a "nice to have"? (real pain = the person is already trying to solve it themselves)

4. TOP-3 hypotheses with the strongest evidence base from these interviews.

Do not over-interpret — stay close to what was actually said or shown.
```

---

## Промпт 3 — Вижн / данные продукта / брейншторм (RU)

```
Хочу сгенерировать гипотезы из внутренних сигналов — данных продукта, остаточных находок и идей.

Контекст продукта (включая Decision Log):
{вставьте ключевые детали из CLAUDE.md, включая shipped products и все DL-N записи}

Внутренние сигналы (заполните то, что есть):
- Паттерны использования текущих продуктов: {что делают неожиданно / часто / не так, как задумывалось}
- Остаточные сигналы из убитых гипотез: {что узнали, но не использовали}
- Запросы и жалобы: {что спрашивают пользователи, на что жалуются}
- Идеи команды: {что предлагают разработчики или вы сами}
- Смежные роли: {роли рядом с теми, кого уже автоматизировали — что делают похожего?}

Задача:

1. Для каждого сигнала сформулируй кандидатную гипотезу:
   «{Роль} будет использовать {решение}, если {условие}»

2. Для каждой гипотезы укажи:
   - Тип источника: Данные (факт) / Наблюдение (интерпретация) / Интуиция (без данных)
   - Связь с уже валидированными продуктами (расширение DL-0, DL-1 и т.д.)
   - Почему именно сейчас — что изменилось, что делает гипотезу актуальной

3. Выдели отдельно:
   - «Остаточные сигналы» — боли, которые уже видели краем глаза, но не тестировали
   - «Расширения» — та же боль у соседней роли или в соседнем контексте

Честно разделяй: данные — это факт, идея команды — это интуиция. Не смешивай.
```

## Prompt 3 — Vision / product data / brainstorm (EN)

```
I want to generate hypotheses from internal signals — product data, residual findings, and ideas.
Answer in Russian — hypothesis wording feeds Russian-language project files.

Product context (including the Decision Log):
{paste key details from CLAUDE.md, including shipped products and all DL-N entries}

Internal signals (fill in what you have):
- Usage patterns of current products: {what users do unexpectedly / frequently / not as designed}
- Residual signals from killed hypotheses: {what we learned but never used}
- Requests and complaints: {what users ask for, what they complain about}
- Team ideas: {what developers or you yourself propose}
- Adjacent roles: {roles next to the ones already automated — what similar work do they do?}

Task:

1. For each signal, formulate a candidate hypothesis:
   "{Role} will use {solution}, if {condition}"

2. For each hypothesis, specify:
   - Source type: Data (fact) / Observation (interpretation) / Intuition (no data)
   - Link to already-validated products (extension of DL-0, DL-1, etc.)
   - Why now — what has changed that makes the hypothesis timely

3. Separately highlight:
   - "Residual signals" — pains already glimpsed but never tested
   - "Extensions" — the same pain in an adjacent role or adjacent context

Be honest about the split: data is fact, a team idea is intuition. Don't mix them.
```

---

## Промпт 4 — Синтез (RU)

> Запускать после того, как прогнали хотя бы два промпта выше. Объединяет все кандидаты в один приоритизированный список.

```
У меня есть кандидатные гипотезы из нескольких источников. Помоги объединить и приоритизировать.

Контекст продукта:
{вставьте ключевые детали из CLAUDE.md}

Кандидаты из источников:
- Из рынка / конкурентов: {список}
- Из CustDev: {список}
- Из визиона / данных: {список}

Задача:

1. Дедуплицируй — объедини гипотезы, которые говорят об одном и том же разными словами.
   Для объединённых — укажи, из скольких источников они подтверждаются.

2. Для каждой уникальной гипотезы оцени по трём параметрам (1–10):
   - Impact: насколько изменит метрики, если подтвердится
   - Confidence: насколько уверен, что боль реальная (на основе имеющихся данных)
   - Доступ: есть ли прямой путь к этой ЦА прямо сейчас (10 = есть, 1 = нет)

3. Выдай финальный список, отсортированный по Impact × Confidence × Доступ.

4. ТОП-1 — та гипотеза, которую рекомендуешь запустить следующей через `skill-hypothesis-check.md`.
   Обоснуй выбор в одном предложении.

Не добавляй новых гипотез на этом этапе — только работай с тем, что получено из источников.
```

## Prompt 4 — Synthesis (EN)

> Run after completing at least two of the prompts above. Merges all candidates into one prioritized list.

```
I have candidate hypotheses from several sources. Help me merge and prioritize them.
Answer in Russian — the output feeds Russian-language project files.

Product context:
{paste key details from CLAUDE.md}

Candidates by source:
- From market / competitors: {list}
- From CustDev: {list}
- From vision / data: {list}

Task:

1. Deduplicate — merge hypotheses that say the same thing in different words.
   For merged ones, state how many sources confirm them.

2. Score each unique hypothesis on three parameters (1–10):
   - Impact: how much it moves the metrics if confirmed
   - Confidence: how sure we are the pain is real (based on available data)
   - Access: is there a direct path to this audience right now (10 = yes, 1 = no)

3. Output the final list sorted by Impact × Confidence × Access.

4. TOP-1 — the hypothesis you recommend running next through `skill-hypothesis-check.md`.
   Justify the choice in one sentence.

Do not add new hypotheses at this stage — work only with what came from the sources.
```

---

## Пример заполнения (Синтез) / Worked example (Synthesis)

| Гипотеза | Источники | Impact | Confidence | Доступ | Итог |
|---|---|---|---|---|---|
| Дизайнеры используют AI для генерации вариантов UI из брифа | Рынок + Визион | 8 | 7 | 3 | 168 |
| Аналитики используют AI для обновления recurring-отчётов | CustDev + Визион | 7 | 5 | 9 | 315 |
| Сценаристы используют AI для диагностики ошибок в скриптах | CustDev (DL-2) + Визион | 7 | 6 | 8 | 336 → **ТОП-1** |

*Несмотря на то что дизайн-гипотеза сильнее по рынку, доступ к ЦА равен 3 — запустить её сейчас невозможно.*

| Hypothesis | Sources | Impact | Confidence | Access | Total |
|---|---|---|---|---|---|
| Designers use AI to generate UI variants from a brief | Market + Vision | 8 | 7 | 3 | 168 |
| Analysts use AI to refresh recurring reports | CustDev + Vision | 7 | 5 | 9 | 315 |
| Scriptwriters use AI to diagnose script defects | CustDev (DL-2) + Vision | 7 | 6 | 8 | 336 → **TOP-1** |

*Even though the design hypothesis is stronger on market evidence, audience access is 3 — it cannot be launched right now.*

---

## Что НЕ делать / What NOT to do

- Не смешивайте источники в одном промпте — сначала каждый отдельно, потом синтез
- Не принимайте рыночный кейс за подтверждение вашей боли — проверьте, что боль существует в вашем контексте
- Не запускайте гипотезу в проверку минуя `skill-hypothesis-check.md` — без ICE и критериев это не гипотеза, а идея
- Не игнорируйте остаточные сигналы из убитых гипотез — они часто ценнее новых рыночных данных

<!-- EN -->
- Don't mix sources in one prompt — each one separately first, then synthesis
- Don't take a market case as proof of your pain — verify the pain exists in your context
- Don't send a hypothesis into validation bypassing `skill-hypothesis-check.md` — without ICE and criteria it's an idea, not a hypothesis
- Don't ignore residual signals from killed hypotheses — they're often worth more than fresh market data

## Метрика качества / Quality bar

Хорошая сессия — это **5–10 кандидатных гипотез, где минимум 2–3 подтверждаются двумя источниками одновременно**.

Если все гипотезы из одного источника — вы работаете в слепом пятне.
Если нет ни одной из CustDev — вы не разговариваете с пользователями.

A good session yields **5–10 candidate hypotheses, of which at least 2–3 are confirmed by two sources at once**.

If all hypotheses come from one source — you're working in a blind spot.
If none come from CustDev — you're not talking to users.

## Ограничения / Limitations

- AI работает только с тем, что вы дали — не знает ваш банк и вашу команду
- Рыночные гипотезы требуют верификации в вашем контексте: ваш стек, ваш LLM, ваши ограничения
- CustDev из 1–2 интервью — слишком маленькая выборка; больше интервью не компенсируется качеством анализа
- «Идеи команды» без данных — это интуиция, не гипотеза; не давайте им высокий приоритет автоматически

<!-- EN -->
- AI works only with what you provide — it doesn't know your bank or your team
- Market hypotheses require verification in your context: your stack, your LLM, your constraints
- CustDev from 1–2 interviews is too small a sample; analysis quality doesn't compensate for missing interviews
- "Team ideas" without data are intuition, not hypotheses; don't auto-assign them high priority
