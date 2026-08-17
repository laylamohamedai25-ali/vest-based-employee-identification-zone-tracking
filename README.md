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

1. **O2 — Preprocessing:** Face blurring (PDPL compliance) → CLAHE contrast enhancement → Gaussian denoising → Unsharp masking → White balance correction
2. **O3 — Detection:** YOLOv8n transfer learning — detects worker body and vest number patch simultaneously
3. **O4 — Recognition:** PARSeq scene text recognition — reads printed employee ID from vest patch
4. **O5a — Tracking:** ByteTrack multi-object tracking — maintains worker identity across frames
5. **O5b — Geofencing:** Point-in-polygon zone assignment — logs zone entry, exit, and dwell time per employee

---

## Key Results

| Stage | Metric | Value |
|---|---|---|
| O3 Detection | mAP@0.5 | 0.994 |
| O3 Detection | F1 Score | 0.978 |
| O3 Detection | Recall | 1.000 |
| O3 Detection | Inference speed | 6ms per frame |
| O4 Recognition | Full sequence accuracy (test) | 87.3% |
| O4 Recognition | Character accuracy (test) | 95.5% |
| O5 Real CCTV | Identification precision | 76.9% |
| O5 Real CCTV | Unique employees identified | 7 |
| O5 Real CCTV | Including generalisation cases | 3 (not in training set) |

---

## Dataset

- 192 annotated images covering 96 unique employee identities
- Two on-site collection sessions at Ramsis Engineering
- Both front-view and back-view orientations included
- Manually annotated using Roboflow — two classes: worker, vest_number
- Training split expanded from 135 to 810 images via augmentation
- Real CCTV evaluation: 15.4-minute Preparation Area clip validated against 177-employee master list

---

## Repository Structure
