# Model Card: SegFormer-B0 10-Band Multi-Spectral
## SIH 2026 Problem Statement 26167 (ISRO / SAC) | Model Evidence

---

### 1. Basic Metadata
- **Model Name:** SegFormer-B0 DLT Multi-Spectral Baseline
- **Primary Task:** 10-Band Copernicus Dominant Leaf Type (DLT 2018) Forest Canopy Partitioning
- **Architecture:** MiT-B0 Multi-Spectral Hierarchical Transformer
- **Parameters:** 3,714,563
- **Input Channels:** 10 Sentinel-2 bands: B02, B03, B04, B05, B06, B07, B08, B8A, B11, B12
- **Checkpoint SHA-256:** `0129f4549cfd3216c31268c3adadb0b5c10d50deb6d716c8852c119ea541712c`
- **File Size:** 14.3 MB (`pytorch_model.bin`)
- **License:** Apache 2.0

---

### 2. Empirical Benchmark Performance
- **Validation Dataset:** Copernicus DLT 2018 + Sentinel-2 European Montane/Temperate Forest Biomes
- **Overall Mean IoU:** **0.6907**
- **Broadleaved Forest IoU:** **0.7765**
- **Non-Tree Class IoU:** **0.7820**
- **Coniferous Forest IoU:** **0.5136**
- **Known Limitation:** Coniferous recall drops to $31.32\%$ at canopy edges ($\le 10\text{m}$) due to mixed pixels.
