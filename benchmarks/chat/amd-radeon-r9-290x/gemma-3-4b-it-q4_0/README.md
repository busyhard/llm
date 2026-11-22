# Gemma 3 4B Q4_K_M on AMD Radeon R9 290X 4 GB

Benchmark results for `gemma-3-4b-it-Q4_K_M` running on an AMD Radeon R9 290X 4GB. For each context size, GPU layers were adjusted to maximize available VRAM usage while avoiding out-of-memory errors. Results therefore represent the best practical configuration for this GPU, rather than a fixed layer-offload comparison.

> **Benchmark context:** Each run populates the selected context length before measuring generation. Generation speed therefore reflects a fully active context of the listed size, not an otherwise empty chat configured with the same context limit. Interactive chat is usually faster until its actual conversation history reaches a similar token count.

## Test Configuration

- GPU: AMD Radeon R9 290X 4 GB
- CPU: Intel Core i9-10850K (4 threads only)
- RAM: 16 GB DDR4-3200
- Model: gemma-3-4b-it-Q4_K_M
- Tool: koboldcpp v1.124.2, Vulkan
- Quantize KV cache: f16
- Parameters:
    - 4 threads
    - 512 batch size
    - Flash Attention disabled (causes crashes and "pos" token loop)

### CPU-only baseline (4K)

This reference run uses the same 4K context, batch size, thread count, model, and KV-cache quantization as the GPU-assisted 4K run below. All model layers are processed on the CPU.

| Context | GPU layers / total | Processing time (s) | Processing (tokens/s) | Generation (tokens/s) | System RAM | Notes |
| ---: | ---: | ---: | ---: | ---: | --- | --- |
| 4K | 0/35 | 80 | 49 | 11 | 3 GB | CPU-only baseline |

### GPU-assisted results

| Context | GPU layers/total | Processing time (s) | Processing (tokens/s) | Generation (tokens/s) | VRAM used / total | System RAM offload | Notes |
| ---: | ---: | ---: | ---: | ---: | --- | ---: | --- |
| 4K | 35/35 | 13 | 292 | 29 | 3.5/4.0 GB | 0 GB | |
| 8K | 35/35 | 28 | 289 | 28 | 3.6/4.0 GB | 0 GB | |
| 16K | 35/35 | 70 | 230 | 26 | 3.8/4.0 GB | 0 GB | |
| 32K | 35/35 | 194 | 169 | 23 | 4.0/4.0 GB | 0 GB | |
| 64K | 18/35 | 513 | 127 | 5 | 3.9/4.0 GB | 2.5 GB | |
| 128K | — | — | — | — | — | — | Not passed |
