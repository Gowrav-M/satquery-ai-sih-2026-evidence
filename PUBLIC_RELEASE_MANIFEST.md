# SatQuery AI — Public Release Manifest

**Repository:** `SatQuery-AI-SIH-2026-Evidence`  
**Problem Statement:** SIH 2026 — PS 26167 (ISRO / SAC)  
**Team:** STARFORGE  
**Release Type:** Technical Evidence Package (Documentation & Provenance Only)  
**Publication Status:** READY FOR MANUAL PUBLICATION — NOT YET PUSHED TO GITHUB

---

## Public Evidence File Matrix

| Path | Type | Purpose | Evidence-backed? | Contains source code? | Contains sensitive data? | Publish? |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| `.gitignore` | Configuration | Git exclusion rules for private weights, source, and .env files | Yes | No | No | **PUBLISH** |
| `README.md` | Core Documentation | Master project documentation, architecture, hero demos, and benchmarks | Yes | No | No | **PUBLISH** |
| `SIH_PROBLEM_STATEMENT.md` | Context | Official Problem Statement 26167 scope, requirements, and background | Yes | No | No | **PUBLISH** |
| `SIH_REQUIREMENT_TRACEABILITY.md` | Compliance | Traceability matrix mapping SIH parameters to architectural components | Yes | No | No | **PUBLISH** |
| `ARCHITECTURE.md` | Technical | Four-tier topology, 8-stage DAG, specialist dispatch, and arbitration | Yes | No | No | **PUBLISH** |
| `SCIENTIFIC_METHODS.md` | Scientific | Spectral index formulas, SAR calibration, Nyquist limit, and co-registration | Yes | No | No | **PUBLISH** |
| `MODEL_ADAPTATION.md` | Model Documentation | Foundation model fine-tuning, training hyperparameters, and runtime status | Yes | No | No | **PUBLISH** |
| `DATA_PROVENANCE.md` | Provenance | 20-scene satellite data catalog, acquisition dates, CRS, and open licensing | Yes | No | No | **PUBLISH** |
| `BENCHMARKS.md` | Benchmark Documentation | RSVQA-LR, CDVQA, and DLT methodology, results, and calibration analysis | Yes | No | No | **PUBLISH** |
| `VALIDATION.md` | Testing | End-to-end regression test results, fault tolerance, and mock verification | Yes | No | No | **PUBLISH** |
| `LIMITATIONS.md` | Technical | Known system boundaries, conifer edge recall, bathymetry, and VQA limits | Yes | No | No | **PUBLISH** |
| `REPRODUCIBILITY.md` | Audit Guide | Verification protocol for evaluators, hash checks, and artifact inspection | Yes | No | No | **PUBLISH** |
| `PUBLIC_RELEASE_SECURITY_CHECK.md` | Security Audit | Automated pre-publication security scan and credential verification | Yes | No | No | **PUBLISH** |
| `PUBLIC_RELEASE_MANIFEST.md` | Release Manifest | Complete inventory of public release files and verification status | Yes | No | No | **PUBLISH** |
| `FINAL_JUDGE_READTHROUGH.md` | Evaluation Audit | Full document-by-document audit against 10 evaluation criteria | Yes | No | No | **PUBLISH** |
| `JUDGE_QUICK_ANSWERS.md` | Evaluation Guide | Fact-backed direct answers to 12 core judge questions | Yes | No | No | **PUBLISH** |
| `FINAL_PUBLIC_RELEASE_SCORECARD.md` | Readiness Scorecard | Internal readiness evaluation across 10 technical categories | Yes | No | No | **PUBLISH** |
| `api/sanitized_openapi.json` | API Contract | OpenAPI 3.1 schema for local evaluation without exposing routing logic | Yes | No | No | **PUBLISH** |
| `architecture/agentic_workflow.png` | Architecture Visual | Query parsing, contract checking, and specialist dispatch workflow | Yes | No | No | **PUBLISH** |
| `architecture/evidence_graph.png` | Architecture Visual | 8-stage cryptographic Directed Acyclic Graph structure | Yes | No | No | **PUBLISH** |
| `architecture/scientific_gatekeeper.png` | Architecture Visual | Cross-sensor contradiction arbitration and physical barrier logic | Yes | No | No | **PUBLISH** |
| `architecture/specialist_dispatch.png` | Architecture Visual | Domain specialist engine routing and parameter dispatch | Yes | No | No | **PUBLISH** |
| `architecture/system_architecture.png` | Architecture Visual | Master four-tier system architecture overview | Yes | No | No | **PUBLISH** |
| `benchmark-results/benchmark_notes.md` | Benchmark Notes | Detailed category breakdowns, metric formulas, and calibration tables | Yes | No | No | **PUBLISH** |
| `benchmark-results/CDVQA_summary.json` | Benchmark Artifact | Machine-readable CDVQA evaluation metrics (200 samples) | Yes | No | No | **PUBLISH** |
| `benchmark-results/RSVQA_summary.json` | Benchmark Artifact | Machine-readable RSVQA-LR evaluation metrics (500 items) | Yes | No | No | **PUBLISH** |
| `demo/demo_timeline.md` | Walkthrough | 6-minute demonstration video timeline, chapter markers, and narration | Yes | No | No | **PUBLISH** |
| `demo/DEMO_VIDEO.md` | Video Link | Demo video link status and chapter timestamps | Yes | No | No | **PUBLISH** |
| `demos/hero_01_water.png` | Forensic Evidence | Chilika Lagoon open-water delineation map console screenshot | Yes | No | No | **PUBLISH** |
| `demos/hero_01_water_detail.png` | Forensic Evidence | Chilika Lagoon pixel probe radiometry and geodesic area calculation | Yes | No | No | **PUBLISH** |
| `demos/hero_02_optical_sar.png` | Forensic Evidence | Bengaluru optical reflectance vs Sentinel-1 C-SAR backscatter | Yes | No | No | **PUBLISH** |
| `demos/hero_02_curtain_detail.png` | Forensic Evidence | Interactive split-curtain swipe tool comparing optical and radar | Yes | No | No | **PUBLISH** |
| `demos/hero_02_trace.png` | Forensic Evidence | Execution trace timeline and multi-sensor contradiction arbitration log | Yes | No | No | **PUBLISH** |
| `demos/hero_03_bitemporal.png` | Forensic Evidence | Bengaluru bi-temporal urban change detection with vector overlay | Yes | No | No | **PUBLISH** |
| `demos/hero_03_change_detail.png` | Forensic Evidence | Fourier phase co-registration offset and change polygon detail | Yes | No | No | **PUBLISH** |
| `demos/nyquist_abstention.png` | Forensic Evidence | Adversarial sub-resolution query refusal under Nyquist-Shannon limit | Yes | No | No | **PUBLISH** |
| `models/checkpoint_hashes.txt` | Verification Hash | Cryptographic SHA-256 digests for all private neural checkpoints | Yes | No | No | **PUBLISH** |
| `models/adaptation_evidence/adaptation_summary.md` | Model Documentation | LoRA adaptation parameters, training loss curves, and evaluation setup | Yes | No | No | **PUBLISH** |
| `models/model_cards/cdvqa_siamese.md` | Model Card | CDVQA Siamese change detection architecture, weights hash, and scope | Yes | No | No | **PUBLISH** |
| `models/model_cards/croma_base.md` | Model Card | CROMA-Base joint optical-SAR embedder card and limited evidence scope | Yes | No | No | **PUBLISH** |
| `models/model_cards/florence2_rs_lora.md` | Model Card | Florence-2 remote sensing visual grounding LoRA model card | Yes | No | No | **PUBLISH** |
| `models/model_cards/segformer_b0_dlt.md` | Model Card | SegFormer-B0 10-band canopy segmentation model card and mIoU | Yes | No | No | **PUBLISH** |
| `provenance/model_manifest.json` | Metadata | Machine-readable model metadata, parameter counts, and target tasks | Yes | No | No | **PUBLISH** |
| `provenance/scenario_manifest.csv` | Catalog | 20-scene satellite acquisition catalog with dates, CRS, and URLs | Yes | No | No | **PUBLISH** |
| `provenance/source_provenance.md` | Provenance | Satellite data providers, ESA Copernicus open access, and licensing | Yes | No | No | **PUBLISH** |
| `reports/final_demo_runbook.md` | Runbook | 6-act evaluator demonstration runbook with step-by-step instructions | Yes | No | No | **PUBLISH** |
| `validation/acceptance_matrix.md` | Testing | Functional acceptance test criteria, test inputs, and pass/fail status | Yes | No | No | **PUBLISH** |
| `validation/corpus_integrity.md` | Data Audit | Metadata verification for 20-scene GeoTIFF test corpus | Yes | No | No | **PUBLISH** |
| `validation/provider_truthfulness.md` | Testing | Multi-tier provider latency benchmarks, failover, and mock verification | Yes | No | No | **PUBLISH** |
| `validation/regression_summary.md` | Testing | Automated regression test suite logs, pass rates, and root cause notes | Yes | No | No | **PUBLISH** |
| `validation/specialist_bypass_results.md` | Testing | Fault tolerance under simulated specialist outage and offline fallback | Yes | No | No | **PUBLISH** |

---

## Boundary Declaration

```
SOURCE CODE:
PRIVATE

PRIVATE ISRO/SAC EVALUATION DATA:
PRIVATE

SECRETS:
EXCLUDED

DEMO VIDEO:
UNLISTED — URL PENDING
```
