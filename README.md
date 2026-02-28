# Assignment 2 — Text Clustering (PubMed Abstracts)

This repository contains an end-to-end **text clustering** pipeline that:
1) collects biomedical abstracts from **PubMed**,  
2) preprocesses and standardizes text length,  
3) builds multiple feature representations,  
4) runs multiple clustering algorithms,  
5) evaluates clusters against human labels, and  
6) performs error analysis + visualizations.

---

## Project Summary

- **Dataset:** 1,000 PubMed records (Title + Abstract), years **2010–2026**
- **Classes (balanced):** 200 per label
  - **a:** Type 2 Diabetes (T2D)  
  - **b:** Thyroid Disorders  
  - **c:** Bone Density / Osteoporosis  
  - **d:** PCOS  
  - **e:** Pituitary Adenomas  
- **Text length rule:** keep docs with **≥130 words**, truncate to **150 words**
- **Preprocessing:** lowercase → remove punctuation/numbers → stopwords → lemmatization
- **Features compared:** BoW, TF‑IDF, LDA, Doc2Vec
- **Algorithms compared:** KMeans, EM/GMM, Hierarchical (Ward)
- **Evaluation:** Silhouette + Cohen’s Kappa (after Hungarian alignment)
- **Best model (final):** **TF‑IDF + KMeans** (Kappa **0.7363**, Silhouette **0.0318**)

---

## Repository Contents

```
Clustering.ipynb                    # Main notebook (data collection → results)
Project Report-Assignment 2-2.docx  # Final report
README.md                           # This file
Group 1 - [Clustering].pptx.        # Project presentation
```

---

## Requirements

- **Python:** 3.9+ recommended
- **OS:** Windows/macOS/Linux
- **Internet access:** required to collect data from PubMed inside the notebook

---

## Install Dependencies

From the project folder, run:

```bash
pip install -U pandas numpy matplotlib seaborn scikit-learn scipy nltk gensim biopython requests
```

### NLTK Data Downloads (first run only)

Run once (in Python or a notebook cell):

```python
import nltk
nltk.download("stopwords")
nltk.download("wordnet")
```

---

## Environment Variables / Configuration

**No environment variables are required.**  
The notebook collects data from PubMed using public NCBI E‑utilities endpoints.


> Do **not** submit any `.env` file.

---

## How to Run (Step‑by‑Step)

### Option A — Run Everything (recommended)
1. Open `Clustering.ipynb` in **Jupyter Notebook** or **JupyterLab**.
2. Run cells **top to bottom**.
3. The notebook will:
   - collect data from PubMed (balanced labels a–e),
   - clean text and enforce the 130–150 word constraint,
   - build features (BoW/TF‑IDF/LDA/Doc2Vec),
   - cluster with KMeans / EM(GMM) / Hierarchical,
   - compute Silhouette + Kappa (with Hungarian alignment),
   - generate evaluation tables and plots,
   - run error analysis (confusions and text characteristics).

### Option B — Skip Data Collection (if you already have the CSV)
If you already generated `Research_Papers_MainFile.csv`, you can:
1. Place the CSV in the same folder as the notebook.
2. Skip the “Data Collection” section in the notebook.
3. Run the remaining cells to reproduce clustering, evaluation, and plots.

---

## Notes on Reproducibility

- Random seed is set in the notebook (e.g., `SEED = 42`) for sampling and model repeatability.
- Since PubMed is live, **re-collecting** data may lead to small variations (new/updated abstracts).
- Cohen’s Kappa uses **Hungarian alignment** to map cluster IDs to label IDs before scoring.

---

## Outputs

The notebook produces:
- Evaluation summary table (Feature × Algorithm → Silhouette, Kappa)
- Cluster visualizations (PCA / t‑SNE)
- Confusion matrix (aligned labels)
- Error analysis: dominant confusion pairs + top terms/collocations
- Exported dataset CSV (e.g., `Research_Papers_MainFile.csv`)

---


## Authors

- Ignancya Michelle George  
- Mamoona Zafar  
- Juan Sebastian Ramirez Acua
