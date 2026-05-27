# SkMTEB: Slovak Massive Text Embedding Benchmark and Model Adaptation

**Authors:** Marek Šuppa, Andrej Ridzik, Daniel Hládek, Natália Kňažeková, Viktória Ondrejová  
**Affiliations:** Comenius University in Bratislava · Cisco Systems · Technical University of Košice · Kempelen Institute of Intelligent Technologies

## Abstract

SkMTEB is the first comprehensive MTEB-style text embedding benchmark for Slovak — a low-resource West Slavic language with ~5 million speakers. The benchmark comprises **31 datasets across 7 task types**, covering nearly 4× the depth of existing multilingual benchmark coverage for Slovak (compared to 8 tasks in MMTEB).

## Benchmark

The benchmark spans 7 task types:

| Task Type         | # Datasets | Description |
|-------------------|:----------:|-------------|
| Bitext Mining     | 6 | Cross-lingual parallel sentence alignment (Slovak–English, Slovak–Czech) |
| Classification    | 7 | Sentiment, hate speech, topic, party, and gender classification |
| Clustering        | 5 | Grouping news articles by topic, URL structure, and editorial category |
| Pair Classification | 3 | Natural language inference and textual entailment |
| Reranking         | 3 | Ranking candidate passages for a query (QA, pharmacy) |
| Retrieval         | 5 | Document retrieval from news, encyclopedic, and FAQ corpora |
| STS               | 2 | Semantic textual similarity scoring |

7 brand-new datasets were created specifically for this work. 6 datasets overlap with MMTEB; the remaining 25 are unique to SkMTEB, covering Slovak-specific domains (medical/pharmacy, fact-checking, parliamentary), temporal ranges (2000–2025), and task formulations (summarization-as-retrieval, URL-based clustering).

## Models

Two compact Slovak embedding models were developed using vocabulary trimming (VT) on Multilingual E5 and fine-tuning on curated Slovak data from the skLEP benchmark:

| Model | Parameters | Size reduction | SkMTEB avg |
|-------|:----------:|:--------------:|:----------:|
| `e5-sk-small` | 45M | −62% vs. mE5-small (118M) | 70.56 |
| `e5-sk-large` | 365M | −35% vs. mE5-large (560M) | 74.70 |

Both models are open-weight, locally deployable (no API required), and suitable for semantic search and RAG applications.

## Key Results

Evaluation of **31 embedding models** on SkMTEB reveals:

- **Best overall:** `multilingual-e5-large-instruct` (77.49), followed by `gemini-embedding-001` (77.23)
- **`e5-sk-small`** (45M) matches `text-embedding-3-small` (70.48 vs. 70.56) — a proprietary API — at a fraction of the size
- **`e5-sk-large`** (365M) is statistically equivalent to `text-embedding-3-large` (74.70 vs. 75.07; TOST 90% CI within ±2 pts)
- Large models (>1B) show diminishing returns: `jina-embeddings-v4` (3.8B, 72.44) trails `nomic-embed-text-v2-moe` (330M, 72.58)
- Existing Slovak NLU models (`slovakbert-*`) transfer poorly to embedding tasks
- Bitext mining is largely solved (F1 > 90 for most models); clustering remains the hardest task (V-measure 17–50)
- Vocabulary trimming preserves cross-lingual transfer: Slovak–English and Slovak–Czech bitext mining degrades by <1 F1 point

## Resources

| Resource | Link |
|----------|------|
| 📄 Paper (arXiv) | *(to be added)* |
| 🤗 Models & Datasets | [huggingface.co/collections/slovak-nlp/skmteb](https://huggingface.co/collections/slovak-nlp/skmteb) |
| 💻 Code | [github.com/slovak-nlp/skmteb](https://github.com/slovak-nlp/skmteb) |

## Citation

If you use SkMTEB in your work, please cite:

```bibtex
@inproceedings{suppa-etal-2025-skmteb,
  title     = {{SkMTEB}: {S}lovak Massive Text Embedding Benchmark and Model Adaptation},
  author    = {{\v{S}}uppa, Marek and Ridzik, Andrej and Hl{\'a}dek, Daniel and
               Kn{\v{a}}{\v{z}}ekov{\'a}, Nat{\'a}lia and Ondrejov{\'a}, Vikt{\'o}ria},
  booktitle = {Proceedings of ACL},
  year      = {2026},
}
```
