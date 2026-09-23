# Model Card: CDVQA Siamese Cross-Encoder
## SIH 2026 Problem Statement 26167 (ISRO / SAC) | Model Evidence

---

### 1. Basic Metadata
- **Model Name:** CDVQA Siamese Attention Network (Condition B Hardened)
- **Primary Task:** Bi-Temporal Remote-Sensing Change Visual Question Answering
- **Architecture:** Dual-Branch Siamese Encoder with cross-temporal cross-attention fusion
- **Parameters:** 214,914,539
- **Input Channels:** 2x 3-channel or 4-channel co-registered temporal rasters (T1 and T2)
- **Checkpoint SHA-256:** `b9a0be3cae0cc42cba731bdd16741836cb6b2a9a7bc12e6078d237e7d0d97101`
- **File Size:** 214.9 MB (`cdvqa_best.pt`)
- **License:** MIT License

---

### 2. Empirical Performance
- **Hybrid Accuracy:** **59.00%** (200 test samples; Deterministic: 38.50%, Learned: 58.00%)
- **Macro F1:** **0.2831** (evaluated on 200 samples)
- **Evaluation Gate:** Evaluated exclusively under Fourier 2D cross-correlation displacement filtering ($<6.0\text{ px}$ offset).
