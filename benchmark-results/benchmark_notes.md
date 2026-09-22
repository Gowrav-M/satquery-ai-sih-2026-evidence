# SatQuery AI — Benchmark Methodology & Reconciliation Notes
## Evaluation Protocol | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

## 1. Authoritative Benchmark Reconciliation

During early exploratory cycles, ungrounded estimates and informal notes existed in working drafts. In accordance with our zero-overclaim scientific policy, **every public figure is reconciled to permanent disk evaluation artifacts**:

### 1.1 RSVQA-LR (Sentinel-2, 10m GSD)
- **Held-Out Test Split:** Official test partition (500 stratified items; `dmarsili/RSVQA-LR-2k`, Sylvain Lobry et al., IEEE TGRS 2020).
- **Overall Top-1 Accuracy:** **29.40%** (147 / 500 correct).
- **Category Breakdown:**
  - Presence queries (*"Is there a river in this scene?"*): **53.71%** (123 / 229 correct).
  - Comparison queries: **44.83%** (13 / 29 correct).
  - Numerical count queries: **4.72%** (10 / 212 correct).
  - Attribute queries: **0.00%** (0 / 29 correct).
- **Calibration Analysis:** Expected Calibration Error (ECE) is **25.26%**, Maximum Calibration Error (MCE) is **41.20%**, Brier Score is **0.2718**.
- **Production Policy (Immediate Null Policy):** Because the model exhibits poor confidence calibration on out-of-domain open queries, raw logit confidences are suppressed. Production VQA responses return `confidence = null` (`"Uncalibrated"` in UI) rather than generating deceptive confidence metrics.
- **Reference Artifact:** `artifacts/rsvqa_public_benchmark_results.json` and `VQA_COMPLIANCE_MATRIX.md`.

### 1.2 CDVQA (Bi-Temporal Change Question Answering)
- **Held-Out Test Split:** 200 bi-temporal image-question pairs.
- **Ablation Results:**
  - **Ablation A (Deterministic Differencing Only):** **38.50%** (77 / 200), Macro F1 = 0.0957.
  - **Ablation B (Learned Siamese VLM Only):** **58.00%** (116 / 200), Macro F1 = 0.2371.
  - **Ablation C (Learned + Deterministic Gate Hybrid):** **59.00%** (118 / 200), Macro F1 = 0.2831.
- **Granular Insights:** Directional change queries (*increase/decrease*) achieve **75.0% – 85.0%** accuracy, while complex ratio and target identification queries remain bounded (**10.0% – 43.75%**).
- **Spatial Precondition:** 2D Fourier phase-shift co-registration must measure $<6.0\text{ px}$ before differencing is permitted.
- **Reference Artifact:** `benchmarks/cdvqa_phase14_evaluation.json`.

### 1.3 Copernicus DLT 2018 (10-Band Multi-Spectral Segmentation)
- **Dataset:** 3,000 Copernicus tiles with 10 Sentinel-2 bands (B2, B3, B4, B5, B6, B7, B8, B8A, B11, B12).
- **Architecture:** SegFormer-B0 encoder adapted for 10 input channels.
- **Observed Mean IoU:** **0.6907 mIoU**.
  - Broadleaved Forest IoU: **0.7765**.
  - Non-Tree IoU: **0.7820**.
  - Coniferous Forest IoU: **0.5136**.
- **Known Diagnostic Limitation:** Conifer edge boundary recall at $\le 10\text{m}$ edge is $31.32\%$ due to mixed canopy pixels along parcel edges.
- **Reference Artifact:** `benchmarks/evaluate_segformer_baseline.py`.

### 1.4 Visual Grounding (VRSBench)
- **Status:** **NOT EVALUATED / NOT PROVEN**. No verified evaluation artifact exists on disk; all prior references have been formally retracted.

### 1.5 Private ISRO Operational Archives
- **Status:** **PRIVATE / NOT PROVEN**. No performance claims are made on unreleased ISRO datasets. Integration readiness is demonstrated via typed sensor adapters (`ISROOpticalAdapter`, `ISROSARAdapter`).
