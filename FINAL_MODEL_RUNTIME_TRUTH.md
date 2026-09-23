# SatQuery AI — Final Model Runtime Truth Audit

**Audit Date:** September 22, 2026  
**Auditor:** Team STARFORGE Internal Audit (Zero-Overclaim Mandate)  
**Strict Principle:** *"Configured" != "Executed"* and *"Checkpoint exists" != "Runtime used"*.

---

## 1. Master Model Runtime Truth Matrix

| Model / Provider | Purpose | Configured? | Actually Executed? | Forensic Evidence | Fallback Position | Public Wording |
| :--- | :--- | :---: | :---: | :--- | :--- | :--- |
| **Gemini 3.5 Flash-Lite / 1.5 Flash** (`GEMINI`) | Natural language intent extraction, competing hypothesis generation, grounded scientific synthesis | **YES** | **YES (LIVE_VERIFIED)** | `hero_demos_interceptions.json` logs 3 live calls in `inv_real_a944bdbf` (latencies: 250ms, 1428ms, 2372ms); `hero_01_water.png` console capture | Active primary runtime engine in current deployment environment | **Cloud API Multi-Modal Reasoning Engine (Google Gemini Flash)** |
| **DeepSeek-V4-Flash** (`AGENTROUTER`) | Multi-billion parameter structured DAG decomposition & reasoning | **YES** | **NO (CONFIGURED — EXECUTION NOT VERIFIED)** | `AGENTROUTER_API_KEY` was not exported in runtime shell; provider manager cascaded to Gemini in live verification | Tier 0 in architectural hierarchy; not executed in current live demo runs | **CONFIGURED — EXECUTION NOT VERIFIED** *(Architectural Tier 0; live runs executed via Gemini Flash)* |
| **Nemotron 3 Ultra / Llama 3.3 70B** (`OPENROUTER` / `NVIDIA NIM`) | Enterprise open-weights instruction following fallback | **YES** | **NO (CONFIGURED — FALLBACK)** | Provider telemetry ledger shows 0 requests routed to OpenRouter/NIM during verified demo runs because Gemini succeeded | Tier 2 / Tier 3 Standby Failover | **CONFIGURED — STANDBY FALLBACK** *(Execution not triggered during demo runs)* |
| **PhysicalGISEngine** (Analytical Raster Physics) | Authoritative radiometric indices (NDWI, NDVI, NDBI), 2D Fourier phase-shift check, calibrated SAR dB conversion, hectare polygonization | **YES** | **YES (LIVE_VERIFIED)** | `hero_demos_interceptions.json` records 2,278.4 ha calculation, $NDWI \ge 0.15$ raster mask, and Fourier shift $0.21\text{ px}$ | Non-fallback; authoritative deterministic ground truth | **Deterministic Physical Remote Sensing Engine (NumPy / Rasterio / GDAL)** |
| **Florence-2-RS-LoRA** | Text-guided bounding-box grounding and single-image remote sensing VQA | **YES** | **YES (BENCHMARK & SPECIALIST)** | Checkpoint on disk: `models/checkpoints/florence2_rs_lora_best`; evaluated on RSVQA-LR (29.40% Overall, 53.71% Presence in `VQA_COMPLIANCE_MATRIX.md`) | Local Vision-Language Specialist (Enforces Immediate Null Policy: `confidence = null`) | **Adapted Florence-2 Vision-Language Specialist** *(Evaluated on RSVQA-LR; enforces Immediate Null Policy)* |
| **SegFormer-B0 (10-Band Multi-Spectral)** | 10-band multi-spectral forest canopy segmentation (Dominant Leaf Type) | **YES** | **YES (BENCHMARK & SPECIALIST)** | Checkpoint on disk: `models/checkpoints/segformer_b0_dlt_best`; measured 0.6907 mIoU on 3,000 Copernicus DLT tiles (`evaluate_segformer_baseline.py`) | Local Optical Segmentation Specialist | **10-Band Multi-Spectral Canopy Specialist** *(Evaluated on Copernicus DLT: 0.6907 mIoU)* |
| **CROMA-Base** (194.3M parameters) | Joint optical-SAR cross-attention latent alignment | **YES** | **YES (INTEGRATION TEST)** | Validated in `tests/test_croma_phase25_integration.py`; operates strictly under `CROMA_LIMITED_EVIDENCE` | Local Multimodal Alignment Specialist | **CROMA Optical-SAR Latent Alignment Model** *(194.3M params; restricted to supporting evidence under CROMA_LIMITED_EVIDENCE)* |
| **Siamese Difference Head** (CDVQA) | Bi-temporal change detection and direction quantification | **YES** | **YES (BENCHMARK)** | Measured 59.00% Hybrid accuracy across 200 CDVQA test samples (`benchmarks/cdvqa_phase14_evaluation.json`) | Local Bi-Temporal Specialist (Subject to 2D Fourier barrier $<6.0\text{ px}$) | **Bi-Temporal Siamese Change Specialist** *(Evaluated on CDVQA: 59.00% Hybrid Accuracy)* |
| **Local Deterministic State Machine Fallback** | 100% offline rule-based query parser and execution planner | **YES** | **YES (OFFLINE VERIFIED)** | Validated in `tests/test_specialist_bypass_resilience.py` with zero network access | Tier 4 Total Network Disconnect Failover | **Offline Deterministic State Machine Fallback** *(Zero-network operational guarantee)* |

---

## 2. Critical Runtime Truth Insights
1. **Primary Reasoning Provider in Current Live System:** Google Gemini Flash is the active reasoning provider verified in current live browser recordings (`hero_demos_interceptions.json`), achieving ~250ms to 2.3s latency.
2. **DeepSeek-V4-Flash Status:** Fully implemented in `real_providers.py` as Tier 0, but during current live evaluations it was not triggered because the environment variable was not set in the shell session. Public documentation must state: **CONFIGURED — EXECUTION NOT VERIFIED**.
3. **Specialist Governance:** Foundation models (`CROMA-Base`, `Florence-2`, `SegFormer-B0`) exist on disk and have verified benchmark evaluation records. However, their live outputs are strictly bound by deterministic physics guardrails (`CROMA_LIMITED_EVIDENCE`, Immediate Null Policy, Fourier co-registration barrier).
