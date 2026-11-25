# Nvidia GeForce GTX 780 Ti 3 GB

Benchmark results for running LLMs on an Nvidia GeForce GTX 780 Ti 3GB. For each context size, GPU layers were adjusted to maximize available VRAM usage while avoiding out-of-memory errors. Results therefore represent the best practical configuration for this GPU, rather than a fixed layer-offload comparison.

> **Benchmark context:** Each run populates the selected context length before measuring generation. Generation speed therefore reflects a fully active context of the listed size, not an otherwise empty chat configured with the same context limit. Interactive chat is usually faster until its actual conversation history reaches a similar token count.

## Test Configuration

- GPU: Nvidia GeForce GTX 780 Ti 3 GB
- CPU: Intel Core i9-10850K (4 threads only)
- RAM: 16 GB DDR4-3200
- Tool: koboldcpp v1.125.1, CUDA backend
- Quantize KV cache: f16
- Parameters:
    - 4 threads
    - 512 batch size

### CPU-only baseline (4K context)

This reference run uses the same 4K context, batch size, thread count, model, and KV-cache quantization as the GPU-assisted runs below. All model layers are processed on the CPU.

| Model | Context | Processing time (s) | Processing (tokens/s) | Generation time (s) | Generation (tokens/s) | Total time (s) | GPU layers / total | System RAM | Notes |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- | --- |
| Gemma 3 1B Instruct Q8 | 4096 | 21.23 | 188.27 | 4.01 | 24.94 | 25.23 | 0/27 | 1 GB | CPU-only baseline |
| Gemma 3 4B Instruct Q4_K_M | 4096 | 80.98 | 49.35 | 10.09 | 9.91 | 91.07 | 0/35 | 3 GB | CPU-only baseline |
| Qwen 2.5 1.5B Instruct Q8 | 4096 | 41.95 | 95.27 | 7.51 | 13.32 | 49.45 | 0/29 | 2 GB | CPU-only baseline |
| Qwen 2.5 3B Instruct Q4_K_M | 4096 | 75.83 | 52.70 | 10.47 | 9.55 | 86.29 | 0/37 | 3 GB | CPU-only baseline |
| Qwen 3 4B Instruct Q4_K_M | 4096 | 120.94 | 33.04 | 21.41 | 4.67 | 142.34 | 0/35 | 4 GB | CPU-only baseline |

### GPU-assisted results

| Model | Context | Processing time (s) | Processing (tokens/s) | Generation time (s) | Generation (tokens/s) | Total time (s) | GPU layers/total | VRAM used / total | System RAM offload | Notes |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- | ---: | --- |
| Gemma 3 1B Instruct Q8 | 4096 | 3.06 | 1304.18 | 2.85 | 35.10 | 5.91 | 27/27 | 2.0/3.0 GB | 0 GB |  |
| Gemma 3 1B Instruct Q8 | 8192 | 6.98 | 1159.81 | 2.90 | 34.45 | 9.88 | 27/27 | 2.1/3.0 GB | 0 GB |  |
| Gemma 3 1B Instruct Q8 | 16384 | 15.34 | 1061.26 | 2.99 | 33.47 | 18.33 | 27/27 | 2.1/3.0 GB | 0 GB |  |
| Gemma 3 1B Instruct Q8 | 32768 | 36.68 | 890.57 | 3.19 | 31.31 | 39.88 | 27/27 | 2.2/3.0 GB | 0 GB |  |
| Gemma 3 1B Instruct Q8 | 65536 | 93.29 | 701.45 | 3.60 | 27.81 | 96.88 | 27/27 | 2.4/3.0 GB | 0 GB |  |
| Gemma 3 1B Instruct Q8 | 131072 | 269.22 | 486.48 | 4.37 | 22.87 | 273.60 | 27/27 | 2.7/3.0 GB | 0 GB |  |
| Gemma 3 1B Instruct Q8 | 262144 | 869.46 | 301.39 | 6.12 | 16.34 | 875.58 | 24/27 | 3.0/3.0 GB | 1.5 GB | CPU offload |
| Gemma 3 4B Instruct Q4_K_M | 4096 | 12.82 | 311.72 | 9.70 | 10.31 | 22.52 | 22/35 | 3.0/3.0 GB | 2 GB | CPU offload |
| Gemma 3 4B Instruct Q4_K_M | 8192 | 27.91 | 289.95 | 10.75 | 9.30 | 38.66 | 21/35 | 2.9/3.0 GB | 2 GB | CPU offload |
| Gemma 3 4B Instruct Q4_K_M | 16384 | 60.79 | 267.90 | 12.61 | 7.93 | 73.39 | 20/35 | 2.8/3.0 GB | 2 GB | CPU offload |
| Gemma 3 4B Instruct Q4_K_M | 32768 | 138.44 | 235.98 | 18.63 | 5.37 | 157.07 | 17/35 | 2.9/3.0 GB | 3 GB | CPU offload |
| Qwen 2.5 1.5B Instruct Q8 | 4096 | 5.21 | 767.13 | 3.54 | 28.25 | 8.75 | 29/29 | 2.5/3.0 GB | 0 GB |  |
| Qwen 2.5 1.5B Instruct Q8 | 8192 | 13.73 | 589.15 | 4.24 | 23.57 | 17.98 | 29/29 | 2.7/3.0 GB | 0 GB |  |
| Qwen 2.5 1.5B Instruct Q8 | 16384 | 38.78 | 419.89 | 5.64 | 17.74 | 44.42 | 29/29 | 2.9/3.0 GB | 0 GB |  |
| Qwen 2.5 1.5B Instruct Q8 | 32768 | 124.42 | 262.55 | 16.19 | 6.18 | 140.62 | 25/29 | 3.0/3.0 GB | 1 GB | CPU offload |
| Qwen 2.5 1.5B Instruct Q8 | 65536 | 436.07 | 150.06 | 52.83 | 1.89 | 488.90 | 18/29 | 3.0/3.0 GB | 2 GB | CPU offload |
| Qwen 2.5 3B Instruct Q4_K_M | 4096 | 10.70 | 373.56 | 5.78 | 17.30 | 16.48 | 37/37 | 2.9/3.0 GB | 0 GB |  |
| Qwen 2.5 3B Instruct Q4_K_M | 8192 | 27.38 | 295.52 | 6.58 | 15.21 | 33.96 | 37/37 | 2.9/3.0 GB | 0 GB |  |
| Qwen 2.5 3B Instruct Q4_K_M | 16384 | 76.43 | 213.05 | 13.77 | 7.26 | 90.20 | 32/37 | 2.9/3.0 GB | 1 GB | CPU offload |
| Qwen 2.5 3B Instruct Q4_K_M | 32768 | 236.73 | 138.00 | 39.62 | 2.52 | 276.35 | 25/37 | 2.9/3.0 GB | 2 GB | CPU offload |
| Qwen 3 4B Instruct Q4_K_M | 4096 | 16.77 | 238.25 | 17.20 | 5.81 | 33.97 | 25/35 | 2.9/3.0 GB | 2 GB | CPU offload |
| Qwen 3 4B Instruct Q4_K_M | 8192 | 44.92 | 180.15 | 38.64 | 2.59 | 83.55 | 21/35 | 2.9/3.0 GB | 2 GB | CPU offload |