# SatQuery AI — Public Technical Evidence & Validation Record
## Smart India Hackathon 2026 | Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  
**Category:** Software | **Theme:** Space Technology  
**Organization:** Indian Space Research Organisation (ISRO) / Space Applications Centre (SAC)  

---

> [!IMPORTANT]
> **Repository Purpose & Scope Notice:**  
> This repository contains selected technical documentation, validation results, architecture diagrams, model information, data provenance and demonstration evidence for SatQuery AI. The production source code, private checkpoints, credentials and restricted evaluation data are intentionally not included.

---

## 1. Problem Statement & Context

Modern Earth Observation (EO) satellites produce vast streams of multi-spectral optical and Synthetic Aperture Radar (SAR) imagery. However, accessing and synthesizing these datasets remains a major bottleneck for non-specialist decision makers (such as district agricultural officers, relief coordinators, and municipal planners). 

General-purpose Large Language Models (LLMs) and consumer Vision-Language Models (VLMs) fail on satellite imagery because they:
1. Cannot ingest multi-spectral or complex-valued radar formats (such as 10-band Sentinel-2 COGs or calibrated Sentinel-1 GRD backscatter).
2. Suffer from spatial and numerical hallucinations, inventing land boundaries and fabricating surface areas.
3. Lack awareness of physical sensor physics, such as cloud attenuation in optical bands or the spatial Nyquist resolution barrier.

**SIH 2026 Problem Statement 26167** calls for an AI-powered system capable of natural language Visual Question Answering (VQA) and multimodal Earth Observation analysis across optical and microwave sensors.

---

## 2. System Overview

**SatQuery AI** is an evidence-driven Earth Observation investigation system developed by Team STARFORGE. The architecture decouples natural language interpretation from physical raster computation:

```
USER QUERY & GEO-RASTERS
         │
         ▼
INTENT INTERPRETATION   ───────► Query intent extraction & tool parameter assignment
         │
         ▼
OBSERVATION VALIDATION  ───────► Resolution check, Nyquist barrier (2x GSD), CRS & bounds
         │
         ▼
SPECIALIST DISPATCH     ───────► Deterministic band math (NDWI, NDVI, NDBI, SAR calibration)
         │
         ▼
EMPIRICAL MEASUREMENT   ───────► Geodesic area calculation, vector polygons, backscatter stats
         │
         ▼
EVIDENCE GRAPH (DAG)    ───────► 8-stage immutable Directed Acyclic Graph (SHA-256 integrity)
         │
         ▼
SCIENTIFIC GATEKEEPER   ───────► Cross-sensor contradiction arbitration (Microwave primacy)
         │
         ▼
STRUCTURED FINDING      ───────► Dual-layer presentation (Executive finding + technical evidence)
```

Rather than allowing an LLM to guess numerical measurements, SatQuery AI delegates spatial and spectral calculations to deterministic GIS engines, locking numerical values directly to raster pixel counts.

---

## 3. Architecture

SatQuery AI consists of four modular layers:
1. **User Interface & Interaction Layer:** Built with React 18, TypeScript, and Leaflet. Features interactive raster maps, split-screen optical-SAR swipe curtains, and vector overlays.
2. **Agentic Orchestration Layer:** Analyzes natural language queries, generates testable hypotheses, checks sensor capabilities, and constructs execution plans.
3. **Specialist & Foundation Model Layer:** Integrates local deterministic physics engines (`PhysicalGISEngine`, `SensorAwareSARProcessor`) with adapted neural models (`SegFormer-B0`, `Florence-2-RS-LoRA`, `CROMA-Base`).
4. **Validation & Provenance Layer:** Enforces the 8-stage cryptographic Directed Acyclic Graph (DAG), records SHA-256 node digests, and enforces physical guardrails.

Detailed documentation: [`ARCHITECTURE.md`](ARCHITECTURE.md) | Diagram: [`architecture/system_architecture.png`](architecture/system_architecture.png)

---

## 4. Technical Capabilities

