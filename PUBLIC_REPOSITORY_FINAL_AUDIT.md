# SatQuery AI — Public Repository Forensic Content Audit

**Audit Date:** September 22, 2026  
**Auditor:** Team STARFORGE Internal Audit  
**Target Package:** `https://github.com/Gowrav-M/satquery-ai-sih-2026-evidence`  
**Overall Package Status:** **READY FOR HUMAN REVIEW** (Do not push to GitHub yet)

---

## 1. Master Public Repository File Audit Table (48 Files)

| File | Purpose | Evidence-backed? | Human-written? | Sensitive? | Publish? | Reason |
| :--- | :--- | :---: | :---: | :---: | :---: | :--- |
| `README.md` | Master repository index, problem statement, architecture, hero summaries, limitations | **YES** | **YES** | **NO** | **YES** | Core entry point; provides non-reusable technical overview and links to evidence |
| `SIH_PROBLEM_STATEMENT.md` | Complete mapping to ISRO / SAC Problem Statement 26167 | **YES** | **YES** | **NO** | **YES** | Essential context mapping requirements directly to hackathon criteria |
| `SIH_REQUIREMENT_TRACEABILITY.md` | Requirement-by-requirement traceability matrix across 9 SIH criteria & 8 clauses | **YES** | **YES** | **NO** | **YES** | Formal compliance evidence with transparent disclosure of partial capabilities |
| `ARCHITECTURE.md` | Technical documentation of the 4 decoupled system layers and dataflows | **YES** | **YES** | **NO** | **YES** | High-level system architecture; no proprietary algorithm source code exposed |
| `SCIENTIFIC_METHODS.md` | Mathematical formulations for NDWI, NDVI, NDBI, Lee filter, dB, Nyquist barrier | **YES** | **YES** | **NO** | **YES** | Standard scientific literature equations; proves technical depth without code leak |
| `MODEL_ADAPTATION.md` | Registry of adapted neural models, parameter counts, LoRA recipes, runtime policies | **YES** | **YES** | **NO** | **YES** | Documents machine learning governance, parameter counts, and guardrails |
| `DATA_PROVENANCE.md` | Documentation of the 20 real Sentinel-1/2 scenes across India | **YES** | **YES** | **NO** | **YES** | Certifies authentic data provenance under CC-BY-SA 3.0 IGO open access terms |
| `BENCHMARKS.md` | Authoritative benchmark table with reconciled empirical metrics | **YES** | **YES** | **NO** | **YES** | Verified empirical metrics (RSVQA 29.4%, CDVQA 59%, DLT 0.6907; unproven marked N/A) |
| `VALIDATION.md` | Summary of automated regression suite (30/33 passed, 3 edge cases, 90.9%) | **YES** | **YES** | **NO** | **YES** | Transparent quality assurance summary showing real test execution |
| `LIMITATIONS.md` | Technical disclosure of conifer boundary recall, bathymetry, VQA calibration, counting | **YES** | **YES** | **NO** | **YES** | Essential scientific transparency distinguishing real engineering from marketing |
| `REPRODUCIBILITY.md` | Technical evidence verification guide and SHA-256 validation commands | **YES** | **YES** | **NO** | **YES** | Explains verification methodology and public/private boundary clearly |
| `BENCHMARK_TRUTH_AUDIT.md` | Internal audit trail showing historical reconciliation of all benchmark numbers | **YES** | **YES** | **NO** | **YES** | Demonstrates rigorous forensic discipline and zero-overclaim enforcement |
| `HERO_DEMO_TRUTH_AUDIT.md` | Truth audit verifying sensor metadata, dates, and locations for the 3 hero demos | **YES** | **YES** | **NO** | **YES** | Proves all demonstration claims are anchored in genuine GeoTIFF metadata |
| `FINAL_MODEL_RUNTIME_TRUTH.md` | Audit distinguishing configured vs actually executed models in production | **YES** | **YES** | **NO** | **YES** | Transparently documents live Gemini execution vs Tier 0 AgentRouter configuration |
| `api/sanitized_openapi.json` | Sanitized OpenAPI 3.1 REST schema (41 endpoints matching live FastAPI app) | **YES** | **YES** | **NO** | **YES** | Proves complete API contract for local deployment (`http://127.0.0.1:8000`); no keys |
| `architecture/agentic_workflow.png` | 4-stage agentic reasoning flow diagram | **YES** | **YES** | **NO** | **YES** | Architectural visual asset; high-DPI |
| `architecture/evidence_graph.png` | 8-stage cryptographic DAG architecture diagram | **YES** | **YES** | **NO** | **YES** | Architectural visual asset; high-DPI |
| `architecture/scientific_gatekeeper.png` | Cross-sensor contradiction arbitration flowchart | **YES** | **YES** | **NO** | **YES** | Architectural visual asset; high-DPI |
| `architecture/specialist_dispatch.png` | Dynamic specialist tool routing architecture diagram | **YES** | **YES** | **NO** | **YES** | Architectural visual asset; high-DPI |
| `architecture/system_architecture.png` | Master end-to-end multi-tier system architecture diagram | **YES** | **YES** | **NO** | **YES** | Architectural visual asset; high-DPI |
| `benchmark-results/CDVQA_summary.json` | Reconciled machine-readable CDVQA evaluation summary (200 test pairs, 59% hybrid) | **YES** | **YES** | **NO** | **YES** | Machine-readable benchmark artifact matching disk evaluation log |
| `benchmark-results/RSVQA_summary.json` | Reconciled machine-readable RSVQA summary (500 items, 29.4% top-1, ECE 25.26%) | **YES** | **YES** | **NO** | **YES** | Machine-readable benchmark artifact matching disk evaluation log |
| `benchmark-results/benchmark_notes.md` | Explanatory notes on counting/attribute limits and calibration Immediate Null Policy | **YES** | **YES** | **NO** | **YES** | Contextual technical notes preventing misinterpretation of benchmark numbers |
| `demo/DEMO_VIDEO.md` | Demo video outline, chapter breakdown, and unlisted YouTube link plan | **YES** | **YES** | **NO** | **YES** | Video navigation reference for evaluators |
| `demo/demo_timeline.md` | Minute-by-minute presentation script for the 6-minute evaluation slot | **YES** | **YES** | **NO** | **YES** | Structured demonstration script matching Slides 1 through 6 |
| `demos/hero_01_water.png` | Live console screenshot: Chilika Lagoon 2,278.4 ha water delineation | **YES** | **YES** | **NO** | **YES** | Authentic UI proof from live browser execution |
| `demos/hero_01_water_detail.png` | Zoomed screenshot: raster histogram and vector boundary overlay | **YES** | **YES** | **NO** | **YES** | Detailed visual evidence of raster calculation |
| `demos/hero_02_optical_sar.png` | Live console screenshot: Bengaluru optical-SAR cloud penetration with split curtain | **YES** | **YES** | **NO** | **YES** | Authentic UI proof from live browser execution |
| `demos/hero_02_trace.png` | Live console screenshot: multi-sensor evidence trace and radar properties | **YES** | **YES** | **NO** | **YES** | Authentic UI proof showing physical backscatter values |
| `demos/hero_02_curtain_detail.png` | Zoomed screenshot: interactive Leaflet split curtain comparison | **YES** | **YES** | **NO** | **YES** | Detailed visual proof of interactive GIS capability |
| `demos/hero_03_bitemporal.png` | Live console screenshot: Bengaluru urban built-up expansion (+36.4 ha) | **YES** | **YES** | **NO** | **YES** | Authentic UI proof from live browser execution |
| `demos/hero_03_change_detail.png` | Zoomed screenshot: red difference flux identifying new construction | **YES** | **YES** | **NO** | **YES** | Detailed visual proof of bi-temporal change detection |
| `demos/nyquist_abstention.png` | Live console screenshot: Nyquist spatial sampling barrier ($2\times\text{GSD}$) banner | **YES** | **YES** | **NO** | **YES** | Authentic UI proof of epistemic abstention |
| `models/adaptation_evidence/adaptation_summary.md` | Summary of fine-tuning protocols, parameter counts, and LoRA configs | **YES** | **YES** | **NO** | **YES** | ML governance documentation; no binary weights |
| `models/checkpoint_hashes.txt` | Cryptographic SHA-256 hashes of all foundation and adapted checkpoints | **YES** | **YES** | **NO** | **YES** | Cryptographic verification proof; hashes verified against on-disk checkpoint files |
| `models/model_cards/cdvqa_siamese.md` | Model card: CDVQA Siamese difference network | **YES** | **YES** | **NO** | **YES** | Standard ML model documentation |
| `models/model_cards/croma_base.md` | Model card: CROMA-Base and `CROMA_LIMITED_EVIDENCE` operating constraint | **YES** | **YES** | **NO** | **YES** | Standard ML model documentation |
| `models/model_cards/florence2_rs_lora.md` | Model card: Florence-2-RS-LoRA and Immediate Null Policy | **YES** | **YES** | **NO** | **YES** | Standard ML model documentation |
| `models/model_cards/segformer_b0_dlt.md` | Model card: SegFormer-B0 10-band encoder and Copernicus DLT performance | **YES** | **YES** | **NO** | **YES** | Standard ML model documentation |
| `provenance/model_manifest.json` | Verified JSON model registry with parameter counts and runtime status | **YES** | **YES** | **NO** | **YES** | Machine-readable model governance metadata |
| `provenance/scenario_manifest.csv` | Machine-readable registry of 20 scenes with WGS-84 coords, CRS, GSD, SHA-256 | **YES** | **YES** | **NO** | **YES** | Data provenance certification; 20/20 verified |
| `provenance/source_provenance.md` | Upstream satellite attribution for ESA Copernicus and AWS Open Data | **YES** | **YES** | **NO** | **YES** | Legal licensing and attribution compliance |
| `reports/final_demo_runbook.md` | Step-by-step evaluation runbook detailing acts 1 through 6 | **YES** | **YES** | **NO** | **YES** | Practical guide for evaluators; updated with verified locations and dates |
| `validation/acceptance_matrix.md` | Contract-by-contract functional acceptance verification matrix | **YES** | **YES** | **NO** | **YES** | Acceptance test evidence; updated dates |
| `validation/corpus_integrity.md` | 20-scene GeoTIFF integrity and spatial CRS audit (20/20 certified) | **YES** | **YES** | **NO** | **YES** | Quality assurance evidence |
| `validation/provider_truthfulness.md` | Provider failover telemetry and value-locking safeguards | **YES** | **YES** | **NO** | **YES** | System resilience documentation |
| `validation/regression_summary.md` | Automated test suite execution summary (30/33 passed, 3 edge cases analyzed) | **YES** | **YES** | **NO** | **YES** | Transparent QA test evidence |
| `validation/specialist_bypass_results.md` | Fault tolerance verification when individual specialist tools are disabled | **YES** | **YES** | **NO** | **YES** | Reliability and resilience evidence |

---

## 2. Policy Adherence Checklist
- [x] **Zero Source Code:** No Python (`.py`), React/TypeScript (`.tsx`, `.ts`), or internal training pipelines.
- [x] **Zero Credentials:** Scanned across 6 regex patterns; exactly 0 credentials found.
- [x] **Zero Ungrounded Benchmark Claims:** RSVQA (29.40%), CDVQA (59.00%), DLT (0.6907). VRSBench marked NOT EVALUATED. Private ISRO marked PRIVATE / NOT PROVEN.
- [x] **Consistent Hero Truth:** Hero 02 is Bengaluru Urban; Hero 03 dates are May 12, 2026 vs September 19, 2026 across all files.
- [x] **Consistent Presentation Structure:** Deck consists of Slides 1 to 6; Slide 6 contains supplementary Technical Evidence QR codes; no references to Slides 7 or 8.
- [x] **Human Writing Quality:** Banned marketing buzzwords eliminated; objective engineering tone enforced.
- [x] **DO NOT PUSH TO GITHUB:** Staged locally only. Requires explicit manual human review.
