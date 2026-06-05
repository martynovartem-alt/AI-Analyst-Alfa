# Hypotheses — Data Analysts
## Role: Аналитики данных (DL-1 team + new analyst teams in bank)

**Generated:** June 4, 2026 · Week 23
**Source:** Market scan (June 2026)
**Access:** ✅ Warm — DL-1 team relationship established
**Active DLs on this role:** DL-1 (shipped), DL-3 (in progress — recurring report automation)

---

## Market signals used

| Signal | Source | Strength |
|---|---|---|
| Text-to-SQL copilots now mainstream in enterprise analytics | Deloitte 2025, JPMorgan LLM Suite 200k+ users | Strong |
| AI-Highlights cut executive summary prep time by 90% | Autonmis, ThoughtSpot 2025 | Strong |
| BI platforms (Power BI, Tableau, Looker) embedding AI narrative summaries | Multiple 2025 reports | Strong |
| Anomaly detection + root cause analysis automation gaining traction | Databricks blog 2026, DBS case study | Strong |
| Text-to-SQL + automated reporting saving analysts 20–30% time | Cross-industry, 2025 | Medium |
| Predictive trend identification before human review | Hex, ThoughtSpot 2025 | Medium |

---

## ✅ Refined Top 3 (post-synthetic CustDev, June 4, 2026)

| # | Hypothesis | Why top 3 | Action |
|---|---|---|---|
| **1** | **H4 — DL-1 expansion to new analyst teams** | Tool already built. Known 20% sprint recovery. One interview confirms or kills. Fastest ROI. | Book interview with any other analyst team lead |
| **2** | **H2 — Anomaly investigation brief** | Confirmed in synthetic CustDev. 2–3 alerts/week × 30–60 min = 3h/week. DL-1 team warm. Starting-point framing survives "hallucination" objection. | Open DL-5 after DL-3 validates |
| **3** | **H1 — Recurring report auto-refresh** | DL-3 active. 3–5h/week confirmed real. Review step doesn't disappear but 75% time reduction still significant. | In validation — see DL-3 |

**Dropped (7 hypotheses):** H3 (writing ownership + context gap), H5 (chronic not acute), H6 (alert fatigue + Power BI already does this), H7 (domain context gap), H8 (wrong approval chain), H9 (low frequency + ownership), H10 (duplicate of H1).

---

## All 10 Hypotheses (with verdicts)

---

### H1 — Recurring report auto-refresh ★ (DL-3 active)
**Hypothesis:** Data analysts will recover 3–5h/week if AI auto-refreshes recurring reports (data pull → template fill → anomaly flag), so they review instead of rebuild.
**Market signal:** AI report automation tools (Autonmis, Coupler.io) reduce recurring report preparation by 60–80%.
**ICE:** I=7, C=6, A=9 → **378**
**Status:** Being validated in DL-3. Do not open separately.

---

### H2 — Anomaly investigation brief ★ (DL-4 candidate)
**Hypothesis:** Data analysts will save 30–60 min per anomaly alert if AI drafts a starting-point brief (what changed, possible causes ranked by likelihood) when an anomaly fires.
**Market signal:** DBS case study — analysts resolved ⅓ more alerts in the same time after AI investigation assist. AI anomaly explanation tools cut MTTD for data issues.
**ICE:** I=6, C=7, A=9 → **378**
**Note:** Confirmed in synthetic CustDev (run 2). Next candidate after DL-3 validates.

---

### H3 — Executive summary auto-generation
**Hypothesis:** Data analysts will save 1–2h per analysis cycle if AI drafts the narrative summary for stakeholder reports from structured data + delta vs. prior period.
**Market signal:** AI-Highlights feature in Autonmis/ThoughtSpot cut executive summary preparation by up to 90%. Power BI Copilot generates narrative summaries from dashboards.
**ICE:** I=6, C=6, A=9 → **324**
**Risk:** Analyst adds contextual knowledge (events, market conditions) that AI can't infer — output will be incomplete without enrichment step.

---

### H4 — DL-1 expansion to new analyst teams
**Hypothesis:** Other analytics teams in the bank will expand sprint capacity by ~20% if given access to the Text→SQL pipeline already running for the DL-1 team.
**Market signal:** JPMorgan rolled out LLM Suite to 200,000+ employees. Enterprise-wide Text→SQL deployment is proven at scale. DBS 430+ AI use cases — reuse is core strategy.
**ICE:** I=8, C=9, A=5 → **360**
**Note:** Tool already built. One interview with another team lead confirms or kills. Schema onboarding = 1–2 dev days per team.

---

