# Technical Architecture — ALLENNLP

**Upstream:** [https://github.com/allenai/allennlp](https://github.com/allenai/allennlp)
**License:** Apache 2.0
**Category:** ACADEMIA_RD
**Anticloud Integration:** PAX L5 Narrow L2 General 27B + AIOSS + Offline-First

## Upstream Description

NLP research library for academic experiments

## Anticloud Architectural Changes

1. PAX L5 Narrow L2 General 27B local research assistant for literature review and synthesis
2. AIOSS cryptographic provenance chain for all datasets and results
3. AES-256 encryption for unpublished research data and pre-prints
4. Single-binary research tool deployment — no IT admin required
5. Offline citation and reference management replacing cloud services
6. Zero-telemetry: removes all upstream analytics
7. Reproducibility ledger: immutable record of software versions, seeds, hardware
8. GPU/CPU equalizer: runs on office laptop CPU or HPC GPU cluster identically

## Integration Points

- **PAX Inference Socket:** Local HTTP endpoint at `127.0.0.1:11434/v1/chat` — same OpenAI-compatible API, zero cloud
- **AIOSS Hook:** Every write operation calls `aioss_append(event, payload)` before commit
- **Encryption Layer:** All file I/O routed through `anticloud_crypto.encrypt_at_rest()`
- **Single Binary Build:** `pyinstaller anticloud_allennlp.spec` or `go build -o allennlp`

## Deployment Modes

| Mode | Hardware | Notes |
| --- | --- | --- |
| Edge CPU | Raspberry Pi 4 / Intel NUC | Full feature set, PAX on CPU |
| Desktop GPU | RTX 3060 / A10 | PAX GPU inference, <1s latency |
| Server | 2× A100 | Full batch throughput |
| Air-gapped | Any x86/ARM | Zero network dependency |