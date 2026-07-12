# rag-eval-bench

> **Archived** — active development is in **[rag-system](https://github.com/vedantrazjpurohit-create/rag-system)**.

**A reproducible RAG evaluation harness** — ingest docs, run retrieval, score recall@k, MRR, nDCG, faithfulness, and latency on a fixed corpus.

Answers one question: *does my retrieval actually help, or am I just paying for embeddings?* Every experiment is a YAML config diff, not a code fork.

## What it does

- Ingests markdown/PDFs with configurable chunk size and overlap
- Indexes with ChromaDB + sentence-transformers
- Scores retrieval (recall@k, MRR, nDCG) and generation (faithfulness, citation coverage)
- Writes `results/run_<timestamp>.json` you can diff across changes

## Quick start

```bash
python -m venv .venv && .venv\Scripts\activate
pip install -r requirements.txt
python scripts/run_eval.py --config configs/default.yaml
```

```json
{
  "metrics": {
    "retrieval.recall_at_k": 0.5,
    "retrieval.mrr": 0.5,
    "gen.faithfulness": 0.8,
    "latency.p95_ms": 16.8
  }
}
```

**Stack:** Python 3.11 · ChromaDB · sentence-transformers · pytest

**Successor:** [rag-system](https://github.com/vedantrazjpurohit-create/rag-system) merges this bench with the API, adds BM25/hybrid fusion, query routing, and live `/eval`.