| Capability | Implementation Mechanism | Evidence Reference |
| :--- | :--- | :--- |
| **Optical Multispectral Analysis** | Sentinel-2 L2A surface reflectance; NDWI, NDVI, NDBI band mathematics | [`demos/hero_01_water.png`](demos/hero_01_water.png) |
| **SAR Microwave Processing** | Sentinel-1 C-band Level-1 GRD; Lee speckle filtering; $\sigma^0\text{ dB}$ calibration | [`demos/hero_02_optical_sar.png`](demos/hero_02_optical_sar.png) |
| **Optical + SAR Cross-Modal Fusion** | Multi-sensor agreement checking; microwave penetration through cloud cover | [`demos/hero_02_trace.png`](demos/hero_02_trace.png) |
| **Bi-Temporal Change Detection** | Sub-pixel 2D Fourier phase registration; spectral differencing; change clustering | [`demos/hero_03_bitemporal.png`](demos/hero_03_bitemporal.png) |
| **Spatial Grounding** | Text-guided bounding box detection; polygonization; UTM to WGS-84 coordinate mapping | [`models/model_cards/florence2_rs_lora.md`](models/model_cards/florence2_rs_lora.md) |
| **Multi-Spectral Segmentation** | 10-band SegFormer-B0 encoder adapted for Copernicus forest canopy classes | [`models/model_cards/segformer_b0_dlt.md`](models/model_cards/segformer_b0_dlt.md) |
| **Nyquist Sampling Guardrail** | Rejects sub-resolution feature requests below $2 \times \text{GSD}$ ($20\text{m}$ for Sentinel) | [`demos/nyquist_abstention.png`](demos/nyquist_abstention.png) |
| **Cryptographic Provenance DAG** | 8-stage immutable graph recording input hashes, parameters, and outputs | [`architecture/evidence_graph.png`](architecture/evidence_graph.png) |

---

## 5. Scientific Validation

The system has been evaluated through automated regression suites and edge-case validation:
- **Critical Regression Suite:** 30 of 33 tests passed (90.9% pass rate); the 3 flagged cases represent rigid string assertion mismatches and cloud weighting edge cases, fully analyzed in [`validation/regression_summary.md`](validation/regression_summary.md).
- **Zero Mock Leakage:** Verified that production routes execute real raster mathematics with zero hardcoded lookup tables.
- **Fault Tolerance:** Evaluated orchestrator resilience when individual specialist modules are bypassed or unavailable ([`validation/specialist_bypass_results.md`](validation/specialist_bypass_results.md)).

Detailed documentation: [`VALIDATION.md`](VALIDATION.md)

---

## 6. Benchmark Results

All metrics below are reconciled against saved evaluation artifacts on disk. We make zero claims on unreleased or private datasets.

| Benchmark | Dataset / Task | Sample Size | Evaluated Metric | Observed Result | Status | Reference Artifact |
| :--- | :--- | :--- | :--- | :--- | :---: | :--- |
| **RSVQA-LR** | Sentinel-2 MSI Single-Image VQA (10m GSD) | 500 held-out items | Overall Top-1 Accuracy | **29.40%** (Presence: **53.71%**, Comparison: **44.83%**, Count: **4.72%**, Attribute: **0.00%**) | **EVALUATED** | [`benchmark-results/RSVQA_summary.json`](benchmark-results/RSVQA_summary.json) |
| **RSVQA Calibration** | VQA Probability Calibration | 500 test items | ECE / MCE / Brier | **ECE: 25.26%**, MCE: 41.20%, Brier: 0.2718 *(Enforces Immediate Null Policy: confidence = null)* | **VERIFIED** | `artifacts/vqa_calibration_metrics.json` |
| **CDVQA** | Bi-Temporal Change Detection QA | 200 test pairs | Classification Accuracy | Deterministic: **38.50%**, Learned: **58.00%**, Hybrid: **59.00%** (Increase: **75–85%**, Decrease: **62.5–70.8%**) | **EVALUATED** | [`benchmark-results/CDVQA_summary.json`](benchmark-results/CDVQA_summary.json) |
| **Copernicus DLT 2018**| 10-Band Canopy Segmentation | 3,000 tiles | Mean IoU | **0.6907 mIoU** (Broadleaved: 0.7765, Non-Tree: 0.7820, Coniferous: 0.5136) | **EVALUATED** | `benchmarks/evaluate_segformer_baseline.py` |
| **VRSBench** | Visual Grounding | N/A | Box IoU @ 0.5 | **N/A** | **NOT EVALUATED / NOT PROVEN** | None |
| **ISRO Private Archives** | Operational Cartosat / RISAT | Unreleased ISRO Data | Task Success Rate | **N/A** | **PRIVATE / NOT PROVEN** | None |