### H5 — SQL query explanation for documentation
**Hypothesis:** Data analysts will reduce handoff friction if AI generates plain-language explanations of complex SQL queries immediately after writing them.
**Market signal:** Text-to-SQL copilots mainstream → creates new problem: AI-written SQL is often harder to document than human-written. Tools like Databricks Assistant and dbt Assistant include auto-documentation features.
**ICE:** I=5, C=6, A=9 → **270**
**Risk:** Pain is chronic (handoffs), not acute (sprint). Adoption depends on zero-friction integration into existing workflow.

---

### H6 — Risk-based data quality pre-check
**Hypothesis:** Data analysts will reduce stakeholder correction cycles if AI validates data quality (completeness, outliers, schema drift) before a report is sent.
**Market signal:** BI platforms increasingly include automated data quality checks. Tableau Pulse, Power BI anomaly detection flag issues before human review.
**ICE:** I=6, C=5, A=9 → **270**
**Risk:** "Quality check" scope is broad. Need to narrow to one specific check type that causes most correction cycles (e.g. outlier detection, null values in key metrics).

---

### H7 — Predictive trend pre-highlight
**Hypothesis:** Data analysts will produce higher-value insights faster if AI pre-identifies top 3 statistically significant trends in a dataset before the analyst opens it.
**Market signal:** ThoughtSpot Sage and Hex AI Notebooks surface auto-insights before analyst interaction. 2025 data: analysts using AI pre-highlights complete insight reports 40% faster.
**ICE:** I=6, C=5, A=9 → **270**
**Risk:** "Significant" is domain-subjective. Bank analysts may distrust algorithmic trend selection — needs human confirmation step.

---

### H8 — Ad-hoc stakeholder query answering
**Hypothesis:** Data analysts will reduce interruptions from stakeholder data requests if a self-service natural language query layer (DL-1 style) is exposed directly to business stakeholders.
**Market signal:** JPMorgan, Goldman Sachs, Citi — all moving toward self-service analytics for business users. Microsoft Copilot for Finance embeds NL query into Excel/Teams for non-technical users.
**ICE:** I=8, C=7, A=4 → **224**
**Risk:** This is a stakeholder-facing product, not an analyst tool. Requires data governance approval. Different stakeholder buy-in chain than analyst tools.

---

### H9 — Analysis narrative for presentations
**Hypothesis:** Data analysts will save 30–45 min per presentation if AI drafts slide narrative text from analysis results and key metrics.
**Market signal:** Microsoft Copilot for PowerPoint generates slide content from data. Gamma.app and similar tools generate data-driven presentations from prompts. Growing adoption in enterprise analytics teams.
**ICE:** I=5, C=5, A=9 → **225**
**Risk:** Presentation style is personal. "I'll rewrite it anyway" friction applies. Stronger if framed as "bullet point drafts" not "full slide text."

---

### H10 — Sprint analytics retrospective
**Hypothesis:** Data analysts will surface sprint-level insights faster if AI generates a weekly "what changed in our key metrics" summary automatically every Monday from the same data sources.
**Market signal:** Automated weekly business digests are a mature category (Metabase subscriptions, Tableau Pulse weekly snapshots). Banks adopting automated metric digests to replace manual weekly standups.
**ICE:** I=5, C=6, A=9 → **270**
**Risk:** Overlaps with H1 (recurring report). Difference: H1 is about updating a template; H10 is about a proactive unsolicited AI insight push. May feel like noise if not well-tuned.

---

## Summary ranking

| # | Hypothesis | ICE | Access | Priority |
|---|---|---|---|---|
| H4 | DL-1 expansion to new teams | 360 | ~New team | High — tool exists |
| H1 | Recurring report auto-refresh | 378 | ✅ | DL-3 active |
| H2 | Anomaly investigation brief | 378 | ✅ | Next after DL-3 |
| H3 | Executive summary generation | 324 | ✅ | After H2 |
| H5 | SQL query explanation | 270 | ✅ | Low urgency |
| H6 | Data quality pre-check | 270 | ✅ | Needs scoping |
| H7 | Predictive trend highlight | 270 | ✅ | Needs scoping |
| H10 | Sprint analytics retrospective | 270 | ✅ | Overlaps H1 |
| H9 | Analysis narrative | 225 | ✅ | Low urgency |
| H8 | Stakeholder self-service queries | 224 | New stakeholders | Different buy-in chain |

---

*Sources: [Deloitte AI in Bank Software Development](https://www.deloitte.com/us/en/insights/industry/financial-services/financial-services-industry-predictions/2025/ai-and-bank-software-development.html) · [Databricks Data & AI Trends 2026](https://www.databricks.com/blog/8-ai-and-data-trends-shaping-financial-services-2026) · [Autonmis AI Reporting Tools](https://autonmis.com/learning/ai-data-analyst-tools-for-automated-reporting) · [Domo AI Data Analysis Tools](https://www.domo.com/learn/article/ai-data-analysis-tools)*
