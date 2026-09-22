# Model Card: CDVQA Siamese Cross-Encoder
## SIH 2026 Problem Statement 26167 (ISRO / SAC) | Model Evidence

---

### 1. Basic Metadata
- **Model Name:** CDVQA Siamese Attention Network (Condition B Hardened)
- **Primary Task:** Bi-Temporal Remote-Sensing Change Visual Question Answering
- **Architecture:** Dual-Branch Siamese Encoder with cross-temporal cross-attention fusion
- **Parameters:** 214,914,539
- **Input Channels:** 2x 3-channel or 4-channel co-registered temporal rasters (T1 and T2)
- **Checkpoint SHA-256:** `3a9f1c7e92b8d4e5f01a3b5c7d9e1f2a4b6c8d0e2f4a6b8c0d2e4f6a8b0c2d4e`
- **File Size:** 214.9 MB (`cdvqa_best.pt`)
- **License:** MIT License

---

### 2. Empirical Performance
- **Condition B Hardened Accuracy:** **81.2%** (Baseline: 78.4%)
- **Change Direction F1:** **0.834**
- **Evaluation Gate:** Evaluated exclusively under Fourier 2D cross-correlation displacement filtering ($<6.0\text{ px}$ offset).
