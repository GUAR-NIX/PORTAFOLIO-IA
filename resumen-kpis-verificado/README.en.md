🇪🇸 [Español (full version)](README.md) · 🇬🇧 **English (summary)**

# 📊 Executive KPI summaries with every figure verified

A local LLM (`qwen2.5:7b` on Ollama, CPU) writes, for management, the economic summary of a Latin American country from World
Bank indicators, and an **automatic verifier checks every number in the text** against a deterministic KPI layer: correct,
incorrect (with the real value) or without a source.

## Results (test: 12 reports for 2024)

| Approach | Figures | Hallucinated (95% CI) | Reports without any error | Coverage of findings (95% CI) | Misleading readings | Time per report |
|---|---:|---:|---:|---:|---:|---:|
| (a) Free-form LLM | 101 | 4.0% (1.1–6.8%) | 66.7% | 66.7% (56.2–77.1%) | 12 of 46 checked | 56 s |
| (b) Structured LLM | 99 | 6.1% (0.0–14.1%) | 83.3% | 81.2% (68.8–93.8%) | 15 of 44 checked | 144 s |
| **(c) (b) + verification and retry** | 97 | 3.1% (0.0–7.9%) | 91.7% | 81.2% (68.8–93.8%) | 13 of 42 checked | 230 s |
| (d) Deterministic template | 288 | 0.0% | 100.0% | 64.6% (54.2–72.9%) | 0 of 24 checked | < 1 s |

1. **The LLM hardly invents figures when it has the table in front of it.** With 12 reports, the differences in hallucination
   are **not significant** (the CIs overlap).
2. **The real problem is misleading readings with correct figures:** between 26.1% and 34.1% of the checkable qualitative
   readings are wrong, such as calling a change in current dollars "growth" when real GDP fell.
3. **Structured output improves coverage:** 81.2% of the essential findings vs. 66.7% in free text (+14.6 pp, CI 6.2 to 25.0).
4. **Verifying and retrying** raises error-free reports from 83.3% to 91.7%, at the cost of 1.50 calls per report.
5. **The deterministic template is never wrong** (288 figures, 0 errors) and reads almost as well as free text (3.62 vs. 3.71
   out of 5), but covers fewer findings.

**Recommendation:** for a report that goes to management, the template gives the reliable base; the LLM adds value when its text
passes **both** checks (figures and direction of comparisons).

**Architecture, method, figures and reproduction commands:** [full README (Spanish)](README.md). Commands are
language-independent.
