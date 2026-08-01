# Alzheimer's Disease Classification from MRI

**Portfolio owner and repository maintainer: Rumo Bian**

A deep learning project for Alzheimer's disease classification from structural
MRI using CNN, Vision Transformer, and hybrid DenseNet-Swin architectures.

[View the research paper](docs/research-paper.pdf)  
[Read the technical explanation](docs/project-explanation.md)

---

## Project Overview

This repository presents the code, experimental results, and technical
documentation for an MRI-based Alzheimer's disease classification project.

The project evaluates:

- VGG-16
- ResNet-50
- DenseNet-121
- DeiT
- Swin Transformer
- DenseNet-121 + Swin Transformer

Experiments were conducted using the Kaggle Alzheimer MRI dataset and OASIS-1.

## Key Technical Features

- CNN, Transformer, and hybrid architecture comparison
- Four-class and binary MRI classification
- Subject-level splitting for OASIS-1
- Axial, coronal, and sagittal MRI processing
- Two-stage transfer learning
- Three-view probability fusion
- Grad-CAM and attention visualisation

## Main Results

| Dataset | Best Model | Accuracy | AUC-ROC |
|---|---|---:|---:|
| Kaggle AD | DenseNet-121 + Swin | 0.9941 | 0.9996 |
| OASIS-1 | DenseNet-121 + Swin | 0.7231 | 0.8249 |

The difference between the two datasets is important. Kaggle contains prepared
2D images, while OASIS-1 uses a more challenging subject-level workflow based
on 3D MRI data.

## Hybrid Architecture

```text
MRI input
   ↓
Preprocessing and slice extraction
   ↓
DenseNet-121 local feature extraction
   ↓
1 × 1 convolutional feature projection
   ↓
Swin Transformer global feature modelling
   ↓
Classification head
   ↓
Three-view probability fusion
   ↓
Final prediction
