🇺🇸 **English** · 🇪🇸 [Español](README.es.md)

# Applied AI with local LLMs

Six projects that run on a PC without a GPU (Ollama, FastAPI, Streamlit). Each one compares the LLM with a simpler baseline and reports
when the baseline wins or ties.

| Project | Measured result | Code | Tests |
|---|---|---|---|
| [Tool-using agent over open data](agente-datos-abiertos/README.md) | **95.0%** correct on 60 unseen questions; rule-based router 60.0% | [code](agente-datos-abiertos/src/agente) | [tests](agente-datos-abiertos/tests) |
| [RAG over Ecuador's Labor Code](rag-ley-laboral-ecuador/README.md) | Cites the correct article in **87%** of the 100 main questions; Recall@5 **0.97** vs. 0.76 for BM25 | [code](rag-ley-laboral-ecuador/src/rag_laboral) | [tests](rag-ley-laboral-ecuador/tests) |
| [Invoice extraction to validated JSON](extraccion-facturas-llm/README.md) | **97.5%** exact fields vs. 81.8% for regex, on 50 synthetic invoices; ~2 min per invoice | [code](extraccion-facturas-llm/src/facturas) | [tests](extraccion-facturas-llm/tests) |
| [Complaint routing](clasificador-quejas-cfpb/README.md) | TF-IDF **0.825** Macro-F1 vs. 0.799 for the few-shot LLM: the cheap model is enough | [code](clasificador-quejas-cfpb/src/quejas) | [tests](clasificador-quejas-cfpb/tests) |
| [Aspect-based sentiment](resenas-sentimiento-aspectos/README.md) | Aspect detection F1 **0.739** (embeddings), 0.722 (rules), 0.688 (LLM) on 320 labeled reviews | [code](resenas-sentimiento-aspectos/src/resenas) | [tests](resenas-sentimiento-aspectos/tests) |
| [KPI summaries with checked figures](resumen-kpis-verificado/README.md) | Error-free reports from 83.3% to **91.7%** with verification and retry (12 reports) | [code](resumen-kpis-verificado/src/kpis) | [tests](resumen-kpis-verificado/tests) |

## Start here

| If you are looking for… | Go to |
|---|---|
| **The clearest engineering example** | [Open-data agent](agente-datos-abiertos/README.md): what the LLM decides and what the code does, measured separately |
| **An honest negative result** | [Complaint routing](clasificador-quejas-cfpb/README.md): the LLM does not beat a linear model |
| **How it is checked** | [CI workflow](.github/workflows/ci.yml): Ruff, Markdown links and the tests of the six projects, with the LLM replaced by test doubles |
| **Design and decisions** | The full README of each project (Spanish) has the architecture, limits and reproduction commands |

## How results were measured

- Where prompts or thresholds were tuned, the tuning set is separate from the test set; figures obtained after seeing the errors
  are marked as optimistic in their project.
- Intervals are 95% bootstrap or Wilson; sample sizes are in the tables.
- Differences whose intervals overlap are reported as not distinguishable.
- Models run on a local CPU; latencies belong to that machine.

## How to use this repository

```bash
git clone https://github.com/GUAR-NIX/PORTAFOLIO-IA.git
cd PORTAFOLIO-IA/<project>
```

Each project has its own README, tests and `docs/GUIA_PASO_A_PASO.md` (Spanish). Raw data are not versioned: a script gets them from
the official source. The English page of each project is a summary; the full documentation is in Spanish.
See [CONTRIBUTING.md](CONTRIBUTING.md) to run the checks.

## Author

**Erick Guarnizo** · [LinkedIn](https://www.linkedin.com/in/erick-g-571a7b3b4) · [GitHub profile](https://github.com/GUAR-NIX)

## License

Code is under the [MIT](LICENSE) license. Each project's data keep the license of their source, stated in its README.
