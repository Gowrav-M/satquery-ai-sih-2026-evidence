# SatQuery AI — Technical Architecture & Evaluation FAQ

**Purpose:** Detailed architectural and engineering answers to core technical evaluation questions for ISRO / SAC and SIH evaluators.  
**Basis:** Verified empirical evidence and documentation in `SatQuery-AI-SIH-2026-Evidence/`.

---

### Q1. What did the team actually build?
We built **SatQuery AI**, a web-based Earth Observation analysis platform that enables natural-language querying of multi-spectral optical (Sentinel-2) and radar (Sentinel-1) satellite imagery. The system pairs an LLM-based reasoning core with deterministic GIS and remote-sensing processing engines. It translates user questions into structured investigation plans, checks whether the input rasters satisfy the query's spatial and spectral prerequisites (Observation Contract), computes calibrated physical indices from pixels, and returns vector polygons, geodesic hectare measurements, and a cryptographic execution trace.

---

### Q2. What part is genuinely agentic?
The agentic core is the **Orchestration Brain** (`RealEOInvestigationOrchestrator` / `QueryInterpreter`). It does not answer questions directly from memory; instead, it:
1. Parses natural-language queries into an abstract syntax tree (intent, target entity, temporal range, geographic constraint).
2. Formulates competing hypotheses ($H_0$: null hypothesis, $H_1$: detection target).
3. Validates the **Query-Observation Contract** (checking spatial CRS, resolution, bounds, and band availability).
4. Dynamically selects and dispatches domain specialist engines (NDWI specialist, SAR processor, bi-temporal differencing, or segmentation).
5. Halts or routes to abstention if observation requirements are physically unsatisfied.

---

### Q3. What part is actually adapted to remote sensing?
1. **Foundation Model Embeddings:** CROMA-Base (194.3M parameters) adapted for cross-attention alignment between 12-channel Sentinel-2 optical and 2-channel Sentinel-1 radar.
2. **Text-Guided Grounding:** Florence-2 fine-tuned with LoRA on remote sensing datasets (BigEarthNet + RS Grounding) to propose geographic bounding boxes from satellite queries.
3. **Multi-Spectral Segmentation:** SegFormer-B0 adapted from 3-channel RGB to 10-channel multi-spectral Sentinel-2 bands for European DLT canopy segmentation.
4. **Bi-Temporal QA:** Siamese dual-branch network adapted for bi-temporal change detection QA on satellite image pairs.

---

### Q4. Which components perform physical measurements?
Physical measurements are **never** estimated by language models or neural token generators. They are executed by deterministic GIS routines:
- **Spectral Radiometry:** Standard algebraic band ratios (NDWI = `(B03-B08)/(B03+B08)`, NDVI = `(B08-B04)/(B08+B04)`, NDBI = `(B11-B08)/(B11+B08)`).
- **SAR Calibration:** Radiometric calibration of Sentinel-1 Level-1 GRD intensity to decibels ($\sigma^0\text{ dB} = 10 \cdot \log_{10}(\text{DN}^2) - 83.0\text{ dB}$) with a $5 \times 5$ Lee adaptive speckle filter.
- **Surface Area:** Geodesic area in hectares and acres computed from polygonized raster pixel counts multiplied by affine transform pixel resolution and projected UTM coordinate systems.

---

### Q5. How does the system handle optical + SAR?
When both optical and SAR rasters are available, the system ingests co-registered pairs and executes a **Five-Point Physical Arbitration Matrix**:
- In clear skies, optical NDWI ($\ge 0.15$) and SAR specular attenuation ($\sigma^0 < -18.0\text{ dB}$) corroborate each other.
- Under heavy cloud, haze, or smoke, optical signals are severely attenuated. Because C-band microwave radiation ($\lambda \approx 5.6\text{ cm}$) penetrates atmospheric moisture, the **Scientific Gatekeeper** grants microwave backscatter primacy, confirming standing water or flood inundation through clouds.
- In urban areas, corner-reflector double-bounce returns ($\sigma^0 > +5.0\text{ dB}$) corroborate built-up infrastructure even in deep optical shadows.

---

### Q6. How does it handle two dates?
For bi-temporal analysis (e.g. urban expansion or crop transitions between Epoch $T_1$ and Epoch $T_2$):
1. **Co-Registration Verification:** Sub-pixel alignment is evaluated using 2D Fourier phase cross-power spectrum correlation. If displacement offset exceeds $6.0\text{ pixels}$, change detection is suppressed to prevent false boundary disparity artifacts.
2. **Spectral Differencing:** The system computes differential spectral rasters ($\Delta\text{NDBI}$ for built-up, $\Delta\text{NDVI}$ for vegetation).
3. **Vector Change Masking:** Positive change clusters are polygonized, area in hectares is calculated, and vector change boundaries are overlaid on the interactive map.

