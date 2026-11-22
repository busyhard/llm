# Qwen2.5-Coder-7B-Instruct-Q4_K_M on AMD Radeon R9 290X 4 GB

Benchmark results for `Qwen2.5-Coder-7B-Instruct-Q4_K_M` running on an AMD Radeon R9 290X 4 GB. For each context size, GPU layers were adjusted to maximize available VRAM usage while avoiding out-of-memory errors. Results therefore represent the best practical configuration for this GPU, rather than a fixed layer-offload comparison.

> **Benchmark context:** Each run populates the selected context length before measuring generation. Generation speed therefore reflects a fully active context of the listed size, such as when a coding request includes large files or repository context. Short coding prompts will usually generate faster until their active context reaches a similar token count.

## Test Configuration

- GPU: AMD Radeon R9 290X 4 GB
- CPU: Intel Core i9-10850K (4 threads only)
- RAM: 16 GB DDR4-3200
- Model: Qwen2.5-Coder-7B-Instruct-Q4_K_M
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
| 2K | 0/29 | 77 | 25 | 7 | 5 GB | CPU-only baseline |

### GPU-assisted results

| Context | GPU layers/total | Processing time (s) | Processing (tokens/s) | Generation (tokens/s) | VRAM used / total | System RAM offload | Notes |
| ---: | ---: | ---: | ---: | ---: | --- | ---: | --- |
| 2K | 24/29| 93 | 20 | 12 | 3.7/4.0 GB | 1 GB | |
| 4K | 24/29| 207 | 19 | 11 | 3.8/4.0 GB | 1 GB | |
| 8K | 20/29| 168 | 47 | 10 | 3.8/4.0 GB | 2 GB | |
| 16K | 14/29| 207 | 78 | 6 | 3.8/4.0 GB | 3 GB | |
| 32K | - | - | - | - | - | - | Not passed |