# Qwen2.5-Coder-3B-Instruct-Q4_K_M on AMD Radeon R9 290X 4 GB

Benchmark results for `Qwen2.5-Coder-3B-Instruct-Q4_K_M` running on an AMD Radeon R9 290X 4 GB. For each context size, GPU layers were adjusted to maximize available VRAM usage while avoiding out-of-memory errors. Results therefore represent the best practical configuration for this GPU, rather than a fixed layer-offload comparison.

> **Benchmark context:** Each run populates the selected context length before measuring generation. Generation speed therefore reflects a fully active context of the listed size, such as when a coding request includes large files or repository context. Short coding prompts will usually generate faster until their active context reaches a similar token count.

## Test Configuration

- GPU: AMD Radeon R9 290X 4 GB
- CPU: Intel Core i9-10850K (4 threads only)
- RAM: 16 GB DDR4-3200
- Model: Qwen2.5-Coder-3B-Instruct-Q4_K_M
- Tool: koboldcpp v1.124.2, Vulkan
- Quantize KV cache: f16
- Parameters:
    - 4 threads
    - 512 batch size
    - Flash Attention disabled

## Results

### CPU-only baseline (2K)

This reference run uses the same 2K context, batch size, thread count, model, and KV-cache quantization as the GPU-assisted 2K run below. All model layers are processed on the CPU.

| Context | GPU layers / total | Processing time (s) | Processing (tokens/s) | Generation (tokens/s) | System RAM | Notes |
| ---: | ---: | ---: | ---: | ---: | --- | --- |
| 2K | 0/37 | 39 | 49 | 13 | 2 GB | CPU-only baseline |

### GPU-assisted results

| Context | GPU layers/total | Processing time (s) | Processing (tokens/s) | Generation (tokens/s) | VRAM used / total | System RAM offload | Notes |
| ---: | ---: | ---: | ---: | ---: | --- | ---: | --- |
| 2K | 37/37 | 6 | 324 | 37 | 2.6/4.0 GB | 0 GB | |
| 4K | 37/37 | 12 | 311 | 32 | 2.7/4.0 GB | 0 GB | |
| 8K | 37/37 | 28 | 283 | 26 | 2.8/4.0 GB | 0 GB | |
| 16K | 37/37 | 70 | 233 | 18 | 3.4/4.0 GB | 0 GB | |
| 32K | 18/37 | 415 | 78 | 7 | 3.9/4.0 GB | 2 GB | |