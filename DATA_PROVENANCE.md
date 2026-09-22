# SatQuery AI — Earth Observation Data Provenance & Corpus Manifest
## Scientific Integrity Record | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

## 1. Data Provenance & Zero-Synthetic-Pixel Guarantee

SatQuery AI is built and evaluated exclusively on **authentic, calibrated Earth Observation satellite rasters**:
- **Optical Sensors:** Copernicus Sentinel-2A / Sentinel-2B / Sentinel-2C Multi-Spectral Instrument (MSI), processed to Level-2A Bottom-of-Atmosphere (BOA) surface reflectance.
- **SAR Sensors:** Copernicus Sentinel-1A C-Band Synthetic Aperture Radar (SAR), processed to Level-1 Ground Range Detected (GRD) with terrain-corrected backscatter.
- **Data Source Provider:** European Space Agency (ESA) Copernicus Data Space Ecosystem via AWS Open Data Cloud-Optimized GeoTIFF (COG) archives.
- **License Terms:** Open Access for Earth Observation Data under Creative Commons Attribution-ShareAlike 3.0 IGO ([CC-BY-SA 3.0 IGO](https://creativecommons.org/licenses/by-sa/3.0/igo/)).

> [!IMPORTANT]
> **Zero Synthetic Pixels in Demonstration Scenarios:**  
> All 20 canonical scenes in the demonstration corpus consist of authentic, real-world satellite acquisitions. No synthetic textures, simulated pixels, or fabricated geometries exist in the operational mission catalog.

---

## 2. Geographic & Thematic Diversity Across India

The 20-scenario demonstration corpus captures the full spectrum of Indian agro-ecological, hydrological, and urban landscapes:

| Scenario ID | Name & Location | Modality & Sensor | Key Physical Capability |
| :--- | :--- | :--- | :--- |
| **`001_chilika_water`** | Chilika Lagoon, Odisha (`EPSG:32645`) | Optical (Sentinel-2C L2A) | Open-water delineation, NDWI thresholding, hectare polygonization |
| **`002_bengaluru_urban`** | Bengaluru, Karnataka (`EPSG:32643`) | Optical (Sentinel-2B L2A) | Urban land cover, impervious surface NDBI analysis |
| **`003_punjab_agriculture`** | Ludhiana, Punjab (`EPSG:32643`) | Optical (Sentinel-2B L2A) | Precision crop health, NDVI photosynthetic vitality mapping |
| **`004_sundarbans_mangrove`** | Sundarbans Delta, West Bengal (`EPSG:32645`) | Optical (Sentinel-2B L2A) | Wetland mangrove ecosystem health and tidal channels |
| **`005_rajasthan_dryland`** | Thar Desert, Rajasthan (`EPSG:32643`) | Optical (Sentinel-2B L2A) | Arid terrain land classification, bare soil spectral signatures |
| **`006_rann_of_kutch`** | Rann of Kutch, Gujarat (`EPSG:32642`) | Optical (Sentinel-2B L2A) | Salt crust, evaporite pan and seasonal mudflat delineation |
| **`007_kerala_flood`** | Kuttanad Wetlands, Kerala (`EPSG:32643`) | Optical (Sentinel-2B L2A) | Flood inundation vulnerability, saturated soil detection |
| **`008_mumbai_coastal`** | Mumbai Coast, Maharashtra (`EPSG:32642`) | Optical (Sentinel-2B L2A) | Coastal megacity urban infrastructure and creek boundary |
| **`009_chennai_urban_water`** | Chennai, Tamil Nadu (`EPSG:32644`) | Optical (Sentinel-2B L2A) | Urban water reservoirs, lake restoration tracking |
| **`010_brahmaputra_river`** | Brahmaputra Basin, Assam (`EPSG:32646`) | Optical (Sentinel-2B L2A) | Braided river morphology, sandbar and channel shifts |
| **`011_himalayas_snow`** | Himachal Himalayas (`EPSG:32643`) | Optical (Sentinel-2B L2A) | Cryosphere snow cover, glaciated valley delineation |
| **`012_goa_coast`** | Mandovi Estuary, Goa (`EPSG:32643`) | Optical (Sentinel-2B L2A) | Estuarine sediment dynamics, coastal forest vegetation |
| **`013_sentinel1_sar_water`** | Chilika Lagoon Shoreline (`EPSG:32645`) | SAR (Sentinel-1A GRD) | Microwave specular water attenuation ($< -18\text{ dB}$) |
| **`014_sentinel1_sar_urban`** | Bengaluru Urban Core (`EPSG:32643`) | SAR (Sentinel-1A GRD) | Corner-reflector double-bounce ($> +5\text{ dB}$) |
| **`015_optical_sar_fusion`** | Bengaluru Urban (`EPSG:32643`) | Optical + SAR Pair | All-weather cross-modal cloud penetration & verification |
| **`016_optical_sar_water`** | Chilika Co-Registered (`EPSG:32645`) | Optical + SAR Pair | Multi-sensor water body corroboration |
| **`017_bitemporal_urban_change`** | Bengaluru (May 12, 2026 vs Sep 19, 2026) (`EPSG:32643`) | Bi-Temporal Optical Pair | Co-registered urban settlement expansion (+36.4 ha) |
| **`018_bitemporal_veg_change`** | Punjab (Pre vs Post Harvest) (`EPSG:32643`) | Bi-Temporal Optical Pair | Agricultural crop harvesting transition ($\Delta\text{NDVI}$) |
| **`019_scientific_abstention`** | Spectral Mismatch Scene (`EPSG:32645`) | Optical (Sentinel-2) | Sensor incompatibility abstention (Thermal/Bathymetry) |
| **`020_nyquist_safety`** | Runway Sub-Pixel Target (`EPSG:32643`) | Optical (Sentinel-2) | Nyquist spatial barrier ($3.5\text{m} < 20.0\text{m}$) abstention |

---

## 3. Cryptographic Verification Manifest

The complete machine-readable manifest including geographic coordinates, bounding boxes, GSD, CRS, and cryptographic SHA-256 hashes is published at:  
[`provenance/scenario_manifest.csv`](provenance/scenario_manifest.csv)
