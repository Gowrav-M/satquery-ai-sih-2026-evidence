# SatQuery AI — System Architecture & Scientific Dataflow
## Technical Specification | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

## 1. High-Level Architectural Philosophy

SatQuery AI is engineered on the principle of **Decoupled Perception and Physics**:
1. **Perception Components (Neural VLMs / Transformers):**
   - Interpret natural language questions and extract query intents.
   - Propose candidate bounding boxes, semantic classes, and visual attention maps.
   - Strictly bounded: When 0 targets match a prompt, neural models must emit `UNRESOLVED_GROUNDING`. They are never allowed to hallucinate coordinates or guess radiometric quantities.
2. **Physics Components (Deterministic GIS Engines):**
   - Calculate exact physical metrics from calibrated sensor pixels: NDWI, NDVI, NDBI, and SAR $\sigma^0\text{ dB}$.
   - Apply geometric affine transformations to compute authoritative geodesic hectares and acres.
   - Evaluate physical barriers (Nyquist spatial resolution, 2D phase co-registration offset).
   - Arbitrate cross-sensor contradictions based on physical wave propagation (e.g. microwave cloud penetration vs optical scattering).

---

## 2. Four-Tier Architectural Topology

```mermaid
flowchart TD
    subgraph Tier1 ["Tier 1: Interaction & Localization Layer"]
        T1_UI["Leaflet WebGL Map Console<br/>(Interactive Vector Overlays)"]
        T1_Curtain["Split-Curtain Swipe<br/>(Optical vs. SAR Inspector)"]
        T1_Persona["3-Way Persona Switcher<br/>(Farmer / Collector / Scientist)"]
        T1_Probe["Real-Time Pixel Probe<br/>(Raw DN & Calibrated Radiometry)"]
        T1_Voice["Indic Multilingual Voice Engine<br/>(Sarvam AI API Integration)"]
    end

    subgraph Tier2 ["Tier 2: Agentic Orchestration Brain"]
        T2_AST["Query Intent Parser & AST<br/>(Spatial & Temporal Extractor)"]
        T2_Contract["Observation Contract Validator<br/>(CRS, Bounds & Resolution Check)"]
        T2_Hypo["Competing Hypotheses Ledger<br/>(Priors, Null & Target Hypotheses)"]
        T2_Planner["VOE Next-Action Planner<br/>(Value of Evidence Optimization)"]
    end

    subgraph Tier3 ["Tier 3: Specialist & Foundation Foundry"]
        subgraph Sensors ["Satellite Rasters Ingested"]
            S_Opt["Sentinel-2 MSI Optical<br/>(10m BOA Reflectance B02–B12)"]
            S_SAR["Sentinel-1 C-SAR Radar<br/>(10m GRD Dual-Pol VV/VH)"]
            S_Temp["Bi-Temporal Observation Pair<br/>(Epoch T1 vs. Epoch T2)"]
        end

        subgraph Engines ["Domain Specialist Engines"]
            E_GIS["PhysicalGISEngine<br/>(Deterministic NDWI / NDVI / NDBI)"]
            E_SAR["SensorAwareSARProcessor<br/>(Lee 5x5 Filter & dB Calibration)"]
            E_CROMA["CROMA-Base Joint Embedder<br/>(194.3M Optical-Radar Latent)"]
            E_Seg["SegFormer-B0 Specialist<br/>(10-Band Canopy Segmentation)"]
            E_Ground["Florence-2-RS-LoRA<br/>(Spatial Bounding Box Grounding)"]
            E_Change["BiTemporal Specialist<br/>(2D Fourier Phase Shift & Differencing)"]
        end
    end

    subgraph Tier4 ["Tier 4: Scientific Trust & Provenance"]
        T4_Nyquist["Nyquist Epistemic Barrier<br/>(Rejects Targets < 2x GSD)"]
        T4_CoReg["Fourier Phase Co-Registration<br/>(Misregistration Barrier < 6.0 px)"]
        T4_Arbiter["Multi-Sensor Contradiction Arbiter<br/>(Microwave Cloud Penetration)"]
        T4_DAG["8-Stage Cryptographic DAG<br/>(SHA-256 Immutable Node Hashes)"]
        T4_Output["Verified Earth Insight Dossier<br/>(GeoJSON, Exact Hectares, PDF/MD)"]
    end

    %% Inter-Tier Operational Flows
    Tier1 -->|"User Query, Persona & Spatial Extent"| Tier2
    Tier2 -->|"Structured Dispatch & Tool Parameters"| Tier3
    Sensors -->|"Calibrated Pixels & Metadata"| Engines
    Engines -->|"Raw Radiometry & Spatial Proposals"| Tier4
    Tier4 -->|"Cryptographically Verified Polygons & Dossier"| Tier1
```

---

## 3. The 8-Stage Cryptographic Evidence Graph (DAG)

Every investigation generates an immutable directed acyclic graph where each node contains the SHA-256 cryptographic digest of its inputs and state:

```mermaid
flowchart TD
    subgraph DAG ["8-Stage Immutable Cryptographic Evidence Graph (DAG)"]
        N1["<b>Node 1: User Query & Intent AST</b><br/><code>hash = SHA-256(raw_query, persona, locale)</code>"]
        N2["<b>Node 2: Competing Hypotheses Formulation</b><br/><code>hash = SHA-256(parent_hash, H0_null, H1_target)</code>"]
        N3["<b>Node 3: Satellite Asset Registration</b><br/><code>hash = SHA-256(parent_hash, raster_sha256, crs, gsd)</code>"]
        N4["<b>Node 4: Specialist Parameter Ingestion</b><br/><code>hash = SHA-256(parent_hash, tools, band_indices, thresholds)</code>"]
        N5["<b>Node 5: Empirical Radiometric Computation</b><br/><code>hash = SHA-256(parent_hash, calibrated_pixel_arrays, mask)</code>"]
        N6["<b>Node 6: Cross-Sensor Contradiction Arbitration</b><br/><code>hash = SHA-256(parent_hash, optical_sar_agreement, physics_rule)</code>"]
        N7["<b>Node 7: Evidence Sufficiency Verification</b><br/><code>hash = SHA-256(parent_hash, nyquist_passed, coreg_passed)</code>"]
        N8["<b>Node 8: Final Grounded Finding & Vector Export</b><br/><code>hash = SHA-256(parent_hash, polygons, hectares, confidence)</code>"]

        N1 -->|"Prior State"| N2
        N2 -->|"Asset Binding"| N3
        N3 -->|"Parameter Binding"| N4
        N4 -->|"Pixel Ingestion"| N5
        N5 -->|"Sensor Cross-Check"| N6
        N6 -->|"Barrier Validation"| N7
        N7 -->|"Cryptographic Seal"| N8
    end
```

### Integrity Guarantee:
If any downstream parameter or finding is altered, the cryptographic chain hash is invalidated. This enables automated auditability for ISRO mission archives.

---

## 4. Multi-Sensor Grounding & Cross-Modal Arbitration Flow

When optical and microwave sensors evaluate the same geographic scene under non-ideal weather conditions, SatQuery AI resolves contradictions through physical wave mechanics rather than statistical guessing:

```mermaid
flowchart TD
    subgraph Sensing ["1. Multi-Sensor Remote Sensing Ingestion"]
        OptFeed["Optical Imagery (Sentinel-2)<br/>Surface Reflectance (B02, B03, B04, B08, B11, B12)"]
        SARFeed["Microwave Radar (Sentinel-1)<br/>C-Band (5.405 GHz) Dual-Pol (VV + VH Backscatter)"]
    end

    subgraph ConditionChecks ["2. Physical Environmental Analysis"]
        CloudDetect{"Cloud / Haze / Shadow Present<br/>in Optical Spectral Bands?"}
        DielectricEval{"Calibrated Radar Backscatter<br/>σ° < -18.0 dB (Specular Water)?"}
        DoubleBounce{"High Orthogonal Return<br/>σ° > +5 dB (Corner Double-Bounce)?"}
    end

    subgraph ArbitrationMatrix ["3. Deterministic Wave Propagation Physics Rules"]
        RuleCloudWater["Rule 1: All-Weather Flood / Lake Primacy<br/><i>Microwave C-band penetrates clouds; confirms standing water</i>"]
        RuleUrban["Rule 3: Urban Structure Corroboration<br/><i>Vertical building walls reflect double-bounce radar pulse</i>"]
        RuleOpticalAgreement["Rule 0: Full Spectral & Radar Concordance<br/><i>Optical NDWI ≥ 0.15 corroborated by SAR σ° < -18 dB</i>"]
    end

    subgraph VerdictState ["4. Synthesis & Grounded Verdict"]
        HighConfidenceWater["Multi-Sensor Verified Water Mask<br/>(Confidence: High | Optical-SAR Corroborated)"]
        AllWeatherWater["All-Weather Grounded Water Mask<br/>(Confidence: Calibrated | SAR Cloud-Penetrating Primacy)"]
        BuiltUpVector["Verified Built-Up Infrastructure Polygon<br/>(Confidence: Calibrated | Structural Radar Return)"]
    end

    OptFeed --> CloudDetect
    SARFeed --> DielectricEval & DoubleBounce

    CloudDetect -- "Clear Sky (No Clouds)" --> RuleOpticalAgreement
    CloudDetect -- "Heavy Cloud Cover" --> DielectricEval

    DielectricEval -- "Yes (σ° < -18 dB)" --> RuleCloudWater
    DoubleBounce -- "Yes (σ° > -6 dB)" --> RuleUrban

    RuleOpticalAgreement --> HighConfidenceWater
    RuleCloudWater --> AllWeatherWater
    RuleUrban --> BuiltUpVector
```

---

## 5. Public API Interface

The system exposes a clean REST API compliant with OpenAPI 3.1:
- `POST /api/frontier/investigate-geotiff`: Executes real-time physical investigation on uploaded or cataloged GeoTIFFs.
- `GET /api/demo-corpus/manifest`: Returns authoritative metadata for the 20 real Earth Observation scenes.
- `GET /api/frontier/reports/{id}`: Downloads verified cryptographic JSON/Markdown audit dossiers.

*Full specification available at:* [`api/sanitized_openapi.json`](api/sanitized_openapi.json).
