# Model Card: SegFormer-B0 10-Band Multi-Spectral
## SIH 2026 Problem Statement 26167 (ISRO / SAC) | Model Evidence

---

### 1. Basic Metadata
- **Model Name:** SegFormer-B0 DLT Multi-Spectral Baseline
- **Primary Task:** 10-Band Copernicus Dominant Leaf Type (DLT 2018) Forest Canopy Partitioning
- **Architecture:** MiT-B0 Multi-Spectral Hierarchical Transformer
- **Parameters:** 3,714,563
- **Input Channels:** 10 Sentinel-2 bands: B02, B03, B04, B05, B06, B07, B08, B8A, B11, B12
- **Checkpoint SHA-256:** `7b8e1f5923bc0912ad8467e21a830df9310cba48392efb51d02c784918e9a112`
- **File Size:** 14.2 MB (`best_model.pt`)
- **License:** Apache 2.0

---

### 2. Empirical Benchmark Performance
- **Validation Dataset:** Copernicus DLT 2018 + Sentinel-2 European Montane/Temperate Forest Biomes
- **Overall Mean IoU:** **0.6907**
- **Broadleaved Forest IoU:** **0.7765**
- **Non-Tree Class IoU:** **0.7820**
- **Coniferous Forest IoU:** **0.5136**
- **Known Limitation:** Coniferous recall drops to $31.32\%$ at canopy edges ($\le 10\text{m}$) due to mixed pixels.
