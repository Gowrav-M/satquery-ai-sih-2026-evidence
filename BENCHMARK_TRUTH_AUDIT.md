# SatQuery AI — Benchmark Truth Forensic Audit & Reconciliation

**Audit Date:** September 22, 2026  
**Auditor:** Maestro AI Forensic Pipeline (Zero-Overclaim Mandate)  
**Target:** Elimination of all ungrounded figures across public evidence documentation.

---

## 1. Truth Reconciliation Matrix

| Benchmark | Previous Unverified Claim | Actual Measured Forensic Truth | Authoritative Disk Artifact | Forensic Notes & Scientific Explanation |
| :--- | :--- | :--- | :--- | :--- |
| **RSVQA-LR** (Sentinel-2, 10m GSD) | 88.7% Overall, 91.2% Presence (1,500 samples) | **29.40% Overall Top-1 Accuracy** (147/500 items)<br>• **Presence:** 53.71% (123/229)<br>• **Comparison:** 44.83% (13/29)<br>• **Count:** 4.72% (10/212)<br>• **Attribute:** 0.00% (0/29) | `artifacts/rsvqa_public_benchmark_results.json`<br>`VQA_COMPLIANCE_MATRIX.md` | Model exhibits strong presence/comparison detection, but near-zero counting (4.72%) and attribute capability (0.00%) due to binary vision-language pretraining. ECE is 25.26%. Production enforces Immediate Null Policy (`confidence = null`). |
| **CDVQA** (Bi-Temporal Change VQA) | 81.2% Overall (1,200 pairs) | **200 Samples Evaluated**:<br>• **Ablation A (Deterministic Only):** 38.50% (77/200)<br>• **Ablation B (Learned Only):** 58.00% (116/200)<br>• **Ablation C (Hybrid):** 59.00% (118/200)<br>• Increase: 75.0% (Det) / 85.0% (Hybrid)<br>• Decrease: 70.83% (Det) / 62.5% (Hybrid) | `benchmarks/cdvqa_phase14_evaluation.json` | Baseline deterministic NDVI differencing achieves 38.5%. Learned Siamese features boost overall to 58.0%, and Hybrid (learned + gate) achieves 59.0%. Granular breakdown: directional change is strong (75–85%), while complex ratio queries are low (10–20%). |
| **VRSBench** (Visual Grounding) | 84.6% Box IoU @ 0.5 (800 regions) | **NOT EVALUATED / NOT PROVEN** (No test artifact exists on disk) | None | Removed from evaluated claims. Marked as pending formal benchmark execution. |
| **Copernicus DLT 2018** (Multi-Spectral Forest) | 0.6907 mIoU | **0.6907 mIoU** (3,000 tiles, 10 Sentinel-2 bands)<br>• Broadleaved Forest: 0.7765<br>• Non-Tree Class: 0.7820<br>• Coniferous Forest: 0.5136 | `benchmarks/evaluate_segformer_baseline.py`<br>`VQA_COMPLIANCE_MATRIX.md` | Verified empirical metric. Coniferous edge recall at $\le 10\text{m}$ boundary is 31.32% due to canopy mixed pixels. |
| **ISRO Private Test Sets** | N/A | **PRIVATE / NOT PROVEN** | None | No claims made. Operational integration ready via typed ISRO adapters (`ISROOpticalAdapter`, `ISROSARAdapter`). |

---

## 2. Corrective Actions Required & Implemented
1. **Update `SatQuery-AI-SIH-2026-Evidence/benchmark-results/RSVQA_summary.json`**:
   - Replace 88.7% with 29.40% Overall (53.71% Presence, 44.83% Comparison, 4.72% Count).
   - Document sample size as 500 stratified items from official held-out test split.
2. **Update `SatQuery-AI-SIH-2026-Evidence/benchmark-results/CDVQA_summary.json`**:
   - Replace 81.2% with exact 200-sample ablation breakdown: 38.5% (Deterministic), 58.0% (Learned), 59.0% (Hybrid).
   - Document directional change accuracy (75.0% increase, 70.83% decrease).
3. **Update `SatQuery-AI-SIH-2026-Evidence/benchmark-results/benchmark_notes.md`**:
   - Provide complete, honest commentary on counting/attribute limits and calibration policy.
4. **Update `SatQuery-AI-SIH-2026-Evidence/BENCHMARKS.md`**:
   - Reconcile Master Table with exact metrics and status flags (EVALUATED vs NOT EVALUATED vs PRIVATE).
