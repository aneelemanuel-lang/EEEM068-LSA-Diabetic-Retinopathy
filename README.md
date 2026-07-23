# EEEM068 LSA: Diabetic Retinopathy Grading

**Student:** Anil Emanuel  
**URN:** 6940610  
**Module:** EEEM068 Applied Machine Learning  
**Assessment:** Individual LSA Coursework  

## Project objective

This individual coursework investigates five-class diabetic retinopathy
grading using retinal fundus photographs from the Kaggle Diabetic
Retinopathy Detection dataset.

## Models

1. EfficientNet-B4 — baseline CNN
2. DeiT III-B/16 — previous main-assessment model
3. MaxViT-Tiny — new LSA hybrid Vision Transformer

## Evaluation

The project will evaluate models using:

- Accuracy
- Macro F1-score
- Balanced accuracy
- Quadratic weighted kappa
- Per-class precision, recall and F1-score
- Confusion matrices
- Training behaviour
- Ablation studies
- Failure-mode analysis
- Bias analysis
- Explainability analysis

## Repository structure

- `notebooks/` — development and experiment notebooks
- `src/` — reusable Python modules
- `configs/` — experiment configurations
- `logs/` — training histories and experiment records
- `results/` — result tables and figures
- `report/` — IEEE coursework report
- `checkpoints/` — model weights stored locally and excluded from GitHub

## Dataset

The dataset is stored separately and is not included in this repository.
