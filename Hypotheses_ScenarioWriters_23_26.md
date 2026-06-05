# Hypotheses — Chatbot Scenario Writers
## Role: Сценаристы чат-ботов (одна роль: JS-скрипты + NLU-данные)

**Generated:** June 4, 2026 · Week 23
**Source:** Market scan (June 2026)
**Access:** ✅ Warm — DL-0 and DL-2 team relationship established
**Active DLs on this role:** DL-0 (shipped — RegExp generation), DL-3 (in progress — script defect diagnosis), DL-4 (in progress — NLU utterance generation)

---

## Market signals used

| Signal | Source | Strength |
|---|---|---|
| LLM-based utterance generation for NLU training data — US patent granted 2024, Rasa ecosystem tooling | USPTO patent 12468938, Rasa docs | Strong |
| Conversational AI platforms adding automated test dialogue generation | Botpress, Rasa CALM 2025 | Medium |
| Self-healing and AI-assisted script maintenance mainstream in enterprise chatbot teams | Boost.ai 2025 Gartner Leader, IBM Watson 2025 | Medium |
| Intent quality scoring and NLU model evaluation tools emerging | Kore.ai, Botpress 2025 | Medium |
| Automated chatbot QA before deployment gaining traction | Botpress, Rasa CALM documentation 2025 | Medium |
| Synthetic conversation generation for edge-case testing | Research papers + enterprise tooling 2025 | Weak-Medium |

---

## ✅ Refined Top 3 (post-synthetic CustDev, June 4, 2026)

| # | Hypothesis | Why top 3 | Action |
|---|---|---|---|
| **1** | **H2 — Script defect diagnosis** | DL-3 active. 20% sprint waste confirmed from real DL-2 interviews. Diagnosis-only scope avoids DL-2 failure mode. Highest ICE (448). | In validation — see DL-3 |
| **2** | **H1 — NLU utterance generation** | DL-4 active. 1.5–2h/intent × 2–4 intents/sprint = 3–8h/sprint confirmed. DL-0 trust transfers directly. | In validation — see DL-4 |
| **3** | **H3 — Test dialogue generation** | Biweekly frequency (every sprint before release). Realistic if uses existing utterances as inputs — confirmed by persona. Natural extension of DL-4. | Open DL-5 after DL-4 validates |

**H4 note (intent conflict detection):** Valid hypothesis, no PII. Quarterly frequency = not sprint-level urgency. Revisit if team lead raises it, or bundle as a release-gate check rather than a sprint tool.

**Dropped (6 hypotheses):** H5 (structural gaps only, needs user data for real value), H6 (low impact — bundle with DL-3), H7 (high action cost, rare refactoring event), H8 (generic without model-specific knowledge), H9 (no sprint urgency), H10 (small pain, infrequent).

---

## All 10 Hypotheses (with verdicts)

---

### H1 — NLU utterance generation ★ (DL-4 active)
**Hypothesis:** Scenario writers will recover ≥10% sprint capacity if AI generates diverse NLU training utterances from intent description, reducing utterance-writing time from 1.5–2h to <30 min per intent.
**Market signal:** US Patent 12468938 (granted 2024): "Training example generation to create new intents for chatbots" — automated utterance generation from existing intent examples is a validated technical approach. Rasa ecosystem includes utterance augmentation tooling.
**ICE:** I=7, C=7, E=8 → **392**
**Status:** Being validated in DL-4. Do not open separately.

---

### H2 — Script defect root-cause diagnosis ★ (DL-3 active)
**Hypothesis:** Scenario writers will reduce script-fix time by ≥50% if AI identifies root cause of broken JS scripts from script + error log, without writing the fix.
**Market signal:** Self-healing test/script tools (Perfecto, Mabl) achieve 40–60% reduction in script maintenance. AI log analysis tools (Splunk AI, Datadog AI) used by enterprise dev teams to accelerate root cause investigation.
**ICE:** I=8, C=7, E=8 → **448**
**Status:** Being validated in DL-3. Do not open separately.

---

### H3 — Automated test dialogue generation
**Hypothesis:** Scenario writers will reduce chatbot QA time by ≥30% if AI generates structured test dialogues from existing scenario scripts and intent library, covering happy paths and edge cases.
**Market signal:** Botpress 2025: built-in test conversation generation from bot flows. Rasa CALM approach includes automated story generation. Enterprise chatbot teams shifting from manual to AI-generated test coverage.
**ICE:** I=6, C=5, A=8 → **240**
**Risk:** Test quality depends on realistic user inputs. AI-generated test inputs from existing intents may only test known patterns, missing genuinely novel user behaviour.

---

### H4 — Intent conflict and overlap detection
**Hypothesis:** Scenario writers will reduce production misrouting incidents if AI scans the intent library and flags overlapping/conflicting intent pairs before release.
**Market signal:** Kore.ai NLU training tools include intent health scoring. NLU platform vendors (Rasa, IBM Watson) offer intent overlap analysis as a built-in quality tool.
**ICE:** I=6, C=6, A=8 → **288**
**Risk:** Quarterly task, not sprint-level. Low adoption urgency unless bundled into release workflow as a mandatory pre-release check.

