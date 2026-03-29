# GSoC-2026-HistoMoE-Proposal-Experiment
Preliminary  experiments for GSoC '26 

# 🧬 HistoMoE: Mixture-of-Experts for Histology-to-Gene Expression Prediction

A lightweight prototype of a **Mixture-of-Experts (MoE)** model for predicting **spatial gene expression** from **histology image patches**, inspired by the HEST-1k dataset and biological heterogeneity challenges.

---

## 🚀 Overview

Spatial Transcriptomics (ST) provides gene expression at tissue locations but is:

- Expensive  
- Limited in scale  
- Not widely available  

On the other hand, **H&E-stained Whole Slide Images (WSIs)** are abundant and rich in morphological information.

👉 This project explores:

> Can we **predict gene expression directly from histology images** using a **Mixture-of-Experts (MoE)** model?

---

## 🧠 Motivation

Biological tissues exhibit **high heterogeneity** across:

- Organs  
- Patients  
- Disease states  

A single model may struggle to generalize across such diversity.

👉 We hypothesize:

> A **Mixture-of-Experts** model can capture this heterogeneity by allowing different experts to specialize in different biological patterns.

---

## 🏗️ Model Architecture

### 🔀 HistoMoE Design

- **Patch Encoder**: Converts image patches → embeddings  
- **Gating Network (Router)**:
  - Takes embeddings as input  
  - Uses **Top-K routing (k = 2)**  
- **Experts**:
  - **Shared Experts** → capture general patterns  
  - **Fine-Grained Experts** → specialize in sub-patterns  
- **Prediction Head**:
  - Outputs expression of top-N HVGs  

---

### ⚙️ Configuration (example)

```python
embed_dim = 256
meta_dim = 64
expert_hidden = 512
num_shared = 2
num_fine = 4
topk = 2
n_hvg = 50
