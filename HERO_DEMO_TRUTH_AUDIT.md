# SatQuery AI — Hero Demo Forensic Truth Audit

**Audit Date:** September 22, 2026  
**Auditor:** Team STARFORGE Internal Audit (Zero-Overclaim Mandate)  
**Purpose:** Ensure every claim made in demonstrations, slides, and public repositories exactly matches physical sensor metadata, code execution thresholds, and real test outputs.

---

## 1. Hero 01: Water Body Grounding & Delineation (Chilika Lake)

| Attribute | Forensic Value from Code & GeoTIFF Metadata | Source / Artifact |
| :--- | :--- | :--- |
| **Scenario ID** | `001_chilika_water` | `demo_corpus/scenes/001_chilika_water/` |
| **Location** | Chilika Lagoon (Balugaon Shoreline), Odisha, India | WGS84: 19.706623°N, 85.196753°E |
| **Sensor & Platform** | Copernicus Sentinel-2 MSI (Platform: Sentinel-2C) | Level-2A BOA Reflectance (`EPSG:32645`) |
| **Acquisition Timestamp** | `2026-09-18T05:03:17.419000Z` | AWS Sentinel COG: `S2C_45QUB_20260918_0_L2A` |
| **Spatial Resolution** | 10.0 meters / pixel (512 × 512 raster, 5.12 km × 5.12 km) | GeoTIFF Header |
| **Cloud Cover** | 5.2% | Scene Metadata |
| **Input Bands** | B02 (Blue), B03 (Green), B04 (Red), B08 (NIR) | Multi-spectral GeoTIFF |
| **SHA-256 Hash** | `6631247daf36cb93672be05118e273091446e0079178767c5c11142776f486d5` | `provenance/scenario_manifest.csv` |
| **Prompt** | *"Identify the major open-water region in this scene and highlight it on the satellite image."* | Canonical query |
| **Scientific Method** | Normalized Difference Water Index ($NDWI = \frac{\text{Green} - \text{NIR}}{\text{Green} + \text{NIR}}$) thresholded at $NDWI \ge 0.15$ | `PhysicalGISEngine` |
| **Empirical Output** | **2,278.4 Hectares (5,630.0 Acres)** delineated water surface | `backend/scenarios/` & `artifacts/demo_validation/` |
| **Visual Evidence** | Delineated cyan/emerald polygon overlay on interactive Leaflet canvas | `demos/hero_01_water.png` & `hero_01_water_detail.png` |

---

## 2. Hero 02: Optical + SAR Cross-Modal Fusion (Cloud & Haze Penetration)

| Attribute | Forensic Value from Code & GeoTIFF Metadata | Source / Artifact |
| :--- | :--- | :--- |
| **Scenario ID** | `015_optical_sar_fusion` | `demo_corpus/scenes/015_optical_sar_fusion/` |
| **Location** | Bengaluru, Karnataka, India | WGS84: 13.061332°N, 77.350195°E |
| **Optical Observation** | Sentinel-2B MSI L2A (10m GSD, `EPSG:32643`), Acquired: `2026-05-12T05:25:16Z` | SHA-256: `a06523027da4eef8251b05bcc8e739cda278...` |
| **SAR Observation** | Sentinel-1A C-band SAR (5.405 GHz), Level-1 GRD RTC, Dual-pol VV/VH | SHA-256: `ef68159a16b4919574e8c946705722b2bcc...` |
| **SAR Radiometry** | VV mean: -21.89 dB, VH mean: -27.94 dB, VV max: +2.28 dB | Calibrated $\sigma^0$ backscatter |
| **Physical Rationale** | C-band microwaves penetrate monsoonal cloud/haze; specular scattering off calm water ($\sigma^0 < -18\text{ dB}$) confirms open water, while dihedral double-bounce scattering ($\sigma^0 > -6\text{ dB}$) confirms urban masonry regardless of cloud cover. | Electromagnetic physics |
| **CROMA Role** | 194.3M parameter cross-attention foundation model evaluated strictly under `CROMA_LIMITED_EVIDENCE` policy. | `backend/agent/specialists/` |
| **Visual Evidence** | Interactive curtain slider comparing optical RGB and SAR backscatter | `demos/hero_02_optical_sar.png`, `hero_02_trace.png`, `hero_02_curtain_detail.png` |

---

## 3. Hero 03: Bi-Temporal Urban Settlement Expansion

| Attribute | Forensic Value from Code & GeoTIFF Metadata | Source / Artifact |
| :--- | :--- | :--- |
| **Scenario ID** | `017_bitemporal_urban_change` | `demo_corpus/scenes/017_bitemporal_urban_change/` |
| **Location** | Bengaluru, Karnataka, India | WGS84: 13.061332°N, 77.350195°E |
| **Sensor & CRS** | Sentinel-2 MSI (Platform: Sentinel-2B), 10m GSD, `EPSG:32643` | Level-2A BOA Reflectance |
| **Acquisition Dates** | Epoch T1: `2026-05-12T05:25:16Z` vs Epoch T2: `2026-09-19T05:00:00Z` | 512 × 512 co-registered tiles |
| **SHA-256 Hashes** | T1: `a06523027da4eef8251b05bcc8e739cda278...`<br>T2: `eade29b29f18851015155ce5a1a0899e76e5...` | `provenance/scenario_manifest.csv` |
| **Co-Registration Check**| 2D Fourier cross-power spectrum phase correlation measured **0.21 px shift**, well below the mandatory $<6.0\text{ px}$ barrier. | `PhysicalGISEngine` co-registration gate |
| **Detected Change** | **+36.4 Hectares** new urban built-up flux delineated via multi-index differencing. | `benchmarks/cdvqa_phase14_evaluation.json` |
| **Visual Evidence** | Red difference flux overlay isolating newly constructed built-up zones | `demos/hero_03_bitemporal.png`, `hero_03_change_detail.png` |

---

## 4. Adversarial Edge Case: Nyquist Spatial Resolution Barrier

| Attribute | Forensic Value from Code & Test Execution | Source / Artifact |
| :--- | :--- | :--- |
| **Scenario** | Sub-resolution object query (e.g. asking for small vehicle, single excavator, or small structure on 10m Sentinel-2 imagery). | `tests/test_nyquist_abstention.py` |
| **Physical Law** | Nyquist-Shannon spatial sampling theorem: minimum resolvable feature size is $\ge 2 \times \text{GSD} = 20\text{m}$. | Remote sensing fundamentals |
| **System Behavior** | System refuses to hallucinate bounding boxes or affirmative counts; returns `ABSTAIN / RESOLUTION_LIMITED` with physical reasoning trace. | `EvidencePolicy` & `ScientificGatekeeper` |
| **Visual Evidence** | Red banner warning stating: *"Query targets sub-resolution feature. Resolvable limit: 20m. Abstained to prevent spatial hallucination."* | `demos/nyquist_abstention.png` |