Detailed documentation: [`BENCHMARKS.md`](BENCHMARKS.md) | [`benchmark-results/benchmark_notes.md`](benchmark-results/benchmark_notes.md)

---

## 7. Three Hero Demonstrations

### Hero 01: Single-Image Water Body Delineation (Chilika Lagoon)
- **Scenario ID:** `001_chilika_water`
- **Location:** Chilika Lagoon (Balugaon Shoreline), Odisha, India (`EPSG:32645`)
- **Sensor:** Copernicus Sentinel-2C MSI (Level-2A BOA Reflectance, 10m GSD), Acquired: `2026-09-18T05:03:17Z`
- **Query:** *"Identify the major open-water region in this scene and highlight it on the satellite image."*
- **Observed Result:** Delineates **2,278.4 Hectares (5,630.0 Acres)** of open water using $NDWI \ge 0.15$. The text finding is locked directly to the raster pixel count.
- **Evidence:** [`demos/hero_01_water.png`](demos/hero_01_water.png) | [`demos/hero_01_water_detail.png`](demos/hero_01_water_detail.png)

### Hero 02: Optical + SAR All-Weather Cross-Modal Fusion (Bengaluru)
- **Scenario ID:** `015_optical_sar_fusion`
- **Location:** Bengaluru Urban Corridor, Karnataka, India (`EPSG:32643`)
- **Sensors:** Sentinel-2B MSI (Optical) + Sentinel-1A C-SAR (Microwave GRD), Acquired: `2026-05-12T05:25:16Z`
- **Query:** *"Use the optical and SAR observations together to determine whether both sensors provide consistent evidence about the major land-cover pattern."*
- **Observed Result:** Evaluates optical reflectance alongside SAR backscatter. Where cloud cover attenuates optical signal, C-band microwave penetration ($\sigma^0 < -18\text{ dB}$ for specular water, $> -6\text{ dB}$ for built-up) provides independent physical corroboration via interactive split curtain.
- **Evidence:** [`demos/hero_02_optical_sar.png`](demos/hero_02_optical_sar.png) | [`demos/hero_02_trace.png`](demos/hero_02_trace.png)

### Hero 03: Bi-Temporal Urban Settlement Expansion (Bengaluru)
- **Scenario ID:** `017_bitemporal_urban_change`
- **Location:** Bengaluru Urban Corridor, Karnataka, India (`EPSG:32643`)
- **Sensors:** Matched Sentinel-2B MSI Pair: Epoch T1 (`2026-05-12T05:25:16Z`) vs Epoch T2 (`2026-09-19T05:00:00Z`)
- **Query:** *"Did the built-up area expand between these two observations? Show where the change occurred."*
- **Observed Result:** Enforces sub-pixel 2D Fourier phase correlation ($0.21\text{ px} < 6.0\text{ px}$ barrier) before differencing. Quantifies **+36.4 Hectares** of new built-up construction flux with vector change boundaries.
- **Evidence:** [`demos/hero_03_bitemporal.png`](demos/hero_03_bitemporal.png) | [`demos/hero_03_change_detail.png`](demos/hero_03_change_detail.png)

---

## 8. Data Provenance

