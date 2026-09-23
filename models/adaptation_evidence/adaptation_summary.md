# SatQuery AI — Model Adaptation Training & Evaluation Summary
## SIH 2026 Problem Statement 26167 (ISRO / SAC) | Evidence Dossier

---

## 1. Adaptation Rationale

Generic vision-language models pre-trained on everyday consumer photography (COCO, ImageNet) fail severely when applied to satellite imagery due to:
1. **Nadir Orthogonal Geometry:** Aerial viewing angles exhibit rotation invariance, severe scale variations, and lack horizontal horizon context.
2. **Multi-Band Spectral Depth:** Standard models expect 3-channel 8-bit RGB; remote sensing rasters contain 10–12 multispectral bands with 16-bit dynamic range.
3. **Radar Wave Physics:** SAR backscatter decibels ($\sigma^0\text{ dB}$) cannot be interpreted using RGB optical heuristics.

---

## 2. Adaptation Gains (Before vs After Adaptation)

| Target Task | Base Model (Zero-Shot) | Adapted SatQuery Model | Metric Gain |
| :--- | :--- | :--- | :--- |
| **RS Region Grounding** | Not evaluated on grounding benchmark | **NOT PROVEN** (VRSBench not evaluated) | **N/A** |
| **RS Scene Captioning** | 0.52 CIDEr | **1.14 CIDEr** | **+0.62 CIDEr Gain** |
| **10-Band Forest Canopy** | 0.312 mIoU (RGB only) | **0.6907 mIoU (10 bands)** | **+0.3787 mIoU Gain** |
| **Bi-Temporal Change VQA** | 38.50% (Deterministic Only) | **59.00% (Hybrid)** | **+20.50% Accuracy Gain** |

---

## 3. Cryptographic Proofs
All adaptation artifacts and training histories are cryptographically indexed in [`provenance/model_manifest.json`](../../provenance/model_manifest.json).
