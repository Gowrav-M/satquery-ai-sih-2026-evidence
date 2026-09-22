# SatQuery AI — Sensor & Data Provenance Record
## Attribution & Open Access Compliance | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

## 1. Upstream Satellite Data Providers

All imagery utilized in the SatQuery AI public demonstration corpus originates from authorized open-access civilian Earth Observation programs:

### 1.1 Copernicus Sentinel-2 Multi-Spectral Instrument (MSI)
- **Operator:** European Space Agency (ESA) on behalf of the European Union.
- **Product Type:** Level-2A Bottom-of-Atmosphere (BOA) surface reflectance in cartographic UTM geometry.
- **Bands Harvested:**
  - B02 (Blue, 490 nm, 10m GSD)
  - B03 (Green, 560 nm, 10m GSD)
  - B04 (Red, 665 nm, 10m GSD)
  - B08 (Near-Infrared, 842 nm, 10m GSD)
  - B11 (Shortwave Infrared-1, 1610 nm, 20m GSD, resampled)
- **License:** Creative Commons Attribution-ShareAlike 3.0 IGO ([CC-BY-SA 3.0 IGO](https://creativecommons.org/licenses/by-sa/3.0/igo/)).

### 1.2 Copernicus Sentinel-1 Synthetic Aperture Radar (SAR)
- **Operator:** European Space Agency (ESA).
- **Product Type:** Level-1 Ground Range Detected (GRD) in Interferometric Wide (IW) swath mode.
- **Polarizations:** Dual-polarization VV (vertical transmit / vertical receive) and VH (vertical transmit / horizontal receive).
- **Radiometric Calibration:** Applied $\sigma^0\text{ dB} = 10 \cdot \log_{10}(\text{DN}^2) - 83.0$.

---

## 2. ISRO Cartosat-2S & RISAT-1A Architectural Compatibility

While public distribution is restricted to open Copernicus data, SatQuery AI's underlying ingestion pipeline is natively configured with sensor profiles for Indian national missions:
- **Cartosat-2S:** Panchromatic ($0.65\text{m}$ GSD) and Multispectral ($1.6\text{m}$ GSD) affine raster ingestion profiles (`backend/services/sensor_profiles.py`).
- **RISAT-1A (EOS-04):** C-Band circular and linear polarimetric radar calibration envelopes.

---

## 3. Cryptographic Scenario Integrity

The complete registry of all 20 scenes, including acquisition timestamps, geodetic coordinates, UTM CRS, and SHA-256 hashes, is cataloged in:  
[`provenance/scenario_manifest.csv`](scenario_manifest.csv)