All demonstration scenarios utilize authentic, calibrated satellite rasters:
- **Optical Data:** Copernicus Sentinel-2 MSI Level-2A surface reflectance (10m GSD).
- **SAR Data:** Copernicus Sentinel-1 C-SAR Level-1 GRD, dual-polarization VV/VH (10m GSD).
- **Source:** European Space Agency (ESA) via AWS Open Data Cloud-Optimized GeoTIFFs.
- **Licensing:** [CC-BY-SA 3.0 IGO](https://creativecommons.org/licenses/by-sa/3.0/igo/) (Copernicus Open Access Terms).
- **Zero Synthetic Pixels:** All 20 scenes represent authentic satellite acquisitions across India.

Complete machine-readable catalog: [`provenance/scenario_manifest.csv`](provenance/scenario_manifest.csv) | Detailed documentation: [`DATA_PROVENANCE.md`](DATA_PROVENANCE.md)

---

## 9. Known Limitations

In accordance with scientific rigor, the operational boundaries of the system are explicitly documented:
1. **Conifer Canopy Margin Recall:** On 10m Sentinel-2 data, coniferous forest recall drops to **31.32%** within $\le 10\text{m}$ of stand edges due to mixed foliage/understory pixels.
2. **Bathymetry Refusal:** The system measures water surface area (2,278.4 ha) but strictly refuses water depth/volume estimation without active sonar or bathymetric surveys.
3. **Co-Registration Barrier:** If bi-temporal image displacement exceeds $6.0\text{ pixels}$, change detection is automatically halted to prevent false edge artifacts.
4. **VQA Calibration:** Vision-language models exhibit significant miscalibration on satellite queries ($ECE = 25.26\%$). The system enforces the **Immediate Null Policy** (`confidence = null`, displaying *"Uncalibrated"*) rather than emitting misleading probabilities.
5. **Numerical Counting Limit:** Fine-grained object counting on 10m rasters is limited (**4.72%** on RSVQA-LR); users are advised to use vector polygonization instead.

Detailed documentation: [`LIMITATIONS.md`](LIMITATIONS.md)

---

## 10. Public vs Private Repository Boundary

| Capability / Asset | Public Evidence Package (`SatQuery-AI-SIH-2026-Evidence/`) | Private Engineering Repository (`d:\SATQUERY`) |
| :--- | :--- | :--- |
| **Purpose** | Supplementary technical evidence & validation record | Complete implementation codebase & development history |
| **Source Code** | None included (no `.py`, `.tsx`, `.ts` implementations) | Full Python backend, React frontend, training routines |
| **Model Weights** | Architectural parameters, model cards, SHA-256 digests | Binary checkpoint files (`.pt`, `.bin`, `.safetensors`) |
| **Rasters** | 20-scene metadata manifest, coordinates, checksums | Multi-gigabyte GeoTIFF raster files and local caches |
| **Credentials** | Zero credentials or tokens included | Protected local `.env` configuration files |
| **API Contract** | Sanitized OpenAPI 3.1 schema for local evaluation | Full live API application with private routing |

---

## 11. Supplementary Demonstration Video

- **Video Link:** [Watch the 6-Minute Demonstration on YouTube (Unlisted)](demo/DEMO_VIDEO.md)
- **Status:** Supplementary technical evidence provided for evaluator convenience.
- **Chapter Breakdown:**
  - `00:00` — Problem Statement 26167 & Earth Observation bottlenecks
  - `00:30` — Architecture: Decoupling perception from raster physics
  - `01:00` — Hero 01: Water body delineation in Chilika Lagoon (2,278.4 ha)
  - `02:00` — Hero 02: Optical + SAR cloud penetration in Bengaluru
  - `03:15` — Hero 03: Bi-temporal urban expansion in Bengaluru (+36.4 ha)
  - `04:30` — Nyquist spatial resolution barrier ($2 \times \text{GSD} = 20\text{m}$)
  - `05:00` — 8-stage cryptographic evidence DAG and exportable report
  - `05:40` — Summary and ISRO adapter interfaces

Detailed timeline: [`demo/demo_timeline.md`](demo/demo_timeline.md)

---

## 12. Official SIH Presentation Alignment

The official SIH 2026 presentation submission consists of a 6-slide deck:
- **Slide 1:** Title, Team STARFORGE, Problem Statement 26167
- **Slide 2:** Problem Identification & Core Earth Observation Challenges
- **Slide 3:** Proposed Solution & Decoupled Perception-Physics Architecture
- **Slide 4:** Technical Methodology, Specialist Dispatch & Physical Formulas
- **Slide 5:** Feasibility, Practicability, Sustainability & Social Impact
- **Slide 6:** Technical Evidence Summary *(contains supplementary QR codes linking to this public GitHub evidence repository and the unlisted demonstration video)*

*(Slide 7 from the original organizer template is the instruction sheet and is excluded from the submission deck).*

---

## 13. Team & Authorship

- **Team:** STARFORGE  
- **Event:** Smart India Hackathon 2026 Grand Finale  
- **Problem Statement:** 26167 (ISRO / SAC) — AI-Powered VQA and Multimodal Earth Observation Analysis  
- **Documentation License:** [CC-BY 4.0 International](https://creativecommons.org/licenses/by/4.0/)  
- **Satellite Data License:** [CC-BY-SA 3.0 IGO](https://creativecommons.org/licenses/by-sa/3.0/igo/) (Copernicus Open Access)
