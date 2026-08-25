# A Non-Biometric Computer Vision Framework for Vest-Based Employee Identification and Zone-Based Activity Tracking in Industrial Workshops

**MSc Artificial Intelligence — Bahrain Polytechnic 2026**  
**Student:** Layla Mohamed | ID: 12011122  
**Supervisor:** Dr. Mamoon Rashid  
**Industry Partner:** Ramsis Engineering, Bahrain

---

## Project Overview

This project presents an end-to-end computer vision framework for automated employee identification and zone-based activity tracking in an industrial workshop environment. The system reads printed numeric identifiers on high-visibility vests using scene text recognition — without facial recognition, physical tags, or biometric data collection. The framework is fully compliant with Bahrain's Personal Data Protection Law (PDPL), Legislative Decree No. 30 of 2018.

The system was developed as part of an MSc AI thesis at Bahrain Polytechnic, in partnership with Ramsis Engineering, Bahrain, and validated on real CCTV footage from the partner facility.

---

## Pipeline

The framework chains five sequential processing stages:

| Stage | Objective | Description |
|---|---|---|
| O2 | Preprocessing | Face blurring (PDPL) → CLAHE → Gaussian denoising → Unsharp masking → White balance |
| O3 | Detection | YOLOv8n transfer learning — detects worker body and vest number patch simultaneously |
| O4 | Recognition | PARSeq scene text recognition — reads printed employee ID from vest patch |
| O5a | Tracking | ByteTrack multi-object tracking — maintains worker identity across frames |
| O5b | Geofencing | Point-in-polygon zone assignment — logs zone entry, exit, and dwell time per employee |

---

## Key Results

### O3 — Detection (YOLOv8n)

| Metric | Value |
|---|---|
| mAP@0.5 | 0.994 |
| F1 Score | 0.978 |
| Precision | 0.982 |
| Recall | 0.974 |
| Inference speed | 5.0ms per frame (NVIDIA T4) |
| Epochs trained | 22 (best weights at epoch 12, early stopping patience=10) |
| Optimiser | AdamW (lr=0.001667, auto-selected) |

### O4 — Recognition (PARSeq)

| Metric | Value |
|---|---|
| Full sequence accuracy (test) | 87.3% |
| Character accuracy (test) | 95.5% |
| Test crops | 157 |
| Validation sequence accuracy | 84.7% |

### O5 — Real CCTV Evaluation (Preparation Area)

| Metric | Value |
|---|---|
| Identification precision | 76.9% |
| Total reads | 636 |
| Matched reads | 489 |
| Unique employees identified | 7 |
| Generalisation cases | 3 employees not in training set |
| Clip duration | 15.4 minutes |

---

## Dataset

- 192 annotated images covering 96 unique employee identities
- Two on-site collection sessions at Ramsis Engineering
- Both front-view and back-view orientations included
- Manually annotated using Roboflow — two classes: `worker`, `vest_number`
- Training split expanded from 135 to 810 images via augmentation
- Real CCTV evaluation: 15.4-minute Preparation Area clip validated against 177-employee master list

> **Dataset access:** The dataset is not publicly available due to the Memorandum of Understanding (MOU) between Bahrain Polytechnic and Ramsis Engineering, and PDPL data protection requirements. Researchers wishing to access the dataset for academic purposes may contact the author.

---

## Repository Structure

```
vest-based-employee-identification-zone-tracking/
├── Worker_Detection_Thesis_Clean.ipynb   # Main pipeline notebook (O1-O5)
├── Ablation_Thesis_Clean.ipynb           # Ablation study notebook
├── requirements.txt                       # Python dependencies
├── data.yaml                             # Dataset configuration
└── README.md                             # This file
```

---

## Setup and Reproduction

### Requirements

- Google Colab Pro (NVIDIA T4 GPU recommended)
- Google Drive with project files
- Python 3.12.13

### Installation

```bash
pip install -r requirements.txt

# Install PARSeq separately
git clone https://github.com/baudm/parseq /content/parseq
pip install -e /content/parseq
```

### Running the notebook

1. Upload `Worker_Detection_Thesis_project.ipynb` to Google Colab
2. Run **Cell 2 (Session Restore)** first — installs all dependencies and mounts Drive
3. Run cells in order from O1 through O5

> **Note:** Reproduction requires access to the original Google Drive data including the annotated dataset, trained model weights, and CCTV clips. Contact the author for access.

### Trained model weights

The trained YOLOv8n weights (`best.pt`) are available in the repository. Load them as follows:

```python
from ultralytics import YOLO
model = YOLO('best.pt')
```

---

## Technical Stack

| Component | Tool | Version |
|---|---|---|
| Detection | YOLOv8n (Ultralytics) | 8.4.96 |
| Scale resolution | SAHI tiled inference | 0.12.6 |
| Recognition | PARSeq | Pre-trained checkpoint parseq-bb5792a6.pt |
| Tracking | ByteTrack (via Ultralytics) | Built-in |
| Framework | PyTorch | 2.11.0+cu128 |
| Language | Python | 3.12.13 |
| Environment | Google Colab Pro | NVIDIA T4 16GB |

---

## Citation

If you use this work, please cite:

```
Mohamed, L. (2026). A Non-Biometric Computer Vision Framework for Vest-Based 
Employee Identification and Zone-Based Activity Tracking in Industrial Workshops. 
MSc Thesis, Bahrain Polytechnic.
```

---

## License

This project is made available for academic research purposes. Commercial use requires written permission from Bahrain Polytechnic and Ramsis Engineering.

---
