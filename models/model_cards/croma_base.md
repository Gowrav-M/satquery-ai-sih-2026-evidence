# Model Card: CROMA-Base (Cross-Modal Foundation Model)
## SIH 2026 Problem Statement 26167 (ISRO / SAC) | Model Evidence

---

### 1. Basic Metadata
- **Model Name:** CROMA-Base (Cross-Modal Alignment)
- **Primary Task:** Joint Optical + SAR Latent Representation Alignment
- **Architecture:** Dual unimodal ViT encoders with 2D ALiBi positional biases and bidirectional cross-attention
- **Parameters:** 194,365,440
- **Input Channels:** 12-channel Sentinel-2 (Optical) + 2-channel Sentinel-1 (VV/VH Radar)
- **Checkpoint SHA-256:** `0238d814b53108f3ad3b5b152d04f2f01f8d9b1c93a0a6d09e51c22bc8c58f9a`
- **File Size:** 777.6 MB (`CROMA_base.pt`)
- **Upstream Authors:** Anthony Fuller et al. (CVPR / NeurIPS)
- **License:** MIT / Academic Research

---

### 2. Operational Adoption Policy
SatQuery AI enforces a strict scientific guardrail:
$$\textbf{CROMA\_LIMITED\_EVIDENCE Policy}$$
- **Role:** Evaluated strictly as representation alignment evidence.
- **Guardrail:** The neural cross-attention score informs multimodal concordance, but **cannot override empirical raster reflectance or radar backscatter decibels**. If optical shows cloud and SAR shows specular water, physical radar wave penetration takes precedence over latent representations.
