# GENESIS VDSI Analysis

BERTopic-based discourse analysis and the **Validated-Discourse Similarity Index (VDSI)**, applied to the UN GENESIS WP4 Multistakeholder Partnerships Database. This repository contains the companion code for the manuscript submitted to *Sustainability* (MDPI).

## Overview

This project examines whether discourse patterns distinguish independently **validated** (Checked-In) from **non-validated** (Checked-Out) multistakeholder partnerships registered on the UN Partnership Platform. Using neural topic modeling (BERTopic) and a novel similarity-based index (VDSI), we test:

- Whether unvalidated projects employ language resembling validated-partnership discourse ("Discourse Surplus")
- Whether structural features (partner count, SDG scope, description length, duration) discriminate validation status
- Whether these patterns hold after adjusting for topic assignment and language

**Corpus:** N = 3,807 project descriptions (153 validated, 3,654 non-validated)
**Methods:** Sentence-BERT embeddings → UMAP → HDBSCAN → BERTopic; leave-one-out cosine similarity (VDSI); Mann–Whitney U tests; multivariable logistic regression; multi-seed/multi-parameter robustness checks.

## Repository Structure
genesis-vdsi-analysis/
├── GENESIS_mdpi_sustainability.ipynb   # Main analysis notebook (Google Colab)
├── data/                               # GENESIS WP4 source data
├── outputs/                            # Generated tables (CSV) and figures (PNG)
├── checkpoints/                        # Cached intermediate results (embeddings, models, stats)
├── LICENSE
└── README.md
## How to Run

1. Open `GENESIS_mdpi_sustainability.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Mount your Google Drive when prompted (the notebook uses Drive to cache checkpoints across sessions).
3. Run cells sequentially from top to bottom. Each analysis section checks for an existing checkpoint before recomputing, so re-running the notebook after an interruption resumes rather than restarting from scratch.
4. Outputs (tables as CSV, figures as PNG) are written to the `outputs/` folder as each section completes.

**Note on reproducibility:** topic modeling with BERTopic/UMAP/HDBSCAN involves several sources of run-to-run non-determinism (parallel nearest-neighbor search, multi-threaded BLAS operations, and BERTopic's automatic topic-count selection). This notebook pins the target topic count explicitly (`nr_topics = TARGET_N_TOPICS`) and forces single-threaded execution at several levels specifically to ensure stable, reproducible results — see the notes in Section 1 (Installation & Setup) and Section 7 (BERTopic Topic Modelling) for details. Section 22–23 report formal multi-seed and multi-parameter robustness checks.

## Dependencies

Key packages (see the notebook's install cell for exact versions):
- `bertopic`, `umap-learn`, `hdbscan`
- `sentence-transformers` (`all-MiniLM-L6-v2`)
- `scikit-learn`, `statsmodels`, `scipy`, `pandas`, `numpy`
- `matplotlib`

## Data

The GENESIS WP4 Database on Multistakeholder Partnerships for Sustainable Development is derived from the UN Partnership Platform's public registry. See `data/` for the version used in this analysis.

## Citation

If you use this code or the VDSI methodology, please cite:

> [Author names]. (2026). [Manuscript title]. *Sustainability*. [DOI to be added upon publication]

## License

Code is released under the MIT License (see `LICENSE`). Data usage is subject to the original terms of the GENESIS WP4 Database / UN Partnership Platform.

## Contact

Questions about the analysis or code can be directed to umit.yilmaz@btu.edu.tr
