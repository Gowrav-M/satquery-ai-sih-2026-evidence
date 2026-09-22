# SatQuery AI — System Validation & Regression Evidence
## Quality Assurance & Automated Testing Record | SIH 2026 Problem Statement 26167 (ISRO / SAC)
**Team:** STARFORGE  

---

## 1. Automated Regression Suite Overview

The SatQuery AI validation methodology follows a multi-tier testing pyramid:
1. **Deterministic Physics Tests:** Verifies pixel conversion, NDWI thresholds, and Lee filter accuracy against analytical mathematical solutions.
2. **Specialist Bypass Resilience Tests:** Verifies that when a specialist or provider is disabled or fails, the orchestrator handles the exception gracefully without crashing or emitting false findings.
3. **Corpus Forensic Tests:** Validates all 20 real Earth Observation scenes against affine bounds, GSD, and cryptographic SHA-256 lockfiles.
4. **End-to-End Real GeoTIFF Tests:** Executes authentic multi-band rasters through the full agentic loop.

---

## 2. Test Execution Summary

```
================================== TEST SUMMARY ==================================
  Total Critical Suite Tests:    33 items
  Passed Tests:                 30 PASSED (90.9% Pass Rate)
  Investigated Edge Cases:       3 Edge Cases Documented
  Execution Runtime:            144.4 seconds
  Mock / Synthetic Leakage:     0 (Zero-Mock Verified)
==================================================================================
```

### Critical Verified Test Cases:
- `test_real_optical_geotiff_investigation` $\to$ **PASSED** (Sentinel-2 multispectral NDWI calculation)
- `test_real_sar_geotiff_investigation` $\to$ **PASSED** (Sentinel-1 calibrated backscatter & dielectric attenuation)
- `test_real_optical_sar_croma_investigation` $\to$ **PASSED** (CROMA 194.3M cross-attention alignment)
- `test_real_bitemporal_pair_investigation` $\to$ **PASSED** (2D phase cross-correlation displacement & change clustering)
- `test_subresolution_nyquist_abstention` $\to$ **PASSED** (Physical Nyquist barrier: $3.5\text{m} < 20.0\text{m}$ rejection)
- `test_provenance_replay_and_downloadable_report` $\to$ **PASSED** (SHA-256 DAG and report generation)
- `test_zero_mock_leakage_measurements` $\to$ **PASSED** (Guarantees zero hardcoded dictionary lookups)
- `test_quarantine_barrier_raises_runtime_error_on_real_investigation` $\to$ **PASSED** (Legacy synthetic mocks quarantined)

---

## 3. Sub-Audit Documentation Links

- [`validation/acceptance_matrix.md`](validation/acceptance_matrix.md) — Complete acceptance matrix matching every functional contract.
- [`validation/specialist_bypass_results.md`](validation/specialist_bypass_results.md) — Defensive fault tolerance when individual tools are unavailable.
- [`validation/corpus_integrity.md`](validation/corpus_integrity.md) — 20-scene GeoTIFF integrity audit results (20/20 certified).
- [`validation/provider_truthfulness.md`](validation/provider_truthfulness.md) — Multi-tier LLM provider failover and latency telemetry.
- [`validation/regression_summary.md`](validation/regression_summary.md) — Detailed pytest logs and failure taxonomy analysis.
