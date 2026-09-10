# Task 01 — Skin Lesion Classification Results

## Table 1. Comparison of Transfer Learning Models

| Model | Accuracy (%) | Precision (%) | Recall (%) | F1-Score (%) | AUC (%) |
| --- | --- | --- | --- | --- | --- |
| AlexNet | 63.75 | 67.87 | 63.75 | 60.37 | 88.93 |
| VGG16 | 66.25 | 67.15 | 66.25 | 64.57 | 89.71 |
| VGG19 | 62.50 | 64.53 | 62.50 | 59.02 | 88.44 |
| ResNet18 | 61.25 | 62.88 | 61.25 | 54.71 | 91.89 |
| ResNet50 | 62.50 | 64.20 | 62.50 | 59.00 | 91.46 |
| ResNet101 | 65.00 | 68.72 | 65.00 | 61.14 | 93.69 |
| DenseNet121 | 58.75 | 58.52 | 58.75 | 53.22 | 88.87 |
| EfficientNet-B0 | 62.50 | 68.13 | 62.50 | 56.47 | 92.44 |

## Table 2. Comparison of Different Classifiers

| Feature Extractor | Classifier | Accuracy (%) | Precision (%) | Recall (%) | F1-Score (%) | AUC (%) |
| --- | --- | --- | --- | --- | --- | --- |
| Deep Features | Logistic Regression | 58.75 | 63.10 | 58.75 | 55.38 | 88.57 |
| Deep Features | Decision Tree | 48.75 | 46.55 | 48.75 | 44.91 | 67.97 |
| Deep Features | Random Forest | 61.25 | 64.34 | 61.25 | 56.70 | 89.07 |
| Deep Features | K-Nearest Neighbors (KNN) | 61.25 | 66.20 | 61.25 | 55.51 | 82.91 |
| Deep Features | Linear SVM | 61.25 | 69.21 | 61.25 | 58.54 | 87.91 |
| Deep Features | RBF-SVM | 60.00 | 61.75 | 60.00 | 55.67 | 89.90 |
| Deep Features | XGBoost | 61.25 | 63.73 | 61.25 | 56.84 | 86.27 |

## Table 3. Computational Efficiency Comparison

| Model | Parameters (M) | Model Size (MB) | FLOPs (G) | Inference Time (ms) | Accuracy (%) |
| --- | --- | --- | --- | --- | --- |
| AlexNet | 57.02 | 217.54 | 0.71 | 2.09 | 63.75 |
| VGG16 | 134.28 | 512.25 | 15.47 | 10.44 | 66.25 |
| VGG19 | 139.59 | 532.51 | 19.63 | 12.46 | 62.50 |
| ResNet18 | 11.18 | 42.72 | 1.82 | 2.27 | 61.25 |
| ResNet50 | 23.52 | 90.02 | 4.13 | 5.77 | 62.50 |
| DenseNet121 | 6.96 | 27.13 | 2.90 | 15.35 | 58.75 |
| EfficientNet-B0 | 4.01 | 15.60 | 0.41 | 7.97 | 62.50 |
