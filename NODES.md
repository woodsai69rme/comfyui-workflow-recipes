# Required Custom Nodes & Models

## Custom Nodes

Install via ComfyUI Manager or git clone into `ComfyUI/custom_nodes/`:

| Node | GitHub | Purpose |
|---|---|---|
| **AnimateDiff Evolved** | `Kosinkadink/ComfyUI-AnimateDiff-Evolved` | Video generation |
| **VideoHelperSuite** | `Kosinkadink/ComfyUI-VideoHelperSuite` | Video loading/saving |
| **IPAdapter Plus** | `cubiq/ComfyUI_IPAdapter_plus` | Style transfer |
| **ControlNet Aux** | `Fannovel16/comfyui_controlnet_aux` | Depth/canny/pose |
| **ComfyUI-RMBG** | `1038lab/ComfyUI-RMBG` | Background removal |
| **Frame Interpolation** | `Fannovel16/ComfyUI-Frame-Interpolation` | Smooth slow-motion |
| **GGUF Loader** | `city96/ComfyUI-GGUF` | Flux Q4/Q5 loading |

## Models

| Model | Size | Download From |
|---|---|---|
| `juggernautXL_v9.safetensors` | 6.5 GB | [CivitAI](https://civitai.com/models/133005/juggernaut-xl) |
| `sdxl_vae.safetensors` | 335 MB | [HuggingFace](https://huggingface.co/madebyollin/sdxl-vae-fp16-fix) |
| `flux1-schnell-Q5.gguf` | 5.2 GB | [HuggingFace](https://huggingface.co/city96/FLUX.1-schnell-gguf) |
| `mm_sdxl_v10_beta.ckpt` | 1.7 GB | [HuggingFace](https://huggingface.co/guoyww/animatediff) |
| `t5xxl_fp16.safetensors` | 9.2 GB | [HuggingFace](https://huggingface.co/comfyanonymous/flux_text_encoders) |
| `clip_l.safetensors` | 246 MB | [HuggingFace](https://huggingface.co/comfyanonymous/flux_text_encoders) |
| `IP-Adapter SDXL` | 1.2 GB | [HuggingFace](https://huggingface.co/h94/IP-Adapter) |

Place models in:
- Checkpoints: `ComfyUI/models/checkpoints/`
- VAE: `ComfyUI/models/vae/`
- ControlNet: `ComfyUI/models/controlnet/`
- AnimateDiff: `ComfyUI/models/animatediff_models/`
- GGUF: `ComfyUI/models/unet/`
- IP-Adapter: `ComfyUI/models/ipadapter/`
- CLIP: `ComfyUI/models/clip/`
