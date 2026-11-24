🇪🇸 [Español (full version)](README.md) · 🇬🇧 **English (summary)**

# 📨 Routing financial complaints: TF-IDF vs. embeddings vs. LLM, cascade and urgency

Is a **local LLM** needed to route financial complaints to the right desk, or is **TF-IDF + logistic regression** enough? This
project measures it on **50,568 real CFPB complaints** (Consumer Financial Protection Bureau, USA; original texts in English)
with a **temporal split** (train on old complaints, test on recent ones), compares 5 approaches and 2 cascades **on the same
300 complaints**, detects **urgency** and tests transfer to **Spanish**. Everything runs locally on CPU with Ollama
(`qwen2.5:7b`, `bge-m3`), with a FastAPI API and a Streamlit app.

## Conclusions

1. **Without examples the LLM clearly loses; with 6 examples it is on par with the cheap classifiers, without beating them.**
   On the same 300 recent complaints (Macro-F1): TF-IDF + LR **0.825** (95% CI 0.779–0.865), zero-shot LLM **0.695**
   (0.643–0.742), few-shot LLM **0.799** (0.754–0.842). TF-IDF's edge over few-shot (+0.027, CI −0.022 to 0.075) is **not
   distinguishable** with 300 complaints; what is clear is that TF-IDF takes 0.10 ms per complaint and the LLM 12.3 s.
2. **Why zero-shot fails:** it sends to "credit reporting" complaints that the CFPB filed elsewhere, because collection and
   card complaints often mention the credit report.
3. **The cascade makes nothing worse and may help a little, but that is not proven.** 23.3% of complaints reach the LLM; the
   few-shot cascade gets 0.842 (0.799–0.880) vs. 0.825 for TF-IDF alone (+0.017, CI −0.018 to 0.051).
4. **Temporal drift is real and measurable:** the same TF-IDF drops from 0.846 (same period as training) to 0.774 on recent
   complaints (−0.072, CI −0.087 to −0.056). A random split would have overestimated production performance.
5. **With few labels, embeddings; with hundreds, TF-IDF is enough.** With 10 examples per desk, bge-m3 + LR gets 0.703 and
   TF-IDF 0.635; with 300 per desk, 0.798 vs. 0.820.
6. **Urgency: no detector is good yet.** On the 10,770 recent complaints, TF-IDF + LR gets F1 0.407 (precision 46.8%, recall
   36.0%).
7. **Spanish:** on 60 real translated complaints, TF-IDF drops from 52 to 29 correct (its vocabulary is English), bge-m3 + LR
   from 49 to 42 and the few-shot LLM from 48 to 43.

**Architecture, all tables and figures, limitations and reproduction commands:** [full README (Spanish)](README.md). Commands
are language-independent.
