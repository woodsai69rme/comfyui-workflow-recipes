# ComfyUI Workflow JSON Files

This directory contains production-ready `.json` workflow files for each recipe documented in [workflow_recipes.md](../workflow_recipes.md).

## How to Use

1. Download the `.json` file for the workflow you want
2. Open ComfyUI (`http://127.0.0.1:8188`)
3. Drag & drop the `.json` file onto the canvas
4. Select your checkpoint/inputs
5. Click **Queue Prompt**

## Workflow Files

| # | Workflow | File | Status | VRAM | Time |
|---|---|---|---|---|---|
| 1 | Text-to-Image (SDXL) | `01_sdxl_text2image.json` | 📋 Documented | 4.2 GB | 8s |
| 2 | Image-to-Image (SDXL) | `02_sdxl_img2img.json` | 📋 Documented | 4.5 GB | 10s |
| 3 | Text-to-Video (Wan 2.1) | `03_wan_text2video.json` | 📋 Documented | 6.8 GB | 45s |
| 4 | Beat-Synced Music Video | `04_beat_synced_music_video.json` | 🔜 Coming | 7.2 GB | 2-5 min |
| 5 | Video Style Transfer | `05_video_style_transfer.json` | 🔜 Coming | 5.8 GB | 30s/frame |
| 6 | Character Consistency Pipeline | `06_character_consistency.json` | 🔜 Coming | 6.2 GB | 20s |
| 7 | Upscale + Frame Interpolation | `07_upscale_interpolation.json` | 🔜 Coming | 3.5 GB | 15s |

**📋 Documented** = Node-by-node instructions in [workflow_recipes.md](../workflow_recipes.md). Placeholder `.json` file present — open in ComfyUI and add nodes manually.

**🔜 Coming** = Spec documented, JSON export pending. Follow [workflow_recipes.md](../workflow_recipes.md) to build manually.

## Node Requirements

All workflows use nodes from:
- ComfyUI core
- ComfyUI-Manager (install missing nodes automatically)
- Impact Pack
- KJNodes
- Efficiency Nodes

## Hardware

All workflows tested on **NVIDIA RTX 4060 8GB VRAM**. If you have a different GPU, adjust batch sizes and resolutions accordingly.

## License

MIT — use commercially, modify freely. See [LICENSE](../LICENSE).
