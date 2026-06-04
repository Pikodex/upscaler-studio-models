# Upscaler Studio — Models

Asset repository for the pre-converted super-resolution models that the
[Upscaler Studio](https://github.com/Pikodex/upscaler-studio) app downloads on
demand.

This repository contains **no code** — only GitHub Releases holding the model
bundles (ONNX / NCNN weights and their helper files). The app fetches the
relevant release at install time, extracts it into the user's local data
directory, and runs it through an isolated per-backend environment. Nothing
here needs to be cloned manually.

> Each release body documents the exact upstream source, checkpoint and paper
> for that model. The table below is a summary index.

## Releases

### CNN / lightweight

| Tag | Model | Scales | License | Commercial |
|---|---|---|---|---|
| `compact-models-v1` | Real-ESRGAN Compact (SRVGGNetCompact) | 4× | BSD-3-Clause | ✅ |
| `realesrgan-extra-ncnn-v1` | Extra Real-ESRGAN RRDBNet variants (NCNN/Vulkan) | 2×/4× | BSD-3-Clause | ✅ |
| `span-models-v1` | SPAN — Swift Parameter-free Attention Network | 2×/4× | Apache-2.0 | ✅ |

### Transformer

| Tag | Model | Variants | License | Commercial |
|---|---|---|---|---|
| `hat-models-v1` | HAT — Hybrid Attention Transformer (CVPR 2023) | 14 (HAT-S/HAT/HAT-L/ImageNet × 2×/3×/4× + Real-HAT-GAN) | Apache-2.0 | ✅ |
| `dat-models-v1` | DAT — Dual Aggregation Transformer (ICCV 2023) | DAT / DAT-2 / DAT-S / DAT-light × scales | Apache-2.0 | ✅ |

### Diffusion-based restoration

| Tag | Model | Notes | License | Commercial |
|---|---|---|---|---|
| `diffbir-onnx-v1` | DiffBIR v2.1 (ECCV 2024) | Two-stage blind restoration (SwinIR + IRControlNet + SD 2.1) | Apache-2.0 | ⚠️ RAIL |
| `ccsr-onnx-v1` | CCSR v2.0 | Content-consistent SR, patched ControlNet | Apache-2.0 | ⚠️ RAIL |
| `ccsr-v1-onnx-v1` | CCSR v1.0 (CVPR 2024) | Stochastic SpacedSampler, monolithic LDM | Apache-2.0 | ⚠️ RAIL |
| `hypir-onnx-v1` | HYPIR | Single-step diffusion restorer (LoRA on SD 2.1) | **CC BY-NC 4.0** | ❌ **non-commercial** |
| `fidesr-onnx-v1` | FiDeSR (CVPR 2026) | One-step diffusion + latent residual refinement | Apache-2.0 | ⚠️ RAIL |
| `vosr-onnx-v1` | VOSR-0.5B (CVPR 2026) | Vision-only Flow-Matching SR (SD 2.1 VAE) | Apache-2.0 | ⚠️ RAIL* |
| `vosr-1.4b-onnx-v1` | VOSR-1.4B (CVPR 2026) | Large variant, Qwen-Image VAE (chunked assets) | Apache-2.0 | ✅* |

\* VOSR-0.5B uses the Stable Diffusion 2.1 VAE (RAIL pass-through applies).
VOSR-1.4B uses the Qwen-Image VAE + DINOv2 and is fully permissive.

## How the bundles are produced

The ONNX/NCNN bundles are exported from the official upstream checkpoints using
the conversion scripts in the app repository under
[`tools/`](https://github.com/Pikodex/upscaler-studio/tree/main/tools)
(e.g. `convert_hat_to_onnx.py`, `convert_diffbir_to_onnx.py`,
`convert_vosr_to_onnx.py`). Each `tools/README_*_CONVERSION.md` documents the
exact procedure. The precise upstream source for every release is listed in
that release's description.

> **Note on chunked assets:** Bundles larger than GitHub's 2 GB per-asset limit
> (currently `vosr-1.4b-onnx-v1`) are split into ~200 MB chunks. The app
> reassembles them automatically on install.

## License

The bundled weights inherit the license of their respective upstream models —
see the **License** column above and each release's description. The full
attribution table and commercial-use status is maintained in the app repo at
[`THIRD_PARTY_LICENSES.md`](https://github.com/Pikodex/upscaler-studio/blob/main/THIRD_PARTY_LICENSES.md).

Key points:

- **HYPIR (`hypir-onnx-v1`) is licensed CC BY-NC 4.0 — non-commercial use only.**
- The **RAIL pass-through** backends (DiffBIR, CCSR v1/v2, FiDeSR, VOSR-0.5B)
  derive from Stable Diffusion 2.1 (CreativeML Open RAIL++-M); the use-based
  restrictions apply.

_This document is informational and not legal advice._
