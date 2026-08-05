# EEEM068 LSA: Diabetic Retinopathy Grading

**Student:** Anil Emanuel  
**URN:** 6940610  
**Module:** EEEM068 Applied Machine Learning  
**Assessment:** Individual LSA Coursework  

## Project objective

This individual coursework investigates five-class diabetic retinopathy
grading using retinal fundus photographs from the Kaggle Diabetic
Retinopathy Detection dataset.

The work compares a baseline convolutional neural network, a previous
Vision Transformer model, and a new hybrid convolution-transformer model.
It also evaluates whether a complementary ensemble can improve class-level
performance and calibration.

## Models

1. **EfficientNet-B4** — baseline convolutional neural network
2. **DeiT-III-B/16** — previous main-assessment Vision Transformer
3. **MaxViT-Tiny M12** — new LSA hybrid convolution-transformer model
4. **M13-D** — complementary class-weighted ensemble using the strongest
   constituent models

MaxViT-Tiny M12 is treated as the primary model because it achieved the
strongest quadratic weighted kappa. M13-D is evaluated as a complementary
ensemble because it produced slightly stronger macro-F1 and calibration,
but lower quadratic weighted kappa and greater complexity.

## Evaluation

The models are evaluated using:

- Accuracy
- Macro F1-score
- Weighted F1-score
- Balanced accuracy
- Quadratic weighted kappa
- Per-class precision, recall and F1-score
- Confusion matrices
- Training behaviour
- Ablation studies
- Bootstrap confidence intervals
- Calibration analysis
- Failure-mode analysis
- High-confidence error analysis
- Under-grading and over-grading analysis
- Persistent-error analysis
- Subgroup and bias analysis
- Explainability analysis

## Explainability methods

Different explainability methods are used according to model architecture:

- **EfficientNet-B4:** Grad-CAM
- **DeiT-III-B/16:** attention rollout
- **MaxViT-Tiny M12:** global and local Grad-CAM
- **M13-D:** class probabilities and highest-weighted class-specific
  constituent evidence

The generated heatmaps and attention maps are interpreted as qualitative
model-behaviour evidence and are not treated as clinically validated lesion
localisations.

## Repository structure

- `notebooks/` — data preparation, model training and analysis notebooks
- `src/` — reusable Python modules
- `configs/` — experiment configurations
- `logs/` — training histories, metrics and analysis tables
- `results/` — result tables and generated figures
- `report/` — IEEE-format coursework report
- `checkpoints/` — model weights stored locally and excluded from GitHub

## Main analysis notebooks

- `A01` — final quantitative model comparison, calibration and statistical
  evaluation
- `A02` — explainability, failure-mode and subgroup/bias analysis

## Dataset

The dataset is stored separately and is not included in this repository.

The project uses retinal fundus photographs and five diabetic retinopathy
severity classes:

0. No diabetic retinopathy
1. Mild
2. Moderate
3. Severe
4. Proliferative diabetic retinopathy

## Reproducibility

Experiment outputs, evaluation tables and report-ready figures are stored
under `logs/` and `results/`.

Large model checkpoint files and the original dataset are excluded from the
repository.
