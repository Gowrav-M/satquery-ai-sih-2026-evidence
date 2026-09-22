# SatQuery AI — Demonstration Recording Script & Timeline
## Practical Recording Guidelines for Team STARFORGE | SIH 2026 Problem Statement 26167
**Duration:** Exactly 6 Minutes (360 Seconds)  

---

### Step-by-Step Recording Blueprint

```text
[00:00 - 00:30] Introduction & Problem Setup
- Visual: Slide 1 & Slide 2 of the presentation or the GrandFinalConsole landing view.
- Narration: "Every day, ISRO constellations like Cartosat and RISAT collect massive multi-sensor Earth Observation imagery. But turning raw pixels into decisions takes hours of manual GIS scripting, optical imagery goes blind under monsoon clouds, and generic AI models hallucinate fake coordinates. We built SatQuery AI: an autonomous, evidence-driven Earth Investigation Agent."

[00:30 - 01:00] Architectural Overview
- Visual: Zoom in on the 4-tier architecture diagram.
- Narration: "SatQuery decouples neural perception from deterministic physics. Neural models propose; verified raster mathematics verify. Let's see it live on real Copernicus Sentinel data."

[01:00 - 02:00] Act 1: Single Image Water Grounding (Hero 01)
- Visual: Select '001_chilika_water' in the left catalog. Click 'Investigate'.
- Narration: "Here is Chilika Lagoon, Odisha. We ask: 'Identify the major open-water region and explain the physical evidence.' SatQuery plans the step, calculates NDWI, and delineates exactly 2,278.4 Hectares. Clicking on the lake reveals our live pixel probe with exact geodetic coordinates and physical land-cover classification."

[02:00 - 03:15] Act 2: All-Weather Optical + SAR Fusion (Hero 02)
- Visual: Select '015_optical_sar_fusion'. Toggle the split-curtain swipe slider.
- Narration: "Next, our all-weather test over the Bengaluru urban corridor. Optical imagery is affected by clouds and atmospheric haze. But our SensorAware SAR processor applies Lee speckle filtering and radiometric calibration to Sentinel-1 radar. Notice how the radar backscatter decibels drop below -18 dB, confirming calm surface water directly beneath the cloud cover."

[03:15 - 04:30] Act 3: Bi-Temporal Urban Expansion (Hero 03)
- Visual: Select '017_bitemporal_urban_change'. Inspect the differential change heatmap.
- Narration: "For multi-temporal analysis, we evaluate Bengaluru between May 12, 2026 and September 19, 2026. SatQuery first enforces a Fourier 2D co-registration barrier. Since displacement is only 0.21 pixels, change detection proceeds safely, isolating +36.4 Hectares of new impervious built-up expansion."

[04:30 - 05:00] Act 4: Scientific Abstention & Physical Nyquist Barrier
- Visual: Select '020_nyquist_safety'. Query: 'Is there a 3.5m car parked on the runway?'
- Narration: "Now an adversarial test. A user asks to detect a 3.5-meter vehicle in 10-meter Sentinel imagery. Unlike commercial LLMs that hallucinate, SatQuery's Observability Engine calculates the Nyquist-Shannon limit: 2x GSD = 20 meters. In under 200 milliseconds, it halts with PHYSICALLY_UNRESOLVABLE. It refuses to guess."

[05:00 - 05:40] Act 5: 8-Stage Cryptographic Evidence Graph
- Visual: Expand the 8-Stage DAG panel in the right sidebar. Click 'Download PDF Report'.
- Narration: "Every decision is recorded in an immutable 8-stage cryptographic Directed Acyclic Graph. Each node from raw query to final hectare measurement is signed with SHA-256, allowing ISRO mission directors to verify the audit trail or export complete peer-review dossiers."

[05:40 - 06:00] Act 6: Non-Technical User Accessibility & Closing
- Visual: Toggle the 'Farmer' persona button, then show Indic voice transcription.
- Narration: "SatQuery translates complex radiometry into plain language for farmers and district collectors in 10 Indian languages via Sarvam AI. Thank you from Team STARFORGE."
```
