🇪🇸 [Español](README.md) · 🇬🇧 **English**

# Applied AI portfolio with local LLMs

Hybrid RAG, structured extraction, classification, tool-using agents and verified summaries, all with local models and honest
evaluation.

**Main tools:** Ollama (qwen2.5:7b, bge-m3) · pydantic · FastAPI · Streamlit

Each folder is an independent project with its own README (results first), step-by-step guide, automated tests and
reproduction instructions. Raw data are not versioned: every project ships a script that downloads them from the official
source.

> 🌐 Each project has an English summary with its key results; the full documentation is in Spanish.

## Projects

| Project | What it is about |
|---|---|
| [**🌐 Open-data agent with tools: World Bank + Open-Meteo**](agente-datos-abiertos/README.en.md) | A local LLM answers questions about Latin American economy and climate by calling 5 tools. What the LLM decides and what the code does are measured separately: 95.0% correct on unseen questions |
| [**📨 Routing financial complaints: TF-IDF vs. embeddings vs. LLM, cascade and urgency**](clasificador-quejas-cfpb/README.en.md) | Is a local LLM needed to route complaints, or is TF-IDF + logistic regression enough? Measured on 50,568 real CFPB complaints with a temporal split |
| [**🧾 PDF invoice extraction to validated JSON (local LLM + Ecuador's SRI rules)**](extraccion-facturas-llm/README.en.md) | Digital, scanned or rotated Ecuadorian invoices turned into structured JSON, validated with business rules |
| [**⚖️ RAG assistant for Ecuador's labor law (hybrid search + re-ranking + refusal)**](rag-ley-laboral-ecuador/README.en.md) | Answers workers' questions citing the exact article of the Labor Code, and says it does not know when the law does not cover it |
| [**🔎 Aspect-based sentiment in Amazon reviews: rules vs. embeddings vs. local LLM**](resenas-sentimiento-aspectos/README.en.md) | What customers complain about and what it costs, comparing three approaches against 700 hand-labeled reviews |
| [**📊 Executive KPI summaries with every figure verified**](resumen-kpis-verificado/README.en.md) | A local LLM writes the economic summary of a country and an automatic verifier checks every number in the text |

## How to use this repository

```bash
git clone https://github.com/GUAR-NIX/PORTAFOLIO-IA.git
cd PORTAFOLIO-IA/<project>
```

Inside each project, follow the reproduction section of its README and `docs/GUIA_PASO_A_PASO.md` (Spanish).

## Author

**Erick Guarnizo** · [LinkedIn](https://www.linkedin.com/in/erick-g-571a7b3b4)

## License

Code is under the [MIT](LICENSE) license. Each project's data keep the license of their source, stated in its README.
