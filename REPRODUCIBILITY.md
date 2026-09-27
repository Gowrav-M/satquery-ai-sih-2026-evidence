# SatQuery AI — Evaluator Guide & Verification Protocol

**Purpose:** Comprehensive evaluation and independent verification protocol for Smart India Hackathon 2026 evaluators scoring Team STARFORGE for Grand Finale candidate selection (Problem Statement 26167, ISRO / SAC).

---

## 1. Quick-Start Evaluation Checklist (5-Minute Review)

Evaluators assessing Problem Statement 26167 can systematically audit our submission using the following 5 verification steps:

| Step | Evaluation Focus | Evidence Artifact | What to Verify |
| :---: | :--- | :--- | :--- |
| **1** | **Physical Measurement Rigor** | [`SCIENTIFIC_METHODS.md`](SCIENTIFIC_METHODS.md) | Verify deterministic band math (NDWI, NDVI, NDBI), Lee SAR speckle filtering, and backscatter dB calibration. Confirm neural networks never guess hectares. |
| **2** | **Empirical Benchmark Accuracy** | [`benchmark-results/`](benchmark-results/) | Inspect raw JSON evaluation logs for RSVQA-LR (500 items, 29.40%) and CDVQA (200 pairs, 59.00%). |
| **3** | **Earth Observation Data Provenance** | [`provenance/scenario_manifest.csv`](provenance/scenario_manifest.csv) | Verify 20 authentic Copernicus Sentinel-1 and Sentinel-2 scenes with real acquisition dates, UTM CRS zones, and 10 m GSD. |
| **4** | **System Architecture & API Contract** | [`ARCHITECTURE.md`](ARCHITECTURE.md) & [`api/sanitized_openapi.json`](api/sanitized_openapi.json) | Audit 4-tier decoupled perception-physics design and 41 typed OpenAPI 3.1 endpoints. |
| **5** | **Physical Guardrails & Safety** | [`LIMITATIONS.md`](LIMITATIONS.md) & [`demos/nyquist_abstention.png`](demos/nyquist_abstention.png) | Verify the Nyquist-Shannon resolution barrier ($2 \times \text{GSD} = 20\text{ m}$) that prevents hallucinations on sub-resolution objects. |

---

## 2. Independent Benchmark Verification (Runnable Commands)

Evaluators can immediately parse and verify our reported benchmark results from the included JSON evaluation artifacts without any setup:

### A. Verify RSVQA-LR Performance (Single-Image VQA):
```bash
python -c "import json; d=json.load(open('benchmark-results/RSVQA_summary.json')); print('RSVQA Overall Accuracy:', str(d['metrics']['overall_top1_accuracy_pct']) + '%'); print('Presence Accuracy:', str(d['metrics']['presence_questions_accuracy_pct']) + '%'); print('Comparison Accuracy:', str(d['metrics']['comparison_questions_accuracy_pct']) + '%')"
```
*Expected Result:* `RSVQA Overall Accuracy: 29.4%`, `Presence Accuracy: 53.71%`, `Comparison Accuracy: 44.83%` across 500 items.

### B. Verify CDVQA Performance (Bi-Temporal Change QA):
```bash
python -c "import json; d=json.load(open('benchmark-results/CDVQA_summary.json')); abl=d['ablations']; print('CDVQA Hybrid Accuracy:', str(abl['ablation_c_learned_deterministic_hybrid']['overall_accuracy_pct']) + '%'); print('Learned Only Accuracy:', str(abl['ablation_b_learned_only']['overall_accuracy_pct']) + '%'); print('Deterministic Baseline:', str(abl['ablation_a_deterministic_only']['overall_accuracy_pct']) + '%')"
```
*Expected Result:* `CDVQA Hybrid Accuracy: 59.0%` vs `Deterministic Baseline: 38.5%` across 200 pairs.

### C. Verify Data Manifest Cryptographic Hash:
```bash
# Unix / macOS:
shasum -a 256 provenance/scenario_manifest.csv

# Windows PowerShell:
Get-FileHash -Algorithm SHA256 provenance\scenario_manifest.csv
```
*Expected Hash:* `99f9604cd61f8c7c9360e766d8e35c50d502707683bcf376eb896e1227c420bc`

---

## 3. Model Weight Hashes & Adaptation Audit

All fine-tuned and adapted models are documented with their exact parameter counts, training objectives, and SHA-256 weight checksums:
- Checkpoint registry: [`models/checkpoint_hashes.txt`](models/checkpoint_hashes.txt)
- Model architecture cards:
  - **CROMA-Base** (194.3M params): Cross-modal optical-SAR attention alignment ([`models/model_cards/croma_base.md`](models/model_cards/croma_base.md))
  - **Florence-2-RS-LoRA**: Text-guided bounding box grounding on remote sensing rasters ([`models/model_cards/florence2_rs_lora.md`](models/model_cards/florence2_rs_lora.md))
  - **SegFormer-B0**: 10-band multi-spectral canopy segmentation, 0.6907 mIoU on DLT ([`models/model_cards/segformer_b0_dlt.md`](models/model_cards/segformer_b0_dlt.md))
  - **CDVQA Siamese**: Bi-temporal difference verification network ([`models/model_cards/cdvqa_siamese.md`](models/model_cards/cdvqa_siamese.md))

---

## 4. Evaluation Repository Structure

| Evidence Category | Included in This Submission Package | Verified In Live Evaluation Session |
| :--- | :--- | :--- |
| **Scientific Methodology** | Complete mathematical equations, radiometric formulas, and physical thresholds | Interactive parameter sweeps and algorithm inspection |
| **System Architecture** | Multi-agent state machine, 4-tier dataflow, and OpenAPI 3.1 specification | Live service routing and sub-second execution traces |
| **Benchmark Artifacts** | Machine-readable JSON summaries for RSVQA-LR, CDVQA, and DLT | Full batch evaluation scripts and loss curves |
| **Satellite Imagery** | 20-scene provenance catalog with ESA scene IDs, EPSG zones, and checksums | Full multi-gigabyte GeoTIFF rasters loaded in Leaflet/WebGL |
| **Model Information** | Model cards, LoRA rank configurations, and SHA-256 weight digests | Live GPU inference execution on RTX 3050 (6 GB VRAM) |
| **Forensic Evidence** | Full-resolution visual proofs, pixel probes, and vector boundary overlays | Arbitrary user query testing with custom raster uploads |

---

## 5. Grand Finale Demonstration Readiness & Live Prototype Verification

Team STARFORGE has already implemented and validated the complete interactive SatQuery AI platform. When selected for the Grand Finale, the system is 100% prepared for live jury evaluation:

1. **Live Interactive Querying:** The platform is configured to process custom, unprompted natural language and Indic voice queries (Hindi, Kannada, Odia, Telugu) in real time.
2. **Adversarial & Edge-Case Testing:** The physical gatekeeper is ready to demonstrate deterministic abstention against adversarial prompts (e.g. requesting sub-pixel vehicle detection to verify the 20 m Nyquist limit, or queries over heavy cloud cover to verify radar microwave penetration).
3. **End-to-End Cryptographic Audit:** Evaluators can inspect the live 8-stage Directed Acyclic Graph (DAG) with SHA-256 node signatures generated dynamically during query execution.
4. **Codebase & Architecture Walkthrough:** We welcome in-depth code review of our backend Python GIS engines, PyTorch models, and frontend geospatial visualizer.
