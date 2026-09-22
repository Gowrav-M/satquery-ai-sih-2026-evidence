# SatQuery AI — Technical Evidence & Verification Guide
## Evaluator Verification Guide | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

> [!IMPORTANT]
> **Repository Purpose & Scope Notice:**  
> This repository contains selected technical documentation, validation results, architecture diagrams, model information, data provenance and demonstration evidence for SatQuery AI. The production source code, private checkpoints, credentials and restricted evaluation data are intentionally not included.

---

## 1. Overview of Verification Architecture

To allow technical reviewers and SIH evaluators to verify our engineering claims without redistributing proprietary software or restricted satellite rasters, SatQuery AI provides an **Open Technical Evidence Trail**:
1. **Cryptographic Checksum Verification:** Validate the SHA-256 digests of all 20 real Earth Observation scenes and trained model checkpoints against our immutable lockfiles.
2. **Sanitized OpenAPI Specification:** Audit the exact request/response schemas, parameter validations, and data models powering the backend.
3. **Forensic Evidence Dossiers:** High-resolution screenshots and machine-readable JSON logs for every canonical scenario.
4. **Authorized Private Inspection:** Evaluators requesting a live clean-room code audit or private demonstration can schedule a walkthrough with the team.

---

## 2. Cryptographic Checksum Audit

Evaluators can verify that the demonstration corpus and model checkpoints are authentic and unmodified by checking their SHA-256 signatures:

```bash
# Verify Scenario Manifest
# Target File: provenance/scenario_manifest.csv
# Expected SHA-256 matches the entries published in the manifest.

# Example Verification on Unix / macOS:
shasum -a 256 provenance/scenario_manifest.csv

# Example Verification on Windows PowerShell:
Get-FileHash -Algorithm SHA256 provenance\scenario_manifest.csv
```

### Authoritative Model Hashes:
Refer to [`models/checkpoint_hashes.txt`](models/checkpoint_hashes.txt) for the complete list of verified model weights.

---

## 3. Public vs Private Artifact Governance

| Evidence Artifact | Public Evidence Repository (`SatQuery-AI-SIH-2026-Evidence`) | Private Engineering Repository (Internal Team STARFORGE) |
| :--- | :--- | :--- |
| **System Architecture** | Full diagrams, 4-tier dataflows, OpenAPI schema | Full implementation code (`backend/`, `frontend/`) |
| **Scientific Formulas** | Exact mathematical equations for NDWI, Lee filter, dB, Nyquist | Python/C++ implementations using `rasterio` & `numpy` |
| **Demonstration Scenes** | Complete 20-scene manifest with GSD, CRS, dates, SHA-256 | Raw Multi-Gigabyte GeoTIFF rasters and cache tiles |
| **Model Weights** | Architectural specifications, parameter counts, SHA-256 digests | Actual binary checkpoints (`.pt`, `.bin`, `.safetensors`) |
| **Benchmark Metrics** | Audited performance tables on CDVQA, RSVQA, DLT | Training scripts, hyperparameter logs, checkpoint bake-offs |
| **Credentials & Secrets** | Excluded; zero tokens, zero local paths | Protected `.env` files and deployment configurations |

---

## 4. Evaluator Inspection Request Protocol

If the SIH evaluation committee or ISRO technical jury requires an authorized live execution walkthrough or inspects the private codebase:
1. Contact the Team STARFORGE technical lead during the Grand Finale evaluation session.
2. The team will execute a live clean-room demonstration from the Private Engineering Repository on official evaluation hardware.
3. All intermediate outputs, terminal logs, and physical GIS measurements can be replayed in real time.
