# Skill — Market Scan

> Превращает «погугли мой рынок» в структурированный запрос с источниками.
> Turns "google my market" into a structured, source-backed request.

**Двуязычный формат / Bilingual format:** каждый раздел продублирован RU → EN; промпт дан в двух версиях. EN-версия обычно ищет и структурирует лучше; отчёт модель напишет на русском. / Each section is duplicated RU → EN; the prompt comes in two versions. The EN version usually searches and structures better; the report itself comes back in Russian.

---

## Назначение / Purpose

Получить картину рынка по теме за 15 минут вместо 4 часов. С источниками — иначе это галлюцинация.

Get a market picture on a topic in 15 minutes instead of 4 hours. With sources — otherwise it's a hallucination.

## Инструмент / Tooling

Любой из / Any of:
- EXA
- Perplexity (платно, лучше всего с источниками / paid, best with sources)
- Claude с web search (рядом по качеству / comparable quality)
- Tavily через API (open-source, для встраивания в скрипты / open-source, for embedding in scripts)
- SearXNG + Llama локально (полный open-source, медленнее / fully open-source, slower)

## Промпт-шаблон (RU)

```
Сделай market scan по теме: {точное описание ниши и сегмента}

Структура отчёта:

1. Размер рынка
   - Глобально (TAM)
   - В моих регионах: {регион}
   - Темп роста за последние 2 года
   - Источник для каждой цифры (без источника — не включай)

2. Игроки (минимум 5):
   - Название
   - Продукт (одной строкой)
   - ICP (для кого)
   - Ценник (от/до, модель)
   - Сильные стороны (2)
   - Слабые стороны (2)
   - Источник информации

3. Тренды (3):
   - Что меняется в отрасли
   - Кто двигает изменение
   - Сигнал для меня

4. Регуляторные риски:
   - Есть ли законы / стандарты, которые влияют
   - Сроки изменений

5. Белые пятна (2):
   - Что игроки НЕ закрывают
   - Где есть незанятая ниша

Правила:
- Каждая цифра — с источником. Без ссылки — не включай.
- Если данных нет — напиши «данных не нашёл», не выдумывай.
- Используй данные не старше 18 месяцев. Старее — помечай как историческое.
```

## Prompt template (EN)

```
Run a market scan on: {precise description of the niche and segment}
Write the report in Russian — it feeds Russian-language project files. Keep company/product names and metrics as-is.

Report structure:

1. Market size
   - Global (TAM)
   - In my regions: {region}
   - Growth rate over the last 2 years
   - A source for every figure (no source — don't include it)

2. Players (at least 5):
   - Name
   - Product (one line)
   - ICP (who it's for)
   - Pricing (from/to, model)
   - Strengths (2)
   - Weaknesses (2)
   - Information source

3. Trends (3):
   - What is changing in the industry
   - Who is driving the change
   - The signal for me

4. Regulatory risks:
   - Are there laws / standards that matter
   - Timeline of changes

5. White spaces (2):
   - What the players do NOT cover
   - Where there is an unoccupied niche

Rules:
- Every figure must have a source. No link — don't include it.
- If no data exists — write "no data found"; do not invent.
- Use data no older than 18 months. Older — mark as historical.
```

## После получения отчёта — проверочные вопросы / After the report — verification questions

### RU

```
По этому отчёту:
1. Какие из утверждений я бы перепроверил вручную?
2. Какие источники могут быть предвзятыми (паблики компаний, маркетинговые материалы)?
3. Что в отчёте противоречит моему опыту? Почему?
4. Какие 3 вопроса я задам реальному человеку из этой индустрии?
```

### EN

```
About this report (answer in Russian):
1. Which claims would I re-verify by hand?
2. Which sources may be biased (company blogs, marketing materials)?
3. What in the report contradicts my experience? Why?
4. Which 3 questions will I ask a real person from this industry?
```

## Метрика качества / Quality bar

Хороший market scan — это **отчёт, в котором есть минимум одна цифра, которая удивит**.
Если всё «как я и предполагал» — переформулируйте запрос на более узкий сегмент.

A good market scan is **a report containing at least one figure that surprises you**.
If everything is "as I expected" — narrow the segment and re-run the request.

## Ограничения / Limitations

- AI оптимизирует под «полный отчёт», а не точность — выдаёт цифры даже когда их нет
- Источники могут быть устаревшими — проверяйте дату
- Региональные данные (особенно RU/CIS) часто беднее западных — закладывайте время на ручной поиск

<!-- EN -->
- AI optimizes for "a complete report", not accuracy — it produces figures even when none exist
- Sources may be outdated — check the dates
- Regional data (especially RU/CIS) is often poorer than Western data — budget time for manual search
