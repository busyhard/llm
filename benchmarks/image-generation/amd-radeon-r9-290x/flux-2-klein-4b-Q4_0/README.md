# Flux.2 Klein 4B Q4_0 on AMD Radeon R9 290X 4 GB

Benchmark results for `flux-2-klein-4b-Q4_0` running on an AMD Radeon R9 290X with 4 GB VRAM. GPU-assisted runs keep the image model in VRAM; the text encoder runs on the CPU.

## Test Configuration

- GPU: AMD Radeon R9 290X 4 GB
- CPU: Intel Core i9-10850K
- RAM: 16 GB DDR4-3200
- Image model: flux-2-klein-4b-Q4_0
- VAE: flux2vae.safetensors
- Text encoder: Qwen3-4B-Q4_K_M (CPU)
- Tool: KoboldCpp v1.124.2, Vulkan
- Generation parameters:
  - Steps: 4
  - Text-encoder context: 8K
  - Text-encoder batch: 512
  - CPU threads: 4

## Results

### CPU-only baseline (512 × 512)

This reference run disables GPU acceleration and uses the same image size and step count as the GPU-assisted 512 × 512 run below.

| Image size | End-to-end time (s) | System RAM | Notes |
| --- | ---: | --- | --- |
| 512 × 512 |237 | 5 GB | CPU-only baseline |

### GPU-assisted results

| Image size | End-to-end time (s) | Reported diffusion speed (it/s) | VRAM used / total | System RAM | Notes |
| --- | ---: | ---: | --- | --- | --- |
| 512 × 512 | 79 | 83 | 3.0 / 4.0 GB | 2.5 GB | No model offload |
| 768 × 768 | 229 | 76 | 3.1 / 4.0 GB | 2.5 GB | No model offload |
| 1024 × 1024 | — | — | — | — | Failed |

> **Timing note:** End-to-end time is the elapsed time for the complete image-generation request. The reported diffusion-speed field is the value emitted by the tool and is not directly comparable with end-to-end time.
