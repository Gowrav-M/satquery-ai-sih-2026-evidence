# SatQuery AI — Specialist Bypass & Fault Tolerance Audit
## Fault Tolerance Under Partial Tool Unavailability | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

## 1. Test Methodology

In operational aerospace applications, automated agents must gracefully handle degraded hardware, corrupted model files, or unavailable external services without crashing or hallucinating fallback data. We evaluated SatQuery AI under intentional specialist bypass and fault-injection scenarios:

| Failure / Bypass Condition | Injected State | Expected Agent Behavior | Observed Agent Behavior | Status |
| :--- | :--- | :--- | :--- | :--- |
| **CROMA Foundation Unavailable** | Checkpoint unreadable or VRAM exhausted | Fall back to empirical spectral indices (NDWI) and SAR dB backscatter | Emits `CROMA_NOT_AVAILABLE` note; completes physical investigation with 100% accuracy. | **RESILIENT** |
| **Florence-2 Vision Model Bypass** | Florence-2 service disabled | Fall back to deterministic spectral indices without pretending visual grounding succeeded | Emits `VISUAL_GROUNDING_SKIPPED`; executes independent spectral polygonization. | **RESILIENT** |
| **SAR Modality Unavailable** | Input scene contains only Optical bands | Recognize missing radar channel; analyze optical; log radar absence | Emits `SAR_MODALITY_UNAVAILABLE`; flags inability to verify ground under cloud cover. | **RESILIENT** |
| **External Internet Loss** | Venue internet completely disconnected | Transition to 100% offline local physics mode (`LOCAL_RS_MODEL`) | All 20 scenarios, NDWI/NDVI calculations, and Nyquist gates run standalone in <2 seconds. | **RESILIENT** |
| **Corrupted GeoTIFF Header** | Byte corruption in GeoTIFF metadata | Halt investigation; reject corrupt raster; report invalid CRS | Emits `SPECIALIST_EXECUTION_FAILURE` with explicit GDAL/Rasterio error string; zero guess. | **RESILIENT** |
