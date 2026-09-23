# SatQuery AI — Remote-Sensing Model Adaptation
## Model Registry & Fine-Tuning Evidence | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

> [!IMPORTANT]
> **Operational Status Distinction:**  
> In scientific machine learning, **CHECKPOINT EXISTS on disk is NOT equivalent to CHECKPOINT USED IN LIVE PRODUCTION**.  
> This document explicitly identifies which weights run in active live execution vs which serve as offline empirical research baselines.

---

## 1. Master Model Adaptation Registry

| Model Name | Role | Base Model | Adaptation Method | Training Dataset | Checkpoint SHA-256 | Live Production Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **CROMA-Base** | Cross-Modal Latent Alignment | 12-ch Optical + 2-ch Radar ViT | Joint Contrastive Cross-Attention | Global Paired Sentinel-1/2 Tiles | `0238d814b531...574b` | **LIVE_EXECUTED** (Integration test verified; under `CROMA_LIMITED_EVIDENCE` policy) |
| **SegFormer-B0 DLT** | 10-Band Multi-Spectral Canopy Segmentation | MiT-B0 Multi-Spectral Transformer | Multi-Spectral Fine-Tuning (Unweighted CE) | Copernicus DLT 2018 + Sentinel-2 L2A | `0129f4549cfd...712c` | **BENCHMARK_ONLY** (Evaluated on Copernicus DLT; not in live investigation loop) |
| **Florence-2-RS-LoRA** | Visual Grounding & Scene Captioning | `microsoft/Florence-2-base` (232M) | PEFT LoRA (Rank 16, Alpha 32) | BigEarthNet RS + RS Grounding & VQA Datasets | `741681f95a5e...1673` | **LIVE_EXECUTED** (Text-guided bounding box grounding; VQA enforces Immediate Null Policy) |
| **CDVQA Siamese** | Bi-Temporal Change VQA | Siamese Dual-Branch ResNet/ViT | Condition B Temporal Regularization | CDVQA Bi-temporal Benchmark | `b9a0be3cae0c...7101` | **BENCHMARK_ONLY** (Offline evaluation on 200 CDVQA samples) |
| **Primary Agent Brain** | Query Intent & Orchestration | Multi-Tier Cascade (DeepSeek-V4-Flash / Gemini / Nemotron) | Multi-Billion Frontier Pretraining | Structured EO Reasoning & JSON Schema | Cloud API / Local Deterministic Fallback | **LIVE_EXECUTED** (Gemini Flash verified; DeepSeek CONFIGURED — NOT VERIFIED) |

---

## 2. Adaptation Details by Architecture

### 2.1 Florence-2 Remote Sensing LoRA
- **Base Architecture:** Microsoft Florence-2-base sequence-to-sequence vision-language model.
- **Adaptation Strategy:** Low-Rank Adaptation (LoRA) applied to self-attention projection matrices ($W_q, W_v$) with rank $r=16$ and scaling $\alpha=32$.
- **Training Objective:**
  1. *Visual Grounding:* Generating normalized bounding coordinates `[ymin, xmin, ymax, xmax]` from natural language phrases (e.g., *"water reservoir"*, *"agricultural parcel"*).
  2. *Scene Captioning:* Generating remote-sensing descriptive captions with sensor metadata awareness.
- **Safety Guardrail:** If Florence-2 detects zero candidate bounding boxes, it emits `UNRESOLVED_GROUNDING` with `grounding_success: false`. The system never synthesizes fake bounding boxes.

### 2.2 SegFormer-B0 10-Band Multi-Spectral Baseline
- **Input Channels:** 10 Sentinel-2 multispectral bands: B02 (Blue), B03 (Green), B04 (Red), B05 (RE1), B06 (RE2), B07 (RE3), B08 (NIR), B8A (Narrow NIR), B11 (SWIR1), B12 (SWIR2).
- **Target Classes:** Copernicus DLT 2018 classes:
  - Class 0: Non-tree land cover
  - Class 1: Broadleaved forest
  - Class 2: Coniferous forest
- **Empirical Metrics:** Calibrated test mIoU of **0.6907** (Broadleaved forest IoU: **0.7765**, Coniferous forest IoU: **0.5136**).

### 2.3 CROMA-Base Foundation Model Integration
- **Parameter Count:** 194,365,440 parameters.
- **Architecture:** Dual unimodal ViT encoders processing 12-channel Sentinel-2 optical and 2-channel Sentinel-1 SAR imagery, fused via bidirectional cross-attention layers.
- **Adoption Policy (`CROMA_LIMITED_EVIDENCE`):** Evaluated strictly as representation alignment evidence. The cross-attention alignment score informs multimodal concordance, but cannot override empirical raster reflectance or radar backscatter decibels.
