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

```
┌────────────────────────────────────────────────────────────────────────┐
│               TIER 1: INTERACTION & LOCALIZATION LAYER                 │
│  • React 18 / TypeScript / Leaflet Analyst Web Console                 │
│  • 3-Way Persona Switcher (Farmer / District Collector / Scientist)    │
│  • Multilingual Indic Speech-to-Text & TTS (Sarvam AI API)             │
│  • Split-Curtain Swipe & Interactive Pixel Probe Inspector             │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ REST / JSON (Sanitized OpenAPI)
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│            TIER 2: AGENTIC ORCHESTRATION & DISCOVERY BRAIN             │
│  • Query Contract Validator (Spatial AST & Modality Intent Resolver)   │
│  • Competing Hypothesis Ledger (Prior & Posterior Evidence Tracking)   │
│  • Value-of-Evidence (VOE) Next-Action Selector & Replanner            │
│  • Multi-Tier Provider Failover (High-Throughput / Local Physics Mode) │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Structured Next-Best Action
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│           TIER 3: SPECIALIST DISPATCH & FOUNDATION FOUNDRY             │
│  • SingleImageSpecialist: Real Multispectral Pixel Math (NDWI / NDVI)  │
│  • SensorAwareSARProcessor: Lee 5x5 Filter, dB Radiometric Calibration │
│  • CROMA-Base Specialist: 194.3M Joint Optical-Radar Latent Alignment  │
│  • SegFormer-B0 Specialist: 10-Band Multi-Spectral Canopy Segmentation │
│  • BiTemporalSpecialist: 2D Fourier Shift & Differential Clustering    │
│  • PhysicalGISEngine: Affine Geodesic Area (Hectares / Acres)          │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Verified Radiometric Measurements
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│           TIER 4: SCIENTIFIC TRUST & CRYPTOGRAPHIC PROVENANCE          │
│  • 8-Stage Immutable Cryptographic Evidence Graph (DAG with SHA-256)   │
│  • Spatial Nyquist-Shannon Sampling Guardrail (2x GSD Barrier)         │
│  • Fourier 2D Phase Correlation Barrier (<6.0 px Barrier)              │
│  • Multi-Format Exporter: Peer-Review Markdown, JSON, & PDF Briefings   │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 3. The 8-Stage Cryptographic Evidence Graph (DAG)

Every investigation generates an immutable directed acyclic graph where each node contains the SHA-256 cryptographic digest of its inputs and state:

```
[Node 1: User Query & Intent AST]
       │
       ▼
[Node 2: Competing Hypotheses Formulation]
       │
       ▼
[Node 3: Satellite Asset Registration & SHA-256 Digest]
       │
       ▼
[Node 4: Specialist Action & Parameter Ingestion]
       │
       ▼
[Node 5: Empirical Radiometric Measurements (Pixels)]
       │
       ▼
[Node 6: Cross-Sensor Contradiction Arbitration]
       │
       ▼
[Node 7: Evidence Sufficiency Verification]
       │
       ▼
[Node 8: Final Synthesized Finding & Polygon Vector]
```

### Integrity Guarantee:
If any downstream parameter or finding is altered, the cryptographic chain hash is invalidated. This enables automated auditability for ISRO mission archives.

---

## 4. Public API Interface

The system exposes a clean REST API compliant with OpenAPI 3.1:
- `POST /api/frontier/investigate-geotiff`: Executes real-time physical investigation on uploaded or cataloged GeoTIFFs.
- `GET /api/demo-corpus/manifest`: Returns authoritative metadata for the 20 real Earth Observation scenes.
- `GET /api/frontier/reports/{id}`: Downloads verified cryptographic JSON/Markdown audit dossiers.

*Full specification available at:* [`api/sanitized_openapi.json`](api/sanitized_openapi.json).
