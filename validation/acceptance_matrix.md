# SatQuery AI — Functional Acceptance Matrix
## Comprehensive System Verification | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

| Functional Acceptance Requirement | Verification Protocol | Observed System Behavior | Acceptance Status |
| :--- | :--- | :--- | :--- |
| **AC-01: Single-Image Optical Water Delineation** | Ingest Sentinel-2 L2A raster over Chilika Lake (`001_chilika_water`). Query for open water. | NDWI computed at $>0.15$; GeoJSON polygon extracted; 2,278.4 ha reported with zero rounding. | **ACCEPTED** |
| **AC-02: All-Weather SAR Cloud Penetration** | Ingest co-registered Sentinel-2 (cloudy) + Sentinel-1 SAR (`015_optical_sar_fusion`). | SAR Lee filter applied; radar decibels calibrated ($<-18\text{ dB}$); water corroborated through clouds. | **ACCEPTED** |
| **AC-03: Bi-Temporal Co-Registration Barrier** | Ingest T1 vs T2 pair with intentional 10 px shift. | Fourier 2D cross-correlation detects shift $>6.0\text{ px}$; suppresses change detection; logs barrier. | **ACCEPTED** |
| **AC-04: Bi-Temporal Urban Change Quantification** | Ingest co-registered Bengaluru acquisitions (May 12, 2026 vs September 19, 2026, offset $<6.0\text{ px}$). | Differential NDBI clustering isolates +36.4 ha of new urban construction with boundary overlay. | **ACCEPTED** |
| **AC-05: Sub-Resolution Nyquist Epistemic Abstention** | Ingest 10m GSD imagery. Request detection of a 3.5m vehicle. | Nyquist filter detects $3.5\text{m} < 20.0\text{m}$; halts with `PHYSICALLY_UNRESOLVABLE`; refuses to guess. | **ACCEPTED** |
| **AC-06: 8-Stage Cryptographic DAG Integrity** | Complete an investigation; inspect hash linkages across all 8 nodes. | Every node (Query $\to$ Hypotheses $\to$ Asset $\to$ Measurement $\to$ Finding) signs state with SHA-256. | **ACCEPTED** |
| **AC-07: Non-Technical User Localization** | Switch persona between Farmer, District Collector, and Scientist. | Farmer mode outputs acres and advisory; Collector mode outputs hazard impact; Scientist mode outputs formulas. | **ACCEPTED** |
| **AC-08: Zero-Mock Quarantine Barrier** | Attempt to trigger synthetic mock dispatcher on real GeoTIFF rasters. | System raises `RuntimeError`; blocks synthetic mocks from contaminating real investigations. | **ACCEPTED** |
