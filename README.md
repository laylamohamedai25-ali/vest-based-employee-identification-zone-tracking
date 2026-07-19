# A Non-Biometric Computer Vision Framework for Vest-Based 
# Employee Identification and Zone-Based Activity Tracking

**MSc Artificial Intelligence — Bahrain Polytechnic 2026**
**Supervisor:** Dr. Mamoon Rashid

## Project Overview
Real-time computer vision system for automated employee 
identification and zone-based activity tracking using 
high-visibility vest numbers — without facial recognition.

## Pipeline
1. CLAHE preprocessing + face blurring (PDPL compliance)
2. YOLOv8n vest detection (mAP@0.5: 0.994, F1: 0.978)
3. PARSeq scene text recognition (83.3% seq acc, 98.6% char acc)
4. ByteTrack multi-object tracking
5. Point-in-polygon geofencing

## Results
| Stage | Metric | Value |
|---|---|---|
| Detection | mAP@0.5 | 0.994 |
| Detection | F1 Score | 0.978 |
| Detection | Recall | 1.000 |
| Recognition | Full seq accuracy | 83.3% |
| Recognition | Character accuracy | 98.6% |

## Dataset
- 190 annotated images, 96 unique employee IDs
- Two on-site collection batches
- Expanded to 810 training images via augmentation

## Requirements
- Python 3.12
- PyTorch 2.11
- Ultralytics YOLOv8
- EasyOCR
- PARSeq (baudm/parseq)
- OpenCV


## References
Key papers: [4] Liu & Bhanu 2019, [15] Koshkina & Elder 2024,
[8] ByteTrack Zhang et al. 2022, [9] Jeelani et al. 2021
