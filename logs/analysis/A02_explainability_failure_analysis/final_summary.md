
## 11. Final evidence-based summary

- **Primary model:** A01 retained **M12** under the
  predefined QWK-first model-selection hierarchy.

- **M12 test predictions:** M12 produced
  **4333** correct predictions,
  **613** under-grades, and
  **324** over-grades.

- **Ordinal error severity:** M12 produced
  **644** errors spanning one severity grade
  and **293** errors spanning two or
  more severity grades.

- **M13-D complementarity:** M13-D corrected
  **203** M12 errors and introduced
  **127** new errors on the frozen test set.
  M13-D does not have one valid ensemble Grad-CAM; its visual
  interpretation instead reports the constituent with the largest
  fixed weight for the predicted class. This is not a per-image
  contribution analysis.

- **Artefact attention:** Mean relative M12 global-branch attention
  was **0.652** at image borders and
  **1.304** in image corners. A value of 1.0 represents
  the mean attention across the complete explanation map.
  These measurements remain qualitative and require manual review.

- **Weakest stable subgroup:** eye=left (n=2635, QWK=0.774).

- **Cross-model interpretation:** EfficientNet-B4 is interpreted
  using Grad-CAM, DeiT-III using transformer attention rollout,
  and M12 using separate global-branch and local-branch Grad-CAM
  maps. These methods should be compared on the same predetermined
  test images so that differences in model behaviour can be
  discussed consistently.

- **Interpretability limitation:** Grad-CAM and attention rollout
  are qualitative sensitivity or attention visualisations. They
  are not causal explanations, clinical lesion localisation, or
  proof that a highlighted area corresponds to a specific retinal
  abnormality. Expert lesion-level annotations were not available
  for validation.

- **A01 consistency:** M12 remains the primary final model because
  it achieved the highest QWK. M13-D remains a complementary
  ensemble with slightly better macro-F1 and calibration, but lower
  QWK and substantially greater computational complexity.
