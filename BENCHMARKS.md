# SatQuery AI — Empirical Benchmark Performance
## Verified Evaluation Results | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

> [!CAUTION]
> **Scientific Integrity & Benchmark Policy:**  
> 1. Every metric reported below is traced directly to an existing evaluation artifact on disk.  
> 2. SatQuery AI does NOT report fabricated numbers on private or unreleased ISRO archives.  
> 3. Private ISRO/SAC test set performance is explicitly marked: **PRIVATE / NOT PROVEN**.  
> 4. Unverified benchmarks (e.g. VRSBench) are marked **NOT EVALUATED / NOT PROVEN**.

---

## 1. Master Benchmark Performance Table

| Benchmark Name | Target Modality / Task | Split / Samples | Official Metric | Observed Result | Evaluation Artifact | Date Evaluated | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **RSVQA-LR** | Single-Image Sentinel-2 MSI VQA | Official Held-Out Split (500 samples) | Overall Top-1 Accuracy (%) | **29.40%** (Presence: **53.71%**, Comparison: **44.83%**) | [`benchmark-results/RSVQA_summary.json`](benchmark-results/RSVQA_summary.json) | 2026-09-18 | **EVALUATED** |
| **CDVQA** | Bi-Temporal Change Question Answering | Public Test Split (200 pairs) | Hybrid Accuracy (%) | **59.00%** (Det Baseline: **38.50%**, Learned: **58.00%**) | [`benchmark-results/CDVQA_summary.json`](benchmark-results/CDVQA_summary.json) | 2026-09-11 | **EVALUATED** |
| **Copernicus DLT 2018** | 10-Band Multi-Spectral Canopy Segmentation | Test Split (3,000 tiles) | Mean IoU (3 classes) | **0.6907 mIoU** (Broadleaf: 0.7765, Conifer: 0.5136) | `benchmarks/evaluate_segformer_baseline.py` | 2026-09-15 | **EVALUATED** |
| **VRSBench** | Visual Grounding on Remote Sensing | N/A | Box IoU @ 0.5 (%) | **N/A** | None | N/A | **NOT EVALUATED / NOT PROVEN** |
| **ISRO Private Archives** | Operational Cartosat / RISAT Evaluation | Unreleased ISRO Data | Task Success Rate | **N/A** | Private Archive | N/A | **PRIVATE / NOT PROVEN** |

---

## 2. Granular Breakdown by Benchmark

### 2.1 RSVQA Low-Resolution (Sentinel-2, 10m GSD)
- **Source:** Sylvain Lobry et al., IEEE TGRS 2020 (`dmarsili/RSVQA-LR-2k`).
- **Presence Questions (e.g. *"Is there a river in this scene?"*):** **53.71% Accuracy** (123 / 229 correct).
- **Comparison Questions:** **44.83% Accuracy** (13 / 29 correct).
- **Numerical Count Questions:** **4.72% Accuracy** (10 / 212 correct).
- **Attribute Questions:** **0.00% Accuracy** (0 / 29 correct).
- **Calibration Metrics:** ECE = **25.26%**, MCE = **41.20%**, Brier Score = **0.2718**.
- **Operational Enforcement:** Enforces the **Immediate Null Policy** (`confidence = null`). UI presents *"Uncalibrated"* rather than fabricating deceptive probability values.

### 2.2 CDVQA (Change Detection Visual Question Answering)
- **Source:** Bi-temporal Sentinel-2 change detection QA split (200 test samples).
- **Directional Change (Increase):** **75.00%** (Deterministic) / **85.00%** (Learned Hybrid).
- **Directional Change (Decrease):** **70.83%** (Deterministic) / **62.50%** (Learned Hybrid).
- **General Change Detection:** **43.66%** (Deterministic) / **76.06%** (Learned Hybrid).
- **Ratio Quantification:** **10.00% – 20.00%**.
- **Co-Registration Barrier:** Verified sub-pixel alignment ($<6.0\text{ px}$ 2D phase shift) is required before difference computation.

### 2.3 Copernicus DLT 2018 Multi-Spectral Segmentation
- **Architecture:** SegFormer-B0 modified for 10 Sentinel-2 bands.
- **Broadleaved Forest IoU:** **0.7765**
- **Non-Tree Class IoU:** **0.7820**
- **Coniferous Forest IoU:** **0.5136** (Conifer boundary recall at $\le 10\text{m}$ edge is $31.32\%$ due to mixed pixels at canopy boundaries).

---

## 3. Benchmark Traceability Notes
Detailed diagnostic notes and raw metrics are documented in:  
[`benchmark-results/benchmark_notes.md`](benchmark-results/benchmark_notes.md)
