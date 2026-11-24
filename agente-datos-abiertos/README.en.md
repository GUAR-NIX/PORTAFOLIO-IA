🇪🇸 [Español (full version)](README.md) · 🇬🇧 **English (summary)**

# 🌐 Open-data agent with tools: World Bank + Open-Meteo

A local LLM (`qwen2.5:7b` on Ollama, CPU) answers questions about Latin American economy and climate by **calling 5 tools**
connected to the World Bank (WDI) and Open-Meteo (ERA5). The project measures separately **what the LLM decides** (which tool,
with which arguments, when to abstain) and **what the code does** (validate, verify, execute and write).

## Results

| | Validation (44) | **Unseen test (60)** |
|---|---:|---:|
| Correct agent answer (95% CI) | 93.2% (0.84–1.00) | **95.0% (0.88–1.00)** |
| The LLM picks exactly the right tools (in-domain questions) | 94.4% | 95.5% |
| The LLM picks exactly the right tools **and** arguments | 86.1% | 95.5% |
| Correct abstention out of domain (95% CI, Wilson) | 100.0% (0.68–1.00) | 100.0% (0.81–1.00) |
| … of those, the LLM abstained **on its own**, without the code | 37.5% | 56.2% |
| LLM turns per question (mean) | 2.11 | 1.95 |
| Mean latency per question (CPU) | 49.2 s | 31.6 s |

Baselines on the test set: LLM without tools **23.3%**, rule-based router **60.0%**, text ReAct **46.7%**.

## Design mistakes I found and fixed

Measuring a tool-using agent is easy to do badly:

- **Overfitting to the benchmark.** A "guardrail" made of the literal words of the trick questions gives a high number that
  means nothing. Here there are no topic lists: the rules derive from what the tools can do.
- **The code must not overwrite the LLM.** If a regex replaces the model's arguments, what is measured is the code. Here what
  the LLM proposes is executed.
- **Tautological faithfulness.** The final answer comes from a template, so its faithfulness is by construction and is **not
  presented as the model's merit**.
- **Separate validation and test.** The 44 validation questions tune everything; the 60 test questions are run only once.

**Full results, ablations, architecture and reproduction commands:** [full README (Spanish)](README.md). Commands are
language-independent.
