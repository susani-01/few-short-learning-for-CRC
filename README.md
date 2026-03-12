# Training-Free Few-Shot Learning for Colorectal Cancer Histopathology Classification

## Status

This repository contains the **research code and experimental notebooks** for the manuscript:

**"Training-Free Few-Shot Learning for Colorectal Cancer Histopathology Classification"**

The paper is currently **in manuscript stage**.

---

# Overview

Colorectal cancer (CRC) is the **third most commonly diagnosed cancer worldwide** and a leading cause of cancer-related deaths. Histopathological diagnosis is essential for CRC detection but faces challenges such as:

* Inter-observer variability among pathologists
* Limited annotated datasets
* Shortage of trained specialists in many regions
* Time-consuming manual workflows

Deep learning methods have improved histopathological image analysis, but most approaches require **large labeled datasets and extensive retraining**, limiting their applicability in clinical environments with limited data.

This work proposes a **training-free few-shot learning framework** that enables **cross-dataset classification without retraining on the target dataset**.

The framework combines **lightweight transfer learning and Prototypical Networks** to achieve reliable tumor–stroma classification in histopathology images.

---

# Key Idea

The proposed framework consists of **two stages**.

### Stage 1 — Encoder Preparation

Pretrained CNN architectures are used as **feature encoders**. Only the **classification head is fine-tuned** while the backbone remains frozen.

Models evaluated:

* MobileNetV3-Large
* EfficientNetV2B0
* ResNet50
* DenseNet121
* ResNet101

Training is performed on the **CRC-VAL-HE-7K dataset**.

---

### Stage 2 — Training-Free Few-Shot Classification

The trained encoders are **frozen** and used as feature extractors.

Prototypical Networks are then applied to perform **few-shot classification** on a different dataset:

**CRC_CFHCD_FIN**

No retraining or fine-tuning is performed on the target dataset.

Classification is performed using **Euclidean and cosine distances to class prototypes in the embedding space**.

---

# Results

### Stage 1: Supervised Training Accuracy

| Model             | Accuracy |
| ----------------- | -------- |
| MobileNetV3-Large | 98.47%   |
| EfficientNetV2B0  | 97.09%   |
| ResNet50          | 98.68%   |
| DenseNet121       | 97.30%   |
| ResNet101         | 98.40%   |

---

### Stage 2: Few-Shot Classification

Few-shot experiments were conducted with **1–20 support samples per class**.

Best performance:

**94.13% accuracy with 20 support samples per class**

The **MobileNetV3-Large encoder achieved the best few-shot transfer performance**, suggesting that lightweight architectures may generalize better in frozen-feature few-shot settings.

---

# Repository Structure

```
project/
│
├── notebooks/
│
├── README.md
```

The main experiments are implemented in the **Jupyter notebook** located in the `notebooks` folder.

---

# Datasets

The experiments use two publicly available datasets:

### CRC-VAL-HE-7K

Used for **training the CNN encoders**.

### CRC_CFHCD_FIN

Used for **few-shot tumor–stroma classification**.


---

# Requirements

The experiments were implemented in **Python using PyTorch**.

Typical dependencies include:

```
Python 3.9+
Tensorflow
NumPy
Scikit-learn
Matplotlib
Jupyter Notebook
```

---

# Limitations

* Experiments are currently implemented **only in notebook format**
* Code organization may be improved in future versions
* The framework is currently evaluated for **binary tumor–stroma classification for the few short learning**

---

# Future Work

Planned extensions include:

* Multi-class CRC tissue classification
* Larger pathology datasets
* Vision Transformer backbones
* Explainable AI integration for clinical interpretability

---
