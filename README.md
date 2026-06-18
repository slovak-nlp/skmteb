# SkMTEB: Slovak Massive Text Embedding Benchmark and Model Adaptation

**Authors:** Marek Šuppa, Andrej Ridzik, Daniel Hládek, Natália Kňažeková, Viktória Ondrejová  
**Affiliations:** Comenius University in Bratislava · Cisco Systems · Technical University of Košice · Kempelen Institute of Intelligent Technologies

## Abstract

SkMTEB is the first comprehensive MTEB-style text embedding benchmark for Slovak — a low-resource West Slavic language with ~5 million speakers. The benchmark comprises **31 datasets across 7 task types**, covering nearly 4× the depth of existing multilingual benchmark coverage for Slovak (compared to 8 tasks in MMTEB).

## Resources

| Resource | Link |
|----------|------|
| 📄 Paper (arXiv) | [arxiv.org/abs/2606.13647](https://arxiv.org/abs/2606.13647) |
| 🤗 Models & Datasets | [huggingface.co/collections/slovak-nlp/skmteb](https://huggingface.co/collections/slovak-nlp/skmteb) |
| 💻 Code | TBD: Part of MMTEB |

## Usage

Install [MTEB](https://github.com/embeddings-benchmark/mteb):

```bash
pip install mteb
```

Evaluate a model on the full SkMTEB benchmark:

```python
import mteb

model = mteb.get_model("slovak-nlp/e5-sk-small")
tasks = mteb.get_benchmark("SkMTEB")
evaluation = mteb.MTEB(tasks=tasks)
results = evaluation.run(model, output_folder="results/")
```

To evaluate on specific task types only:

```python
tasks = mteb.get_tasks(task_types=["Retrieval", "Classification"], languages=["slk"])
evaluation = mteb.MTEB(tasks=tasks)
results = evaluation.run(model, output_folder="results/")
```

## Models

Two compact Slovak embedding models were developed using vocabulary trimming (VT) on Multilingual E5 and fine-tuning on curated Slovak data from the skLEP benchmark:

| Model | Parameters | Size reduction | SkMTEB avg |
|-------|:----------:|:--------------:|:----------:|
| `e5-sk-small` | 45M | −62% vs. mE5-small (118M) | 70.56 |
| `e5-sk-large` | 365M | −35% vs. mE5-large (560M) | 74.70 |

Both models are open-weight, locally deployable (no API required), and suitable for semantic search and RAG applications.


## Datasets

> ⭐ marks the **7 brand-new datasets** created specifically for this work.

### Retrieval

| Dataset | HuggingFace |
|---------|-------------|
| SKQuadRetrieval | [TUKE-KEMT/retrieval-skquad](https://huggingface.co/datasets/TUKE-KEMT/retrieval-skquad) |
| SlovakSumRetrieval | [NaiveNeuron/slovaksum](https://huggingface.co/datasets/NaiveNeuron/slovaksum) |
| SMESumRetrieval | [NaiveNeuron/SMESum](https://huggingface.co/datasets/NaiveNeuron/SMESum) |
| BelebeleRetrieval | [facebook/belebele](https://huggingface.co/datasets/facebook/belebele) |
| WebFAQRetrieval | [mteb/WebFAQRetrieval](https://huggingface.co/datasets/mteb/WebFAQRetrieval) |

### Reranking

| Dataset | HuggingFace |
|---------|-------------|
| SkQuadReranking | [TUKE-KEMT/reranking-skquad](https://huggingface.co/datasets/TUKE-KEMT/reranking-skquad) |
| ⭐ SlovakPharmacyDrMaxReranking | [slovak-nlp/slovak-pharmacy-drmax-reranking](https://huggingface.co/datasets/slovak-nlp/slovak-pharmacy-drmax-reranking) |
| ⭐ SlovakPharmacyMojaLekarenReranking | [slovak-nlp/slovak-pharmacy-mojalekaren-reranking](https://huggingface.co/datasets/slovak-nlp/slovak-pharmacy-mojalekaren-reranking) |

### Classification

| Dataset | HuggingFace |
|---------|-------------|
| SlovakHateSpeechClassification.v2 | [mteb/slovak\_hate\_speech](https://huggingface.co/datasets/mteb/slovak_hate_speech) |
| SlovakMovieReviewSentimentClassification.v2 | [mteb/slovak\_movie\_review\_sentiment](https://huggingface.co/datasets/mteb/slovak_movie_review_sentiment) |
| SIB200Classification | [mteb/sib200](https://huggingface.co/datasets/mteb/sib200) (subset: slk\_Latn) |
| MultilingualSentimentClassification | [mteb/multilingual-sentiment-classification](https://huggingface.co/datasets/mteb/multilingual-sentiment-classification) (subset: slk) |
| SlovakParlaSentClassification | [classla/ParlaSent](https://huggingface.co/datasets/classla/ParlaSent) (subset: SK) |
| MultiEupSlovakPartyClassification | [unimelb-nlp/MultiEup-v2](https://huggingface.co/datasets/unimelb-nlp/MultiEup-v2) |
| MultiEupSlovakGenderClassification | [unimelb-nlp/MultiEup-v2](https://huggingface.co/datasets/unimelb-nlp/MultiEup-v2) |

### Clustering

| Dataset | HuggingFace |
|---------|-------------|
| SIB200ClusteringS2S | [mteb/sib200](https://huggingface.co/datasets/mteb/sib200) (subset: slk\_Latn) |
| ⭐ PravdaSKTagClustering | [NaiveNeuron/pravda-sk-tag-clustering](https://huggingface.co/datasets/NaiveNeuron/pravda-sk-tag-clustering) |
| ⭐ PravdaSKURLClustering | [NaiveNeuron/pravda-sk-url-clustering](https://huggingface.co/datasets/NaiveNeuron/pravda-sk-url-clustering) |
| SlovakSumURLClustering | [kiviki/slovaksum-url-clustering](https://huggingface.co/datasets/kiviki/slovaksum-url-clustering) |
| SMESumCategoryClustering | [NaiveNeuron/SMESum](https://huggingface.co/datasets/NaiveNeuron/SMESum) |

### Bitext Mining

| Dataset | HuggingFace |
|---------|-------------|
| OpusSlovakEnglishBitextMining | [Helsinki-NLP/opus-100](https://huggingface.co/datasets/Helsinki-NLP/opus-100) (subset: en-sk) |
| TatoebaBitextMining | [mteb/tatoeba-bitext-mining](https://huggingface.co/datasets/mteb/tatoeba-bitext-mining) (subset: slk-eng) |
| FloresBitextMining | [mteb/FloresBitextMining](https://huggingface.co/datasets/mteb/FloresBitextMining) (subsets: eng\_Latn-slk\_Latn, ces\_Latn-slk\_Latn) |
| NTREXBitextMining | [mteb/NTREXBitextMining](https://huggingface.co/datasets/mteb/NTREXBitextMining) (subsets: eng\_Latn-slk\_Latn, ces\_Latn-slk\_Latn) |
| WebFAQBitextMiningQuestions | [PaDaS-Lab/webfaq-bitexts](https://huggingface.co/datasets/PaDaS-Lab/webfaq-bitexts) (subsets: eng-slk, ces-slk) |
| WebFAQBitextMiningQAs | [PaDaS-Lab/webfaq-bitexts](https://huggingface.co/datasets/PaDaS-Lab/webfaq-bitexts) (subsets: eng-slk, ces-slk) |

### Pair Classification

| Dataset | HuggingFace |
|---------|-------------|
| ⭐ SlovakNLI | [natalia-nk/NLI-SK-annotated](https://huggingface.co/datasets/natalia-nk/NLI-SK-annotated) |
| SlovakRTE | [slovak-nlp/sklep](https://huggingface.co/datasets/slovak-nlp/sklep) (subset: rte) |
| ⭐ DemagogSKNLI | [NaiveNeuron/DemagogSK](https://huggingface.co/datasets/NaiveNeuron/DemagogSK) |

### Semantic Textual Similarity

| Dataset | HuggingFace |
|---------|-------------|
| SlovakSTS | [slovak-nlp/sklep](https://huggingface.co/datasets/slovak-nlp/sklep) (subset: sts) |
| ⭐ SlovakSumSTS | [slovak-nlp/slovak-sts-synthetic](https://huggingface.co/datasets/slovak-nlp/slovak-sts-synthetic) |


## Citation

If you use SkMTEB in your work, please cite:

```bibtex
@inproceedings{suppa-etal-2025-skmteb,
  title     = {{SkMTEB}: {S}lovak Massive Text Embedding Benchmark and Model Adaptation},
  author    = {{\v{S}}uppa, Marek and Ridzik, Andrej and Hl{\'a}dek, Daniel and
               Kn{\v{a}}{\v{z}}ekov{\'a}, Nat{\'a}lia and Ondrejov{\'a}, Vikt{\'o}ria},
  booktitle = {Proceedings of ACL},
  year      = {2026},
  eprint    = {2606.13647},
  archivePrefix = {arXiv},
  url       = {https://arxiv.org/abs/2606.13647},
}
```
