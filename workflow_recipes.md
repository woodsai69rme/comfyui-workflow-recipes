# ComfyUI Workflow Recipes — RTX 4060 8GB

Build these in ComfyUI by adding nodes from the node menu (right-click → Add Node).
Drag-connect the outputs (right-side dot) to inputs (left-side dot) as described.

## 1. Flux Schnell — Instant HQ Image (4-step)
**VRAM: ~6.5 GB | Ideal for quick references**

```
Load Diffusion Model (GGUF)
  ├─ flux1-schnell-Q5.gguf (ONLY flux/schnull/text_encoders on load)
  └─ ClipLoader → flux1-schnell
       └─ DualCLIPLoader → CLIP-L + T5-XXL (fp8)

VAELoader → ae.safetensors (= VAE)

ClIP Text Encode (Prompt) → positive
CLIP Text Encode (Prompt) → negative

KSampler
  ├─ model ← Load Diffusion Model
  ├─ positive ← CLIP Text Encode
  ├─ negative ← CLIP Text Encode  
  ├─ VAE ← VAELoader (decoded)
  ├─ latent_image → Empty Latent Image (1024×1024)
  ├─ steps=4, cfg=1, sampler=uni_pc, scheduler=simple
  └─ Seed (random)

Save Image ← KSampler (output)
```

## 2. SDXL Turbo — Real-time-ish Image
**VRAM: ~4.5 GB | For fast tests**

```
Load Diffusion Model → juggernautXL_v9 or sd_xl_turbo_1.0
Load VAE → sdxl_vae.safetensors
CLIPTextEncodeSDXL → positive/negative

Empty Latent Image → 1024×1024

KSampler
  ├─ steps=2-4, cfg=1-2
  └─ sampler=dpmpp_2m, scheduler=karras
  
VAE Decode → Save Image
```

## 3. SDXL + AnimateDiff — Short Video
**VRAM: ~7.0 GB | 16 frames, 512×768**

```
Load Diffusion Model → juggernautXL_v9

Load VAE → sdxl_vae.safetensors  

CLIPTextEncodeSDXL → positive/negative

Empty Latent Image → 512×768

AnimateDiff Loader
  ├─ model_name: mm_sdxl_v10_beta.ckpt
  ├─ beta_schedule: sqrt_linear
  └─ context_options: 16 frames
  
AnimateDiff Sampler (custom node from AnimateDiff-Evolved)
  ├─ steps=25, cfg=7
  ├─ sampler=ddpm, scheduler=karras
  ├─ frames=16
  └─ seed=random

VAE Decode → Save Video (from VideoHelperSuite)
```

## 4. SDXL + ControlNet (Depth) + LoRA
**VRAM: ~6.0 GB | Image-to-image with control**

```
Load Diffusion Model → juggernautXL_v9
Load VAE → sdxl_vae.safetensors
CLIPTextEncodeSDXL → positive/negative

Load Image → image input

ControlNetLoader → diff_control_sd15_depth or kohya_depth
Apply ControlNet
  ├─ control_net ← ControlNetLoader
  ├─ image ← Load Image
  └─ strength=0.8

Load LoRA → Hyper-SDXL-8steps-lora.safetensors (strength=0.6)

Empty Latent Image → 1024×1024

KSampler
  ├─ steps=8, cfg=3, sampler=uni_pc
  └─ scheduler=normal

VAE Decode → Save Image
```

## 5. Hybrid — Reference Style via IP-Adapter
**VRAM: ~6.5 GB | Style from reference image**

```
Load Diffusion Model → juggernautXL_v9
Load VAE → sdxl_vae.safetensors

CLIPTextEncodeSDXL → positive/negative

IPAdapter Unified Loader (from IPAdapter_plus)
  ├─ ip_adapter → IP-Adapter SDXL model
  ├─ clip_vision → CLIP-ViT-H or ViT-bigG
  └─ image → reference image

Apply IPAdapter
  ├─ ip_adapter ← IPAdapter Unified Loader
  ├─ image ← reference image
  ├─ weight=0.5-0.8
  └─ noise=0.15

Empty Latent Image → 1024×1024

KSampler
  ├─ steps=20-25, cfg=5-7
  └─ sampler=dpmpp_2m, scheduler=karras

VAE Decode → Save Image
```

## 6. Stock Video + Background Removal
**VRAM: ~5.0 GB | Compositing workflow**

```
Load Video (Upload) → from VideoHelperSuite
  ├─ video → input/stock_videos/clip.mp4
  └─ frame_load_cap=24

RMBG (Remove Background) → from ComfyUI-RMBG
  └─ image ← Load Video

Image Composite Masked → composite foreground over background
  └─ background ← generated image or solid color

Save Video → composite output
```

## 7. Frame Interpolation — Smooth Slow Motion
**VRAM: ~4.0 GB | Post-processing**

```
Load Video → 8 fps video input

IFRNet (from Frame-Interpolation)
  └─ frames ← Load Video
  └─ multiplier=2 (4x for 32fps)

Save Video → interpolated output (higher fps)
```

## VRAM Budget Reference

| Workflow Components | VRAM Used | Safe? |
|---|---|---|
| SDXL base only | 4.0 GB | Yes |
| SDXL + ControlNet | 5.0 GB | Yes |
| SDXL + AnimateDiff (16 frames) | 6.5 GB | Yes |
| SDXL + AnimateDiff + LoRA | 6.8 GB | Tight |
| Flux Q5 (GGUF) only | 6.5 GB | Yes |
| Flux Q5 + LoRA | 7.3 GB | Tight |
| Flux Q5 + ControlNet + IP | ~9 GB | No ❌ |
| SDXL + AnimateDiff + ControlNet + IP | ~9 GB | No ❌ |

## Tips

- **Prefer Q4 over Q5** for Flux if you need headroom for ControlNet/LoRA
- **Use FP16 mode** (`--force-fp16` flag)
- **Use `--lowvram`** when combining ControlNet + AnimateDiff + LoRA
- **Keep frame count** ≤ 16 for AnimateDiff on 8GB
- **Use 512×768** instead of 1024×1024 for video
- **Set batch_size=1** in KSampler

To load a workflow: drag the .json file into the ComfyUI browser window.
