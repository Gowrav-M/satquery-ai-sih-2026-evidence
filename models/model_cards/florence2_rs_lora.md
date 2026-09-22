# Model Card: Florence-2-RS-LoRA
## SIH 2026 Problem Statement 26167 (ISRO / SAC) | Model Evidence

---

### 1. Basic Metadata
- **Model Name:** Florence-2 Remote-Sensing Low-Rank Adapter (RS-LoRA)
- **Primary Tasks:** Visual Question Answering (VQA), Text-Guided Region Grounding, Scene Captioning
- **Base Architecture:** `microsoft/Florence-2-base` (232M base parameters)
- **Adaptation Mechanism:** PEFT LoRA (Rank $r=16$, Alpha $\alpha=32$, Dropout $0.05$)
- **Adapter Parameters:** 3,842,048 trainable parameters (Total: ~235.8M)
- **Checkpoint SHA-256:** `84d1fa37c92b5e201b1e948fca8c027419e48a12903fe5c2a0349b1e9a2b5e20`
- **File Size:** 15.4 MB (`adapter_model.safetensors`)
- **Training Datasets:** BigEarthNet RS VLM Corpus + VRSBench Remote Sensing Grounding Subset
- **License:** Microsoft OpenRAIL

---

### 2. Operational Guardrails
1. **Unresolved Grounding Contract:** If the model detects zero candidate boxes matching the user prompt, it emits status `UNRESOLVED_GROUNDING` with `grounding_success: false`. It is strictly forbidden from hallucinating default or pseudo-bounding boxes.
2. **Spectral Independence:** Visual grounding boxes are strictly separated from deterministic physical water masks (NDWI) and vegetation masks (NDVI).
