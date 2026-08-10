# EEEM068 LSA: Diabetic Retinopathy Grading

**Student:** Anil Emanuel  
**URN:** 6940610  
**Module:** EEEM068 Applied Machine Learning  
**Assessment:** Individual LSA Coursework

## Project objective

This individual coursework investigates five-class diabetic retinopathy
grading using retinal fundus photographs from the Kaggle Diabetic
Retinopathy Detection / EyePACS dataset.

The work compares three core architectures:

1. **EfficientNet-B4** — baseline convolutional neural network
2. **DeiT-III-B/16** — Vision Transformer from the main assessment with
   additional LSA fine-tuning experiments
3. **MaxViT-Tiny** — new LSA hybrid convolution-attention architecture

The study also investigates class-imbalance handling, augmentation,
fine-tuning strategy, ordinal-aware optimisation and fine-grained retinal
guidance through a structured component-wise and branch-based ablation
programme.

A complementary calibrated ensemble, **M13-D**, is evaluated separately
from the three core architectures.

## Final selected models

- **EfficientNet-B4** — baseline CNN
- **DeiT-III-B/16** — previous transformer architecture with additional
  LSA fine-tuning experiments
- **MaxViT-Tiny M12** — final selected single-model LSA configuration
- **M13-D** — complementary calibrated class-specialist ensemble
  constructed from frozen candidate models spanning EfficientNet-B4,
  DeiT-III and MaxViT experiments

MaxViT-Tiny M12 is treated as the primary model because it achieved the
strongest quadratic weighted kappa on the frozen internal test set.

M13-D slightly improved macro-F1 and calibration but reduced QWK relative
to M12 and required multiple constituent models, so it is treated as a
complementary analysis rather than the final selected architecture.

## Experimental programme

A total of **21 evaluated configurations** were investigated:

- **8 DeiT-III experiments (D01-D08)**
- **12 MaxViT-Tiny experiments (M01-M12)**
- **1 complementary ensemble (M13-D)**

The later MaxViT experiments were not a single cumulative chain.
M09-M11 were separate fine-grained guidance branches from the M07
reference, while M12 combined the selected fine-grained views.

### DeiT-III experiments

Eight DeiT-III experiments were evaluated:

- `D01` — unweighted cross-entropy baseline
- `D02` — clipped weighted cross-entropy
- `D03` — safe retinal augmentation
- `D04` — learning-rate experiment
- `D05` — weight-decay experiment
- `D06` — batch-size experiment
- `D07` — two-phase fine-tuning
- `D08` — random-seed stability check

### MaxViT-Tiny experiments

Twelve single-model MaxViT-Tiny experiments were evaluated:

- `M01` — unweighted baseline
- `M02` — clipped weighted cross-entropy
- `M03` — WeightedRandomSampler
- `M04` — focal loss
- `M05` — safe retinal augmentation
- `M06` — two-phase fine-tuning
- `M07` — ordinal-aware loss
- `M08` — random-seed stability check
- `M09` — detection-guided regions
- `M10` — pseudo-segmentation guidance
- `M11` — global-local crop fusion
- `M12` — combined fine-grained guidance

### Complementary ensemble

- `M13-D` — calibrated class-specialist ensemble constructed from frozen
  candidate models spanning EfficientNet-B4, DeiT-III and MaxViT experiments

## Final test-set results

| Model | Accuracy | Balanced Accuracy | Macro F1 | QWK | ECE |
|---|---:|---:|---:|---:|---:|
| EfficientNet-B4 | 0.568 | 0.444 | 0.396 | 0.5164 | 0.130 |
| DeiT-III-B/16 | 0.786 | 0.487 | 0.509 | 0.6690 | 0.158 |
| MaxViT-Tiny M12 | 0.822 | 0.560 | 0.574 | **0.7957** | 0.066 |
| M13-D ensemble | 0.837 | 0.548 | 0.577 | 0.7780 | **0.046** |

MaxViT-Tiny M12 achieved the strongest ordinal agreement and was therefore
selected as the final primary model.

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
- ROC-AUC analysis
- Failure-mode analysis
- High-confidence error analysis
- Under-grading and over-grading analysis
- Persistent-error analysis
- Eye-laterality subgroup analysis
- Deterministic image-quality subgroup analysis
- Explainability analysis

Quadratic weighted kappa is used as the primary model-selection metric
because diabetic retinopathy grades are ordinal and large grade-distance
errors should be penalised more strongly than neighbouring-grade errors.

## Explainability methods

Different explainability methods are used according to model architecture:

- **EfficientNet-B4:** Grad-CAM
- **DeiT-III-B/16:** attention rollout
- **MaxViT-Tiny M12:** global and local Grad-CAM
- **M13-D:** class probabilities and class-specific constituent evidence

The generated heatmaps and attention maps are interpreted as qualitative
model-behaviour evidence and are not treated as clinically validated lesion
localisations.

## Main analysis notebooks

- `A01_final_model_comparison_and_statistical_evaluation.ipynb`  
  Final quantitative comparison, calibration, per-class evaluation,
  ordinal-error analysis and bootstrap statistical evaluation.

- `A02_explainability_failure_analysis_and_bias_evaluation.ipynb`  
  Explainability, high-confidence failures, persistent errors, subgroup
  analysis and model-behaviour investigation.

- `A03_multiclass_roc_analysis.ipynb`  
  One-vs-rest multiclass ROC analysis for EfficientNet-B4, DeiT-III-B/16
  and MaxViT-Tiny M12.

## Dataset and splitting

The project uses the Kaggle Diabetic Retinopathy Detection / EyePACS
dataset containing **35,126 labelled retinal fundus images** across five
severity grades:

0. No diabetic retinopathy
1. Mild
2. Moderate
3. Severe
4. Proliferative diabetic retinopathy

The data were divided into:

- **Train:** 24,586 images
- **Validation:** 5,270 images
- **Internal test:** 5,270 images

Patient identifiers were used as grouping units so that images from the
same patient could not occur in different partitions.

## Preprocessing

Two deterministic preprocessing variants were defined:

- **P0** — conservative border crop and resize
- **P1** — P0 plus Ben Graham-style local contrast enhancement

P1 was explored within the tuned EfficientNet configuration, but that
experiment also changed balancing and loss choices. Therefore, the isolated
causal effect of P1 cannot be established from a one-factor comparison.

P0 was retained for the headline DeiT-III and MaxViT experiments to
preserve a common input pipeline.

## Repository structure

- `notebooks/` — data preparation, training and analysis notebooks
- `src/` — reusable Python modules
- `configs/` — experiment configurations
- `logs/` — training histories, metrics and analysis tables
- `results/` — result tables and generated figures
- `report/` — IEEE-format coursework report
- `checkpoints/` — model weights stored locally and excluded from GitHub

## Reproducibility

Experiment outputs, evaluation tables and report-ready figures are stored
under `logs/` and `results/`.

Large model checkpoint files and the original EyePACS dataset are excluded
from the repository.

The complete experiment progression, additional quantitative comparisons,
training curves, ROC analysis, calibration results, explainability outputs,
failure-mode visualisations and subgroup analyses are documented in the
coursework report appendices.
