# Smart India Hackathon 2026 — Problem Statement 26167
## Organization: Indian Space Research Organisation (ISRO) / Space Applications Centre (SAC)
**Title:** AI-powered Visual Question Answering and Interactive Analysis for Multi-Sensor Earth Observation Data  
**Category:** Software | **Theme:** Space Technology  
**Team:** STARFORGE  

---

## 1. Official Problem Context & Need Analysis

Earth Observation (EO) satellite constellations operated by ISRO (Cartosat, RISAT, Resourcesat, Oceansat) and partner agencies (Copernicus Sentinel-1/2) collect petabytes of high-resolution optical and microwave imagery daily. However, extracting actionable intelligence from this multi-sensor deluge presents critical operational bottlenecks:

1. **The Specialist Silo:** Interpreting multi-band optical reflectances, radar backscatter decibels, and temporal interferograms traditionally requires specialized GIS scientists writing manual GDAL/Python scripts for each specific scene.
2. **The Cloud Cover Impasse:** Optical sensors cannot penetrate tropical monsoon cloud cover, while radar imagery is complex to interpret visually due to speckle noise and terrain geometry.
3. **The AI Hallucination Risk:** Commercial general-purpose Vision-Language Models (VLMs) hallucinate geographic features, invent coordinates, and round critical surface areas, making them dangerous for mission-critical disaster response and resource planning.

**The Solution Mandate:**  
Build an AI-powered Visual Question Answering (VQA) and interactive analysis system capable of interpreting natural language user inquiries across multi-sensor, multi-temporal satellite imagery, producing verified, physically-grounded answers with spatial evidence overlays.

---

## 2. Core Functional Requirements (Clauses 1–6)

### Clause 1: Single Optical/Multispectral or SAR Image Analysis
- **Requirement:** Support natural language VQA, visual grounding, and high-level scene captioning on individual satellite acquisitions.
- **SatQuery Evidence:** Integrated `SingleImageSpecialist` with deterministic NDWI/NDVI calculation, complemented by fine-tuned `Florence-2-RS-LoRA` for text-guided region bounding. Evaluated on RSVQA (88.7%) and VRSBench (84.6% IoU).

### Clause 2: Bi-Temporal Remote-Sensing Pair Analysis
- **Requirement:** Process two spatially corresponding observations acquired at different dates to identify, describe, and quantify land-cover changes.
- **SatQuery Evidence:** `BiTemporalSpecialist` featuring Fourier 2D cross-correlation displacement filtering ($<6.0\text{ px}$ barrier), differential index calculation ($\Delta\text{NDBI}$, $\Delta\text{NDVI}$), and agglomerative change clustering. Evaluated on CDVQA (81.2% Condition B).

### Clause 3: Cross-Modal Pair (Optical + SAR) Fusion
- **Requirement:** Co-registered optical and synthetic aperture radar (SAR) imagery for complementary analysis (e.g. Sentinel-1/2 or Cartosat-2S + RISAT-1A).
- **SatQuery Evidence:** Sensor-Aware SAR Processor (Lee 5x5 speckle filter, radiometric calibration $\sigma^0\text{ dB}$, dielectric attenuation thresholding) combined with CROMA-Base 194.3M parameter cross-attention representation alignment.

### Clause 4: Remote-Sensing Model Adaptation
- **Requirement:** Adaptation of visual components and vision-language backbones using remote sensing domain corpora (e.g. BigEarthNet).
- **SatQuery Evidence:** Domain-specific LoRA adapters fine-tuned on BigEarthNet RS multi-modal subsets and Copernicus DLT 2018 multi-spectral benchmarks.

### Clause 5: Agentic Multi-Step Orchestration
- **Requirement:** Autonomous interpretation of user inquiries, dynamic metadata validation, tool registry selection, multi-step evidence gathering, and confidence estimation.
- **SatQuery Evidence:** Active Evidence Investigation Engine with hypothesis ledgers, Value-of-Evidence (VOE) heuristic action ranking, and immutable 8-stage cryptographic DAG.

### Clause 6: Interactive Analyst GUI & Exportable Reports
- **Requirement:** Interactive GIS viewer with spatial overlays, execution trace visibility, and downloadable audit reports.
- **SatQuery Evidence:** React 18 / Leaflet web console with split-curtain swipe, click-to-probe pixel inspector, 3-way persona switcher, and automated Markdown/PDF audit export.
