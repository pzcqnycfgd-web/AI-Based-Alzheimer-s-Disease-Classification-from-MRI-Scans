# Technical Project Explanation

## 1. Project Purpose

This project investigates deep learning methods for Alzheimer's disease
classification from structural MRI scans.

The study compares three architecture categories:

- Convolutional neural networks
- Vision Transformers
- Hybrid CNN-Transformer models

The central model is a hybrid DenseNet-121 and Swin Transformer architecture.

## 2. Datasets

### Kaggle Alzheimer MRI Dataset

The Kaggle dataset contains four classes:

- Non-Demented
- Very Mild Demented
- Mild Demented
- Moderate Demented

The dataset consists of prepared 2D MRI slices. It was used for four-class
classification and additional binary evaluation.

### OASIS-1

OASIS-1 contains 3D structural MRI data and Clinical Dementia Rating labels.

The data were split at subject level to reduce the risk of slices from the same
participant appearing in both training and test sets.

Three anatomical views were extracted:

- Axial
- Coronal
- Sagittal

## 3. Model Architecture

The hybrid model contains four main components.

### DenseNet-121

DenseNet-121 extracts local MRI features such as anatomical edges, textures,
ventricular boundaries, and local atrophy patterns.

### Feature Projection

A 1 × 1 convolution converts the CNN feature representation into a dimension
that can be processed by the Transformer.

### Swin Transformer

The Swin Transformer uses shifted-window attention to model broader spatial
relationships between different brain regions.

### Classification Head

Global pooling, dropout, and a fully connected layer are used to produce the
final classification probability.

## 4. Three-View Fusion

For OASIS-1, axial, coronal, and sagittal models generate separate prediction
probabilities.

The probabilities are combined after training to generate the final
subject-level prediction.

## 5. Training Strategy

The hybrid model uses a two-stage training strategy.

### Phase 1: Warm-up

- Freeze the CNN backbone
- Freeze the Transformer backbone
- Train the projection layer
- Train the classification head

### Phase 2: Fine-tuning

- Unfreeze the CNN
- Unfreeze the Transformer
- Fine-tune the complete model using a lower learning rate

## 6. Evaluation Metrics

The experiments use:

- Accuracy
- Precision
- Recall
- F1-score
- AUC-ROC
- Confusion matrix
- Grad-CAM visualisation

## 7. Main Results

### Kaggle Dataset

| Model | 4-Class Accuracy | Binary Accuracy | F1-score |
|---|---:|---:|---:|
| VGG-16 | 0.5625 | 0.5741 | 0.6126 |
| ResNet-50 | 0.9375 | 0.9533 | 0.9313 |
| DeiT | 0.9524 | 0.9537 | 0.9514 |
| DenseNet-121 | 0.9818 | 0.9825 | 0.9830 |
| Swin Transformer | 0.9524 | 0.9537 | 0.9557 |
| DenseNet-121 + Swin | **0.9941** | **0.9943** | **0.9945** |

### OASIS-1 Dataset

| Model | Accuracy | AUC-ROC | F1-score |
|---|---:|---:|---:|
| VGG-16 | 0.6360 | 0.7110 | 0.6470 |
| ResNet-50 | 0.5450 | 0.7300 | 0.4830 |
| DeiT | 0.6060 | 0.6560 | 0.5520 |
| DenseNet-121 | 0.6030 | 0.7350 | 0.5820 |
| Swin Transformer | 0.6670 | 0.7670 | 0.6670 |
| DenseNet-121 + Swin | **0.7231** | **0.8249** | **0.7909** |

## 8. Interpretation

The results show a large difference between the Kaggle and OASIS-1 datasets.

The Kaggle dataset contains prepared 2D slices and therefore represents a
comparatively easier classification setting.

OASIS-1 uses raw 3D MRI data, a smaller sample size, class imbalance, and
subject-level splitting. Its results provide a more realistic indication of
generalisation performance.

Grad-CAM visualisations showed that the model sometimes focused on regions
near the ventricles, temporal lobe, and hippocampal areas.

These visualisations represent model attention and should not be interpreted
as clinical proof.

## 9. Limitations

- The two datasets use different image formats and task definitions.
- OASIS-1 has a relatively small dementia test group.
- The Kaggle results may be influenced by characteristics of prepared slices.
- No independent clinical dataset was used for external validation.
- The model is not suitable for clinical diagnosis.

## 10. Ethical Notice

This project is intended for educational and research purposes only.

It must not be used as a substitute for professional medical diagnosis,
clinical assessment, or treatment decisions.