---

### H5 — Conversation flow completeness check
**Hypothesis:** Scenario writers will reduce user dead-end incidents if AI analyses dialogue flow and identifies paths where the bot has no response defined.
**Market signal:** Enterprise chatbot platforms (Botpress, Kore.ai) include visual flow analysers with gap detection. Missing dialogue paths are a documented source of chatbot failure in production.
**ICE:** I=5, C=5, A=8 → **200**
**Risk:** "Missing path" detection needs user behaviour data to know what paths are actually taken. Without conversation logs → can only detect structural gaps, not behavioural ones.

---

### H6 — Auto-generated script changelog
**Hypothesis:** Scenario writers will reduce documentation debt if AI auto-generates a changelog entry from the git diff of a script fix and appends it without human action.
**Market signal:** GitHub Copilot PR summaries, Sourcegraph Cody commit documentation — auto-commit documentation is an established pattern in enterprise dev teams.
**ICE:** I=4, C=5, A=8 → **160**
**Risk:** Zero-friction requirement (must be a git hook, not a manual step). Low impact — prevents future pain, doesn't recover current sprint time. Best as DL-3 phase 2 feature.

---

### H7 — Intent rationalization assistant
**Hypothesis:** Scenario writers will improve NLU model accuracy if AI clusters the intent library by semantic similarity and flags candidates for merging or splitting.
**Market signal:** NLU model governance is an emerging concern as intent libraries grow to 200+ intents. Rasa and IBM Watson documentation references intent proliferation as a known quality problem.
**ICE:** I=5, C=4, A=8 → **160**
**Risk:** Restructuring intents has downstream impact on routing logic and scripts — risky change, high effort to implement suggestions even when correct.

---

### H8 — Synthetic edge-case user input generation
**Hypothesis:** Scenario writers will catch more edge-case failures pre-production if AI generates a list of unusual/adversarial user inputs designed to break the chatbot's intent classification.
**Market signal:** Adversarial NLU testing is a research-documented technique. Enterprise chatbot teams at large banks use red-teaming for conversational AI. IBM Watson includes robustness testing tools.
**ICE:** I=6, C=4, A=8 → **192**
**Risk:** "Adversarial" inputs require knowing the failure modes of the specific NLU engine. Generic edge cases may not match the actual model's weak spots.

---

### H9 — Script refactoring opportunity flagging
**Hypothesis:** Scenario writers will reduce future maintenance burden if AI passively flags scripts that have grown too complex (high cyclomatic complexity, repeated logic) and suggests where refactoring would help.
**Market signal:** Static code analysis with AI recommendations (SonarQube AI, CodeClimate) standard practice in enterprise dev teams. Proactive tech debt management gaining traction in financial services IT.
**ICE:** I=4, C=5, A=8 → **160**
**Risk:** "Proactive" tooling has low adoption without sprint pressure. Scenario writers will not refactor scripts unless they're actively breaking. Low urgency.

---

### H10 — Chatbot release notes for business stakeholders
**Hypothesis:** Scenario writers will save 30–60 min per release if AI generates human-readable release notes for business stakeholders from the list of changed intents and scripts.
**Market signal:** AI-generated release notes from code changes (GitHub Copilot, Axolo) — established pattern. Business stakeholders in banks require plain-language change summaries before chatbot updates go live.
**ICE:** I=4, C=5, A=8 → **160**
**Risk:** Business stakeholders may require more context than a list of changed intents. The "what does this mean for users" framing requires judgment that AI may not provide reliably.

---

## Summary ranking

| # | Hypothesis | ICE | Access | Priority |
|---|---|---|---|---|
| H2 | Script defect diagnosis | 448 | ✅ | DL-3 active |
| H1 | Utterance generation | 392 | ✅ | DL-4 active |
| H4 | Intent conflict detection | 288 | ✅ | After DL-3/DL-4 |
| H3 | Test dialogue generation | 240 | ✅ | After H4 |
| H5 | Conversation flow completeness | 200 | ✅ | Needs user data caveat |
| H8 | Edge-case input generation | 192 | ✅ | Needs NLU expertise |
| H7 | Intent rationalization | 160 | ✅ | High effort, low urgency |
| H6 | Auto-changelog | 160 | ✅ | Bundle with DL-3 |
| H9 | Refactoring flagging | 160 | ✅ | No sprint urgency |
| H10 | Release notes for business | 160 | ✅ | Small pain |

---

*Sources: [USPTO Patent 12468938 — Utterance Generation](https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/12468938) · [Botpress Conversation Design 2026](https://botpress.com/blog/conversation-design) · [Boost.ai Conversational AI Trends](https://boost.ai/blog/conversational-ai-technology-trends/) · [Kore.ai Intent Design](https://www.kore.ai/blog/craft-successful-conversational-user-interfaces-align-user-intent-with-developed-intent)*
