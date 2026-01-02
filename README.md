# LMD-KANet: A Lightweight Multimodal Dual-Attention Kolmogorov-Arnold Network for Robust and Interpretable Cross-Domain Lung Cancer Diagnosis
[![Framework](ELITE Research Lab)]
[![Paper Status](https://img.shields.io/badge/Status-Submitted-green)](https://doi.org/10.3390/1010000) [![License](https://img.shields.io/badge/License-CC_BY_4.0-blue.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Parameters](https://img.shields.io/badge/Parameters-3.5M-lightgrey)](https://github.com/)
[![Framework](https://img.shields.io/badge/PyTorch-Deep_Learning-orange)](https://pytorch.org/)

## 📜 Abstract
**LMD-KANet** is a lightweight deep learning framework designed to address the high computational cost and "black box" nature of automated lung cancer diagnosis. With a compact footprint of only **3,496,530 parameters**, this architecture is engineered for robust cross-domain performance across histopathology and radiology.


<img width="1857" height="1383" alt="1  Methodology" src="https://github.com/user-attachments/assets/d51b5193-19ae-4092-9118-f983de665bd9" />
*Figure 1: Workflow of the proposed methodology.*


The architecture integrates:
1.  **Hybrid Inverse Bottleneck (HIB)** backbone for efficient feature extraction.
2.  **Dual-Attention Mechanism** combining Coordinate Attention and Simple Attention Module (SimAM).
3.  **Kolmogorov-Arnold Network (KAN)** classifier utilizing learnable B-Spline activations.

Validated across three benchmark datasets (LC25000, Chest CT-Scan, and IQ-OTH/NCCD), LMD-KANet achieved accuracies of **99.98%**, **98.50%**, and **99.55%** respectively. It outperforms heavier benchmark models like EfficientNet-B0 and Vision Transformers (ViTs) while offering clinical interpretability through Explainable AI (XAI).

---

## 🏗️ Architecture

The LMD-KANet pipeline is composed of three synergistic stages: (1) A Hybrid Inverse Bottleneck (HIB) backbone, (2) A Dual-Attention Mechanism for spatial and energy-based refinement, and (3) A KAN classifier for dynamic non-linear decision modeling.

![LMD-KANet Architecture]

<img width="1920" height="2005" alt="2  Model Architecture" src="https://github.com/user-attachments/assets/8e4dc9fc-3e7d-48fd-9c60-cf87bc81b0b3" />
*Figure 2: The end-to-end architecture of the LMD-KANet. The workflow transitions from HIB blocks to Dual-Attention, concluding with a learnable Spline-based KAN head.*

### Key Modules
* **HIB Backbone:** Uses an "Inverse" design to expand channel dimensions and disentangle information before lightweight spatial filtering, reducing FLOPs.
* **Dual-Attention Mechanism:**
    * *Coordinate Attention:* Preserves spatial location information along vertical and horizontal axes.
    * *SimAM:* A parameter-free operator calculating 3D neuron energy to distinguish active tumor features from background noise.
* **KAN Head:** Replaces traditional MLPs with Kolmogorov-Arnold Networks, positioning learnable activation functions (B-Splines) on edges rather than nodes to reduce parameters and improve plasticity.

---

## 📂 Datasets

This study utilizes three diverse datasets to validate cross-domain generalizability.

| Feature | LC25000 (Histopathology) | Chest CT-Scan Images | IQ-OTH/NCCD |
| :--- | :--- | :--- | :--- |
| **Source** | Digital Pathology (Biopsy) | Radiology (CT Scan) | Radiology (CT Scan) |
| **Total Images** | 25,000 | ~1,000 | 1,097 |
| **Task Type** | Multi-Class (5 Classes) | Multi-Class (4 Classes) | Ternary Classification |
| **Challenge** | Cellular Texture & Morphology | 3D Geometry & Nodule Shape | Intensity Variation & Density |

![Sample Images]

<img width="4567" height="2610" alt="Preprocessed_Data_Viz" src="https://github.com/user-attachments/assets/fbd75b1d-1231-42e7-bca8-4bf5a2f0a593" />

*Figure 3: Representative sample images from the three datasets utilized in this study.*

---

## 🚀 Performance & Results

### 1. Accuracy Comparison

**LC25000 Dataset (Histopathology)**
| Model | Accuracy (%) | Precision (%) | Recall (%) | F1 (%) |
| :--- | :---: | :---: | :---: | :---: |
| Self-ONN (2024) | 99.74 | 99.74 | 99.74 | 99.74 |
| FusionNet-ViT (2025) | 99.36 | 99.38 | 99.37 | 99.37 |
| Ensemble (VGG+ResNet+EffNet) | 98.00 | 98.00 | 98.00 | 98.00 |
| **LMD-KANet (Ours)** | **99.98** | **99.98** | **99.98** | **99.98** |

**Chest CT-Scan Dataset (Radiology)**
| Model | Accuracy (%) | Precision (%) | Recall (%) | F1 (%) |
| :--- | :---: | :---: | :---: | :---: |
| Deep CNN + SVM (2022) | 94.00 | 95.00 | 94.50 | 94.50 |
| SqueezeNodule-Net V2 (2022) | 95.80 | - | 96.20 | - |
| **LMD-KANet (Ours)** | **98.50** | **98.14** | **98.48** | **98.31** |

**IQ-OTH/NCCD Dataset (Radiology)**
| Model | Accuracy (%) | Precision (%) | Recall (%) | F1 (%) |
| :--- | :---: | :---: | :---: | :---: |
| Hybrid LECNN (2025) | 99.00 | 99.06 | 98.82 | 98.94 |
| Self-Attention VGG16 (2025) | 99.36 | 98.68 | 99.28 | 98.78 |
| **LMD-KANet (Ours)** | **99.55** | **99.67** | **98.67** | **99.16** |

### 2. Computational Efficiency

LMD-KANet demonstrates a superior trade-off, achieving the highest throughput (146 FPS) with significantly fewer parameters (3.5M) compared to VGG16 (138M) or ViT (86M).

| Model Architecture | Params (M) | GFLOPs | Size (MB) | Latency (ms) |
| :--- | :---: | :---: | :---: | :---: |
| VGG16 | 138.35 | 15.50 | 528.0 | 18.2 |
| Vision Transformer (ViT-B) | 86.60 | 17.60 | 330.0 | 24.5 |
| ResNet50 | 25.56 | 4.12 | 98.0 | 12.5 |
| EfficientNet-B0 | 5.30 | 0.39 | 21.0 | 8.4 |
| **LMD-KANet (Ours)** | **3.50** | **0.74** | **13.43** | **6.83** |

![Training Curves]

<img width="700" height="548" alt="histo acc" src="https://github.com/user-attachments/assets/34ac1936-2fc5-428d-a2ea-a9c9b878981f" />
<img width="691" height="548" alt="chest acc" src="https://github.com/user-attachments/assets/40b008a6-6a6d-4c79-9c0b-cbd8c08192ee" />
<img width="700" height="548" alt="iq acc" src="https://github.com/user-attachments/assets/903d0913-97f1-40d2-a166-710eb57d2a60" />

*Figure 4: Training and Validation Accuracy curves showing stable convergence and high generalization capability over 50 epochs.*

---

## 🔍 Explainable AI (XAI)

We employed Grad-CAM, Occlusion Sensitivity, and LIME to validate that the model relies on clinically relevant biomarkers (e.g., nuclear density, nodule margins) rather than artifacts.

![XAI Visualization]

<img width="1842" height="1439" alt="histo xai" src="https://github.com/user-attachments/assets/7f3855a4-f391-41b5-90b5-25893fd2e6a8" />
*Figure 5: XAI visualizations for the LC25000 histopathology dataset. Grad-CAM and Occlusion maps confirm focus on nuclear density and cellular atypia.*

![Feature Space]

<img width="678" height="529" alt="histo features" src="https://github.com/user-attachments/assets/e5c4be89-2054-4648-b35d-9227431cd731" />
<img width="678" height="529" alt="chest features" src="https://github.com/user-attachments/assets/16ed4ce9-ef66-486d-860c-cf01b80d8e88" />
<img width="678" height="529" alt="iq features" src="https://github.com/user-attachments/assets/a61d9fb0-45d3-47de-a1af-c5597309d525" />
*Figure 5: t-SNE visualization of the learned feature space, indicating robust and separable representations for each disease category.*

---

## 🤝 Acknowledgments

The work was conducted at **ELITE Research Lab**. The authors of the manuscript acknowledge **ELITE Research Lab** for providing the computational resources and support necessary for this research.

---

