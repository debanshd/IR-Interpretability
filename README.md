# Beyond the Vector Black Box: Toward Interpretable Semantic Resonance in Neural Information Retrieval

[![Conference](https://img.shields.io/badge/SIGIR-2026-blue)](https://sigir.org/)
[![License](https://img.shields.io/badge/License-Apache_2.0-green.svg)](LICENSE)

**Authors:** Vinay Venkatesh (Google), Debanshu Das (Google), Surbhi Motghare (Salesforce)

This repository contains the code and reproducibility resources for the paper **"Beyond the Vector Black Box: Toward Interpretable Semantic Resonance in Neural Information Retrieval"**, accepted at **SIGIR '26**.

## Abstract

The rapid adoption of dense retrieval and Large Language Model (LLM) embeddings has shifted Information Retrieval (IR) from transparent lexical matching to opaque, high-dimensional latent space representations. While these neural models excel at capturing deep semantic nuance, they introduce a critical operational bottleneck: the loss of deterministic control and explainable relevance. In production environments, the inability to diagnose why a model exhibits semantic drift creates a significant trust deficit.

We argue that optimizing exclusively for offline ranking performance ignores the practical necessity for diagnostic clarity and user-in-the-loop steerability. This paper proposes **Interpretable Semantic Resonance (ISR)**, a novel framework bridging the gap between opaque neural embeddings and deterministic search requirements. By prioritizing *Controllability* and *Diagnostic Traceability* via **Sparse Autoencoders (SAEs)**, we decompose dense vectors into human-interpretable semantic facets. Our evaluation across five diverse BEIR benchmarks demonstrates that ISR maintains competitive zero-shot retrieval performance against state-of-the-art sparse and dense baselines while enabling unprecedented real-time latent steerability.

## Repository Contents

*   **`notebooks/Neural_IR_Interpretability_Framework.ipynb`**: The primary research notebook containing:
    *   **ISR Architecture**: Implementation of the Sparse Bottleneck Layer and training loop.
    *   **Experimental Pipeline**: End-to-end evaluation on BEIR datasets (SciDocs, ArguAna, NFCorpus, FiQA, TREC-COVID).
    *   **Ablation Studies**: Analysis of hyperparameter tradeoffs ($\lambda_{L1}$, $\lambda_{IP}$).
    *   **Results**: Pre-computed outputs demonstrating the performance metrics reported in the paper.

## Key Results

Our framework (ISR) introduces interpretability and steerability with minimal degradation in retrieval accuracy (NDCG).

### Table 1: Retrieval, Controllability, and Hardware Footprint
*Statistical significance (p-value) tested against Contriever baseline.*

| Dataset | Model | NDCG@10 | DTS (%) | MCI | p-value | Zero-Vals (%) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Scidocs** | Contriever (Dense) | 0.5615 | 1.0 | N/A | - | 0.0% |
| | ColBERTv2.0 | 0.6105 | 5.0 | N/A | 0.168 (ns) | 0.0% |
| | SPLADE (Sparse) | 0.5979 | 14.5 | N/A | 0.325 (ns) | 99.4% |
| | **ISR-Contriever** | **0.5610** | **28.0** | **8.5** | **0.958 (ns)** | **96.5%** |
| **ArguAna** | Contriever (Dense) | 0.4628 | 15.0 | N/A | - | 0.0% |
| | **ISR-Contriever** | 0.4390 | **41.5** | **4.0** | 0.148 (ns) | 96.9% |
| **Nfcorpus** | Contriever (Dense) | 0.5928 | 0.0 | N/A | - | 0.0% |
| | **ISR-Contriever** | 0.5300 | **45.5** | **9.0** | 0.006 (**) | 97.5% |
| **Fiqa** | Contriever (Dense) | 0.6141 | 1.0 | N/A | - | 0.0% |
| | **ISR-Contriever** | 0.6201 | **36.0** | **6.0** | 0.642 (ns) | 96.4% |
| **Trec-covid** | Contriever (Dense) | 0.3441 | 18.5 | N/A | - | 0.0% |
| | **ISR-Contriever** | 0.3563 | **95.5** | **10.0** | 0.806 (ns) | 99.5% |

**Metrics:**
*   **DTS (Diagnostic Traceability Score)**: % of top-10 docs where the primary facet matches the query's intent.
*   **MCI (Mean Correction Interactions)**: Average steps to steer a relevant document into the top-10 via facet sliders.

## Installation & Usage

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/debanshd/IR-Interpretability.git
    cd IR-Interpretability
    ```

2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
    *Note: Requires `torch`, `sentence-transformers`, `beir`, `numpy`, `scipy`.*

3.  **Run the Notebook:**
    Launch Jupyter Lab or Notebook and open `notebooks/Neural_IR_Interpretability_Framework.ipynb` to reproduce the experiments.

## Citation

If you use this code or findings in your research, please cite our SIGIR '26 paper:

```bibtex
@inproceedings{venkatesh2026beyond,
  title={Beyond the Vector Black Box: Toward Interpretable Semantic Resonance in Neural Information Retrieval},
  author={Venkatesh, Vinay and Das, Debanshu and Motghare, Surbhi},
  booktitle={Proceedings of the 49th International ACM SIGIR Conference on Research and Development in Information Retrieval},
  year={2026},
  publisher={ACM},
  address={Melbourne, Australia},
  doi={XXXXXXX.XXXXXXX}
}
```

## Statement of AI Use
The authors acknowledge the use of Gemini AI to refine the text and generate the images included in the paper (and this README).
