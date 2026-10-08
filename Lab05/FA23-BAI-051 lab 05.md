# Lab 05 — HOG-Based Industrial Defect Detection and Classification

**Name:** Junaid
**Roll No:** FA23-BAI-051

## Objective

To detect and classify surface defects on hot-rolled steel using Histogram of Oriented Gradients (HOG) features with classical machine-learning classifiers, and to study how the HOG parameters and image perturbations affect performance.

## Dataset

NEU steel surface defect dataset (`sovitrath/neu-steel-surface-defect-detect-trainvalid-split`, Kaggle), using the train and validation folders combined.

- **Total images:** 1,800 (200×200 grayscale, original)
- **Classes (6):** crazing, inclusion, patches, pitted surface, rolled-in scale, scratches
- **Class counts:** inclusion 312, patches 307, rolled-in scale 300, crazing 300, scratches 291, pitted surface 290
- **Labels:** taken from Pascal VOC XML annotations (most frequent defect name per image), falling back to the parent folder name.

## Method

1. **Preprocessing:** convert to grayscale, resize to 128×128, and apply histogram equalisation to reduce lighting variation.
2. **Features:** HOG with 8×8-pixel cells (unless varied), 2×2 cells per block, L2-Hys block normalisation.
3. **Classifiers:** RBF-kernel SVM (C=10, standardised features) and Random Forest (300 trees).
4. **Split:** stratified 75/25 train/test split with a fixed seed (1,350 train / 450 test).

## Results

### Parameter sweep (cell size × orientations × classifier)

| Cell | Orientations | Model | Accuracy | Macro Precision | Macro Recall | Macro F1 |
| --- | --- | --- | --- | --- | --- | --- |
| 4 | 6 | HOG + SVM | 0.789 | 0.787 | 0.787 | 0.781 |
| 4 | 6 | HOG + RandomForest | 0.600 | 0.608 | 0.596 | 0.562 |
| 4 | 9 | HOG + SVM | 0.764 | 0.765 | 0.762 | 0.751 |
| 4 | 9 | HOG + RandomForest | 0.587 | 0.601 | 0.583 | 0.547 |
| 4 | 12 | HOG + SVM | 0.787 | 0.790 | 0.784 | 0.774 |
| 4 | 12 | HOG + RandomForest | 0.600 | 0.599 | 0.595 | 0.562 |
| 8 | 6 | HOG + SVM | 0.871 | 0.870 | 0.871 | 0.870 |
| 8 | 6 | HOG + RandomForest | 0.720 | 0.738 | 0.718 | 0.698 |
| 8 | 9 | HOG + SVM | 0.840 | 0.839 | 0.839 | 0.837 |
| 8 | 9 | HOG + RandomForest | 0.740 | 0.761 | 0.737 | 0.717 |
| 8 | 12 | HOG + SVM | 0.864 | 0.864 | 0.864 | 0.863 |
| 8 | 12 | HOG + RandomForest | 0.744 | 0.753 | 0.742 | 0.726 |
| 16 | 6 | HOG + SVM | 0.878 | 0.880 | 0.878 | 0.878 |
| 16 | 6 | HOG + RandomForest | 0.851 | 0.855 | 0.850 | 0.849 |
| **16** | **9** | **HOG + SVM** | **0.896** | **0.895** | **0.896** | **0.895** |
| 16 | 9 | HOG + RandomForest | 0.824 | 0.830 | 0.823 | 0.819 |
| 16 | 12 | HOG + SVM | 0.882 | 0.884 | 0.883 | 0.882 |
| 16 | 12 | HOG + RandomForest | 0.860 | 0.863 | 0.859 | 0.857 |

**Best setting:** cell size 16, 9 orientations, HOG + SVM (macro F1 0.895).

### Per-class results for the best setting

**HOG + SVM (cell 16, orientations 9)** — accuracy 0.90, macro F1 0.89

| Class | Precision | Recall | F1 | Support |
| --- | --- | --- | --- | --- |
| crazing | 0.93 | 0.99 | 0.95 | 75 |
| inclusion | 0.86 | 0.81 | 0.83 | 78 |
| patches | 0.92 | 0.86 | 0.89 | 77 |
| pitted surface | 0.83 | 0.90 | 0.87 | 72 |
| rolled-in scale | 0.99 | 0.99 | 0.99 | 75 |
| scratches | 0.85 | 0.84 | 0.84 | 73 |

**HOG + Random Forest (cell 16, orientations 9)** — accuracy 0.82, macro F1 0.82

| Class | Precision | Recall | F1 | Support |
| --- | --- | --- | --- | --- |
| crazing | 0.86 | 0.99 | 0.92 | 75 |
| inclusion | 0.69 | 0.85 | 0.76 | 78 |
| patches | 0.85 | 0.78 | 0.81 | 77 |
| pitted surface | 0.81 | 0.78 | 0.79 | 72 |
| rolled-in scale | 0.91 | 0.99 | 0.95 | 75 |
| scratches | 0.85 | 0.56 | 0.68 | 73 |

The SVM confusion matrix is shown in the notebook (Section 9).

### Robustness of the best SVM model

The model was trained on clean images. Each perturbation was applied only to the test images.

| Condition | Accuracy | Macro F1 | Δ Accuracy | Δ Macro F1 |
| --- | --- | --- | --- | --- |
| Clean | 0.896 | 0.895 | — | — |
| Brightness (×1.4 + 30) | 0.176 | 0.074 | −0.720 | −0.821 |
| Gaussian noise (σ = 15) | 0.453 | 0.368 | −0.442 | −0.527 |
| Rotation (15°) | 0.789 | 0.785 | −0.107 | −0.110 |
| Gaussian blur (5×5, σ = 1.5) | 0.227 | 0.163 | −0.669 | −0.732 |

### Product inspection demo

The quality-control function was run on one test image (a pitted-surface sample). It predicted **DEFECTIVE (pitted_surface)** with 99% confidence and returned **REJECT PRODUCT**.

## Discussion

- **Cell size matters most.** Larger cells (16 px) gave the best results for both classifiers. Small cells (4 px) produced very long feature vectors that performed worst, with SVM accuracy between 0.76 and 0.79.
- **SVM beat Random Forest** at every setting, by 0.03 to 0.25 accuracy. The gap was largest for small cells.
- **Rolled-in scale** was almost perfectly separated (F1 0.99). **Inclusion** and **scratches** were the hardest classes, and scratches were the most-missed class for Random Forest (recall 0.56).
- **The model is fragile to appearance changes.** Brightness and blur shifts reduced accuracy by about 67–72 points, and noise by 44 points. Rotation of 15° had the smallest effect (−11 points). HOG depends on gradient magnitudes, and the brightness and blur changes altered them strongly. Training with augmented images would likely improve robustness.

## Limitations

- Single train/test split. Using 5-fold cross-validation would give more reliable estimates.
- Images were resized to 128×128, which may hide fine scratches.
- Robustness was tested with one perturbation of each type and one rotation angle only.
- The dataset has no defect-free class, so this is a six-class problem rather than a Normal/Defective decision.

## Conclusion

HOG features with an RBF-SVM classify the six steel-surface defect types with 90% accuracy and macro F1 of 0.895 when cell size is 16 px and 9 orientations are used. The model performs well on clean images but is sensitive to brightness, blur, and noise changes, so it would need augmentation or further preprocessing before use in a real inspection line.
