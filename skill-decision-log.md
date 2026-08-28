# Skill — Decision Log

> Принцип: «Если решение не записано — его не было».
> Principle: "If a decision isn't written down — it didn't happen."

**Двуязычный формат / Bilingual format:** каждый раздел продублирован RU → EN. Шаблон записи остаётся русским — канонический `decision-log.md` ведётся на русском; EN-версия промпта надёжнее заполняет шаблон без выдумывания. / Each section is duplicated RU → EN. The entry template stays Russian — the canonical `decision-log.md` is kept in Russian; the EN prompt fills the template more reliably without inventing data.

---

## Назначение / Purpose

Превращает каждый цикл проверки гипотезы в запись, которую агент «помнит» при следующем обращении. И вы тоже помните — что для команды важнее.

Turns every hypothesis-validation cycle into a record the agent "remembers" on the next session. And so do you — which matters more for the team.

## Где хранить / Where to keep it

Один из вариантов (выбрать один и не смешивать) / One of (pick one, don't mix):
- `decision-log.md` рядом с CLAUDE.md / next to CLAUDE.md
- Раздел в Notion / Obsidian / A section in Notion / Obsidian
- Issue в GitHub с лейблом `decision` / A GitHub issue labeled `decision`

## Шаблон записи / Entry template

*Шаблон один, на русском — записи в канонический лог всегда на русском. / One template, in Russian — canonical log entries are always in Russian.*

```markdown
## DL-{номер} — {короткая суть решения} ({дата})

**Гипотеза:**
> {точная формулировка}

**Что проверяли:**
- Метод: {синтетический CustDev / интервью / данные / рынок}
- Объём: {сколько респондентов / запросов / источников}
- Период проверки: {N дней}

**Что узнали (3-5 пунктов):**
1.
2.
3.

**Цитаты / данные (доказательная база):**
> «…»
> Источник: {имя / ссылка}

**Решение:**
- [ ] Зелёный — продолжаем
- [ ] Жёлтый — pivot: {что меняем}
- [ ] Красный — стоп: {почему окончательно}

**Что делаем дальше:**
- Следующий шаг: {конкретное действие}
- Ответственный:
- Дедлайн:

**Связанные:**
- Предыдущее решение: DL-{N}
- Гипотеза, которая родилась отсюда:

**Авторство:**
- Кто принял решение:
- Кто участвовал в обсуждении:
```

## Промпт для генерации записи (RU)

```
На основе нашей сессии проверки гипотезы — заполни Decision Log по шаблону:
{вставьте шаблон выше}

Учти только то, что мы реально проверили в этой сессии. Не выдумывай данные. Если чего-то не было — оставь поле пустым с пометкой "не проверяли".
```

## Entry-generation prompt (EN)

```
Based on our hypothesis-validation session, fill in the Decision Log using this template (fill it in Russian — the canonical log is kept in Russian):
{paste the template above}

Include only what we actually tested in this session. Do not invent data. If something wasn't done — leave the field empty with the note "не проверяли" (not tested).
```

## Что делает Decision Log сильным / What makes a Decision Log strong

- **Цитаты и цифры** — без них это «мне показалось»
- **Связь с предыдущими** — видно, как эволюционирует продукт
- **Авторство** — понятно, кто отвечает
- **Следующий шаг** — иначе решение зависает

<!-- EN -->
- **Quotes and numbers** — without them it's just "it seemed to me"
- **Links to previous entries** — you can see how the product evolves
- **Authorship** — it's clear who is accountable
- **A next step** — otherwise the decision hangs in the air

## Антипаттерны / Anti-patterns

- «Мы решили продолжать» без критериев — это не решение, а пауза
- Список «выводов» без действий — мёртвый документ
- Один человек заполняет за всю команду — теряется контекст
- Decision Log без срока пересмотра — устаревает

<!-- EN -->
- "We decided to continue" without criteria — that's not a decision, it's a pause
- A list of "takeaways" without actions — a dead document
- One person filling it in for the whole team — context gets lost
- A Decision Log without a review date — it goes stale

## Бонус — петля / Bonus — the loop

После заполнения: полная запись остаётся в `decision-log.md` (канонический лог), а в `CLAUDE.md → Decision Log Index` добавьте её однострочную сводку. Следующий раз, когда вы откроете Claude и спросите «какую гипотезу проверять?», агент учтёт прошлый decision log и не предложит то, что вы уже отбросили.

After filling it in: the full entry stays in `decision-log.md` (the canonical log), and you add its one-line summary to `CLAUDE.md → Decision Log Index`. Next time you open Claude and ask "which hypothesis should I test?", the agent takes the past decision log into account and won't re-propose what you've already discarded.
