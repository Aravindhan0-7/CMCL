# ASD Prediction Using CMCL on MRI and Gut Biome Data

This project applies **Cross-Modality Contrastive Learning (CMCL)** to integrate heterogeneous data sources—**MRI imaging** and **gut microbiome tabular data**—to predict whether an individual has Autism Spectrum Disorder (ASD). The system uses a multimodal fusion framework with separate encoders for each modality and contrastive + supervised objectives to learn informative representations.

---

## 🧠 Project Overview

### Objectives
- Fuse MRI and gut biome data for ASD prediction.
- Use CMCL to align and learn shared latent space representations from heterogeneous modalities.
- Leverage both contrastive self-supervised learning and supervised fine-tuning.

---

## 📁 Data Sources

### 1. **MRI Imaging Data**
- Dataset: [ABIDE (Autism Brain Imaging Data Exchange)](http://fcon_1000.projects.nitrc.org/indi/abide/)
- Format: 3D NIfTI images (`.nii.gz`)
- Stored on: **AWS S3 Bucket**
- Note: Metadata and non-image files (e.g., `.json`, `.xml`) are filtered out during data loading.

### 2. **Gut Biome Data**
- Format: `.csv`
- Contains: Microbial abundance features, patient IDs, and ASD labels (binary).

---

## 🏗️ Model Architecture

### 1. **MRI Encoder**
- Architecture: 3D CNN (e.g., based on MedicalNet)
- Output: 128-dimensional latent vector

### 2. **Gut Biome Encoder**
- Architecture: Multi-layer perceptron (MLP)
- Output: 128-dimensional latent vector

### 3. **Projection Heads**
- Maps encoded outputs into a **shared embedding space**
- Used for contrastive training

### 4. **Classifier Head**
- Combines both modalities and performs binary classification (ASD or not)

### 5. **Loss Functions**
- **NT-Xent Contrastive Loss** between modalities
- **Binary Cross Entropy (BCE)** loss for classification
- **Total Loss** = `λ1 * L_contrastive + λ2 * L_supervised`

---

## 🧪 Training Pipeline

1. **Data Preprocessing**
   - MRI: Skull stripping, normalization, resizing
   - Gut Biome: Log transform, normalization, feature selection

2. **Contrastive Pretraining (CMCL Phase)**
   - Aligns embeddings of paired MRI and gut biome data

3. **Supervised Fine-tuning**
   - Uses labeled data to train classifier head

4. **Evaluation**
   - Metrics: Accuracy, F1, ROC-AUC, t-SNE/UMAP visualization

5. **Inference**
   - Predict ASD from new subject data (MRI + gut biome)

---


