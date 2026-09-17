# Lab Task 02 — Effect of Image Filtering on Skin-Lesion Classification

**Name:** Junaid
**Roll No:** FA23-BAI-051

## Objective

To investigate how different spatial-domain image-processing filters affect the performance of pretrained deep-learning models for skin-lesion classification.

## Dataset

HAM10000 skin-lesion dataset, subset: `nv`, `mel`, `bkl`, `bcc`.

## Best Three Pretrained Models (from Lab Activity 1 / Task 01)

- **Model 1:** VGG16
- **Model 2:** ResNet101
- **Model 3:** AlexNet

## Required Experimental Results

| Model | Filter | Accuracy (%) | Precision (%) | Recall (%) | F1-score (%) | Macro-F1 (%) | AUC (%) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Best Model 1 (VGG16) | No Filter | 80.51 | 82.80 | 80.51 | 81.20 | 68.00 | 92.76 |
| Best Model 1 (VGG16) | Average | 79.77 | 78.73 | 79.77 | 77.98 | 61.03 | 91.32 |
| Best Model 1 (VGG16) | Gaussian | 80.83 | 80.85 | 80.83 | 79.22 | 64.09 | 91.79 |
| Best Model 1 (VGG16) | Median | 81.04 | 79.33 | 81.04 | 78.75 | 62.22 | 91.35 |
| Best Model 1 (VGG16) | Sharpening | 80.83 | 80.05 | 80.83 | 79.37 | 64.77 | 91.41 |
| Best Model 1 (VGG16) | Sobel | 73.09 | 73.78 | 73.09 | 73.14 | 53.68 | 86.46 |
| Best Model 2 (ResNet101) | No Filter | 86.44 | 86.15 | 86.44 | 85.70 | 75.07 | 95.69 |
| Best Model 2 (ResNet101) | Average | 81.36 | 83.45 | 81.36 | 81.99 | 66.82 | 94.34 |
| Best Model 2 (ResNet101) | Gaussian | 85.17 | 85.67 | 85.17 | 85.29 | 73.03 | 95.74 |
| Best Model 2 (ResNet101) | Median | 83.58 | 83.64 | 83.58 | 83.60 | 71.36 | 94.57 |
| Best Model 2 (ResNet101) | Sharpening | 87.29 | 86.84 | 87.29 | 86.80 | 77.29 | 95.79 |
| Best Model 2 (ResNet101) | Sobel | 77.44 | 75.02 | 77.44 | 75.69 | 57.80 | 88.21 |
| Best Model 3 (AlexNet) | No Filter | 80.51 | 78.68 | 80.51 | 78.79 | 63.15 | 91.89 |
| Best Model 3 (AlexNet) | Average | 79.34 | 77.83 | 79.34 | 77.19 | 59.05 | 91.48 |
| Best Model 3 (AlexNet) | Gaussian | 81.36 | 81.62 | 81.36 | 80.82 | 65.75 | 92.80 |
| Best Model 3 (AlexNet) | Median | 80.93 | 80.71 | 80.93 | 80.47 | 65.89 | 91.53 |
| Best Model 3 (AlexNet) | Sharpening | 79.77 | 78.91 | 79.77 | 78.89 | 62.85 | 91.87 |
| Best Model 3 (AlexNet) | Sobel | 73.09 | 73.37 | 73.09 | 71.68 | 49.12 | 86.20 |

## Key Observations

- **Sharpening** was the only filter that consistently helped (ResNet101: +0.85% accuracy, +2.22 Macro-F1 vs. baseline).
- **Sobel** was consistently the worst filter across all three models (−7% to −9% accuracy vs. baseline), since it discards all color/texture information the models were pretrained on and keeps only edges.
- The effect of filtering is **not fully consistent** across models — e.g., Gaussian and Median slightly *improved* VGG16 and AlexNet's accuracy but *hurt* ResNet101's.