---

### Q7. What prevents unsupported answers?
Three deterministic barriers prevent hallucination:
1. **Nyquist Epistemic Guardrail:** By the Nyquist-Shannon sampling theorem, reliable detection requires an object dimension $\ge 2 \times \text{GSD}$ ($20\text{ m}$ for Sentinel-2 $10\text{ m}$ bands). Any query requesting targets smaller than $20\text{ m}$ (e.g., cars, individual trees) is immediately halted with status `PHYSICALLY_UNRESOLVABLE`.
2. **Immediate Null Policy:** Due to known VLM miscalibration on satellite data ($ECE = 25.26\%$), confidence scores are explicitly returned as `null` ("Uncalibrated") rather than outputting misleading probability numbers.
3. **8-Stage Cryptographic DAG:** All analysis stages generate immutable SHA-256 node hashes linking raw pixel inputs to output polygons, ensuring end-to-end auditability.

---

### Q8. What was actually benchmarked?
Three public benchmark evaluations were executed and verified against on-disk artifacts:
1. **RSVQA-LR:** 500 held-out Sentinel-2 items evaluated on single-image VQA (**29.40%** overall top-1 accuracy; Presence: **53.71%**, Comparison: **44.83%**, Count: **4.72%**, Attribute: **0.00%**).
2. **CDVQA:** 200 bi-temporal Sentinel-2 image pairs evaluated on change QA (**59.00%** hybrid accuracy vs **38.50%** deterministic baseline).
3. **Copernicus DLT 2018:** 3,000 tiles evaluated on 10-band multi-spectral canopy segmentation (**0.6907 mIoU**; Broadleaved: **0.7765**, Non-Tree: **0.7820**, Coniferous: **0.5136**).

---

### Q9. What was NOT evaluated?
- **VRSBench:** Marked **NOT EVALUATED** (no official public run completed).
- **ISRO Private Archives:** Marked **PRIVATE / NOT PROVEN** (no performance claims made on unreleased Cartosat/RISAT datasets).
- **Bathymetry & Water Depth:** Marked **UNSUPPORTED / REFUSED** (the system measures surface area but explicitly refuses depth/volume estimation).

---

### Q10. What remains private?
To protect intellectual property, private weights, and security boundaries:
- **Private Source Code:** Python backend orchestration, agent prompt templates, and TypeScript frontend components.
- **Model Checkpoints:** Binary neural weights (`.pt`, `.bin`, `.safetensors`) are maintained privately; their authenticity is verifiable via public SHA-256 checksums in `models/checkpoint_hashes.txt`.
- **Credentials & API Keys:** All environment secrets and tokens are excluded.
- **Raw Large Rasters:** Heavy GeoTIFF mosaics are archived privately; 20 representative demonstration GeoTIFFs are cataloged with open Copernicus URLs.

---

### Q11. Can the judges understand the evidence without seeing source code?
**Yes.** The public evidence package contains:
- 5 comprehensive architecture diagrams illustrating end-to-end data flow, specialist dispatch, and arbitration logic.
- 8 high-resolution forensic screenshots showing exact console outputs, pixel probe values, and vector polygons.
- Raw benchmark output JSON files (`RSVQA_summary.json`, `CDVQA_summary.json`) that can be inspected directly.
- A 20-scene data catalog (`scenario_manifest.csv`) with verifiable ESA Copernicus scene identifiers and SHA-256 hashes.
- Sanitized OpenAPI 3.1 schema documenting all 41 API endpoints.
- Detailed operational hero scenarios documented directly with input rasters, queries, and vector change boundaries.

---

### Q12. What differentiates this from a generic VLM wrapped around an image?
| Feature | Generic VLM Wrapper | SatQuery AI |
| :--- | :--- | :--- |
| **Area & Quantity Calculation** | Guesses numbers via language tokens (prone to hallucination) | Computes geodesic hectares from calibrated pixel counts via affine transforms |
| **All-Weather Capability** | Blind under clouds/monsoons (optical only) | Cross-modal optical + C-band SAR fusion with physical wave penetration primacy |
| **Sub-Resolution Safety** | Hallucinates small objects (e.g. cars in 10m pixels) | Rejects queries below Nyquist barrier ($2 \times \text{GSD} = 20\text{m}$) with `PHYSICALLY_UNRESOLVABLE` |
| **Auditability** | Black-box single-turn text answer | 8-stage cryptographic DAG with SHA-256 node signatures linking pixels to polygons |
| **Temporal Change** | Hallucinates changes from misaligned images | Suppresses change detection if 2D Fourier phase displacement $> 6.0\text{ px}$ |
| **Confidence Integrity** | Emits overconfident, miscalibrated percentages | Enforces Immediate Null Policy (`confidence = null`) for uncalibrated VLM outputs |
