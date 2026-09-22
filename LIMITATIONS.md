# SatQuery AI — Scientific Assumptions & Known Limitations
## Honest Technical Disclosure | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

## 1. Principles of Scientific Transparency

A core tenet of ISRO engineering is the honest delineation of operational boundaries. SatQuery AI does not claim universal, omniscient intelligence. Rather, it explicitly defines its mathematical and physical boundaries:

---

## 2. Documented Operational Limitations

### 2.1 Conifer Forest Boundary Mixed Pixels
- **Observation:** In the SegFormer-B0 10-band European DLT baseline, coniferous forest recall drops from $59.74\%$ globally to **$31.32\%$ at canopy boundaries ($\le 10\text{m}$ from edge)**.
- **Physical Cause:** At 10m GSD, pixels on the periphery of narrow coniferous stands capture a spectral mixture of needleleaf foliage, understory grass, and bare soil, resulting in spectral confusion with broadleaved species.
- **System Behavior:** When reporting forest canopy classifications, SatQuery logs a boundary uncertainty metric in the evidence metadata.

### 2.2 Bathymetric Water Depth & Volume
- **Observation:** When asked *"What is the volume of water in Chilika Lake in cubic meters?"*, the system delineates surface area (**2,278.4 ha**) but explicitly **refuses to estimate total water volume**.
- **Physical Cause:** 2D optical surface reflectance (NDWI) and C-band microwave backscatter cannot penetrate water depth to resolve underwater bathymetric topography.
- **System Behavior:** Emits a limitation note: *"Surface water area is rigorously measured at 22.78 km²; water volume cannot be calculated without active sonar bathymetry or calibrated elevation soundings."*

### 2.3 Co-Registration Displacement Barrier
- **Observation:** Bi-temporal change detection requires a spatial alignment shift of $\le 6.0\text{ pixels}$.
- **Physical Cause:** When two acquisitions suffer from gross orthorectification disparity ($> 6.0\text{ px}$), standard 2D cross-correlation produces severe false-positive edge disparities along building perimeters and road margins.
- **System Behavior:** Suppresses change clustering and alerts the operator: *"Registration offset exceeds 6.0 px threshold. Re-orthorectification with ground control points (GCPs) required."*

### 2.4 High-Wind SAR Surface Roughening
- **Observation:** Under severe gale or storm conditions (wind speed $> 15\text{ m/s}$), calm water surfaces develop capillary waves, causing C-band radar backscatter to rise above the $-18.0\text{ dB}$ specular attenuation threshold.
- **System Behavior:** The system cross-references optical NDWI against SAR backscatter; if optical confirms open water while SAR indicates rough surface backscatter, a *Wind Roughening / Maritime Disparity* caveat is logged.

### 2.5 Local Compute & VRAM Requirements
- **Observation:** Running fine-tuned `Florence-2-RS-LoRA` locally in float16 requires $\ge 6.0\text{ GB}$ of dedicated GPU VRAM.
- **System Behavior:** If executing on a resource-constrained edge terminal ($< 6\text{ GB}$ VRAM), SatQuery gracefully falls back to:
  1. Multi-tier cloud provider failover (AgentRouter / Gemini).
  2. Pure local deterministic physics mode (`[LOCAL_RS_MODEL]`), which executes complete GIS calculations and polygonization using $< 500\text{ MB}$ RAM on standard CPUs.

### 2.6 VQA Confidence Calibration & Immediate Null Policy
- **Observation:** Vision-language models exhibit significant miscalibration on out-of-distribution satellite queries (empirical RSVQA-LR Expected Calibration Error: $ECE = 25.26\%$, Maximum Calibration Error: $MCE = 41.20\%$).
- **System Behavior:** Rather than presenting fabricated or misleading probability scores, SatQuery strictly enforces the **Immediate Null Policy**: production VQA responses return `confidence = null` and display *"Uncalibrated"* in the user interface. Post-hoc Platt scaling and temperature calibration remain active research areas.

### 2.7 Numerical Counting on Satellite Rasters
- **Observation:** In public benchmark evaluation on RSVQA-LR, open-ended numerical counting queries achieve only **$4.72\%$ accuracy** (10/212 items correct), while presence detection achieves **$53.71\%$**.
- **Physical Cause:** Pretraining on binary classification (presence vs absence) does not provide fine-grained multi-object counting representations across dense satellite imagery.
- **System Behavior:** Numerical counting queries trigger explicit guidance recommending the user rely on deterministic vector polygonization (e.g. water bodies, agricultural fields) rather than relying on raw VLM token counts.

