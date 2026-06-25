# 🎨 ComfyUI Workflow Recipes — RTX 4060 8GB

> 7 proven ComfyUI workflows optimised for RTX 4060 8GB VRAM. Production-ready, drag-and-drop.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![ComfyUI](https://img.shields.io/badge/ComfyUI-Latest-blue)](https://github.com/comfyanonymous/ComfyUI)
[![VRAM](https://img.shields.io/badge/VRAM-8GB-orange)]()

## 🚀 Quick Start

1. Install [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
2. Install required custom nodes (see [NODES.md](NODES.md))
3. Download the `.json` workflow files from `workflows/`
4. Drag into ComfyUI browser window — done.

## 📋 Workflows Included

| # | Workflow | VRAM | Use Case |
|---|---|---|---|
| 1 | **Flux Schnell** | 6.5 GB | Instant HQ image (4 steps) |
| 2 | **SDXL Turbo** | 4.5 GB | Real-time image gen |
| 3 | **SDXL + AnimateDiff** | 7.0 GB | 16-frame short video |
| 4 | **SDXL + ControlNet + LoRA** | 6.0 GB | Controlled img2img |
| 5 | **IP-Adapter Style Transfer** | 6.5 GB | Reference image style |
| 6 | **Stock Video + Background Removal** | 5.0 GB | Compositing |
| 7 | **Frame Interpolation** | 4.0 GB | Smooth slow motion |

## ⚡ Performance Tips

- Use `--force-fp16` for extra VRAM headroom
- Use `--lowvram` when combining ControlNet + AnimateDiff
- Keep AnimateDiff frames ≤ 16 on 8GB
- Use 512×768 for video (not 1024×1024)
- Always `batch_size=1` in KSampler

## 📦 Dependencies

See [NODES.md](NODES.md) for the full list of required custom nodes and models.

## 🤝 Services

Need a custom workflow? [AusAI Tech](https://ausai.tech) builds production ComfyUI pipelines — from A$200.

## 📄 License

MIT — use freely, attribution appreciated.
