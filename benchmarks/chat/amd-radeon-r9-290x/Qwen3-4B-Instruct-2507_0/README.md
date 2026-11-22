# Qwen3-4B-Instruct-2507-Q4_K_M on AMD Radeon R9 290X 4 GB

Benchmark results for `Qwen3-4B-Instruct-2507-Q4_K_M` running on an AMD Radeon R9 290X 4 GB. For each context size, GPU layers were adjusted to maximize available VRAM usage while avoiding out-of-memory errors. Results therefore represent the best practical configuration for this GPU, rather than a fixed layer-offload comparison.

> **Benchmark context:** Each run populates the selected context length before measuring generation. Generation speed therefore reflects a fully active context of the listed size, not an otherwise empty chat configured with the same context limit. Interactive chat is usually faster until its actual conversation history reaches a similar token count.

## Test Configuration

- GPU: AMD Radeon R9 290X 4 GB
- CPU: Intel Core i9-10850K (4 threads only)
- RAM: 16 GB DDR4-3200
- Model: Qwen3-4B-Instruct-2507-Q4_K_M
- Tool: koboldcpp v1.124.2, Vulkan
- Quantize KV cache: f16
- Parameters:
    - 4 threads
    - 512 batch size

## Results

### CPU-only baseline (4K)

This reference run uses the same 4K context, batch size, thread count, model, and KV-cache quantization as the GPU-assisted 4K run below. All model layers are processed on the CPU.

| Context | GPU layers / total | Processing time (s) | Processing (tokens/s) | Generation (tokens/s) | System RAM | Notes |
| ---: | ---: | ---: | ---: | ---: | --- | --- |
| 4K | 0/37 | 102 | 39 | 4 | 3 GB | CPU-only baseline |

### GPU-assisted results

| Context | GPU layers/total | Processing time (s) | Processing (tokens/s) | Generation (tokens/s) | VRAM used / total | System RAM offload | Notes |
| ---: | ---: | ---: | ---: | ---: | --- | ---: | --- |
| 4K | 37/37 | 85 | 46 | 22 | 3.7 / 4.0 GB | 0 GB | |
| 8K | 32/37 | 319 | 25 | 8 | 3.8 / 4.0 GB | 1 GB | |
| 16K | 24/37 | 1216 | 13 | 2 | 3.8 / 4.0 GB | 2 GB | |
| 32K | - | - | - | - | - | - |  Not passed |