# AI Benchmarks on Old Graphics Cards

Can older graphics cards run modern AI models?

This repository explores the capabilities and limitations of legacy GPUs when running modern AI workloads, including local LLM inference, code assistance, and image generation.

The goal is to document real-world performance, VRAM limitations, CPU/GPU offloading configurations, software compatibility, and the practical usability of AI models on older hardware.

## Benchmark Categories

### Chat / LLM Inference

Performance benchmarks for conversational language models running locally.

| GPU | Model | Details |
|---|---|---|
| AMD Radeon R9 290X 4 GB | Gemma 3 4B IT Q4_0 | [Benchmark](benchmarks/chat/amd-radeon-r9-290x/gemma-3-4b-it-q4_0/README.md) |
| AMD Radeon R9 290X 4 GB | Qwen3 4B Instruct 2507 | [Benchmark](benchmarks/chat/amd-radeon-r9-290x/Qwen3-4B-Instruct-2507_0/README.md) |
| NVIDIA GeForce GTX 680 4 GB | Gemma 3 4B IT Q4_K_M | [Benchmark](benchmarks/chat/nvidia-geforce-gtx-680/gemma-3-4b-it-q4_0/README.md) |
| NVIDIA GeForce GTX 680 4 GB | Qwen3 4B Instruct 2507 | [Benchmark](benchmarks/chat/nvidia-geforce-gtx-680/Qwen3-4B-Instruct-2507_0/README.md) |
| NVIDIA GeForce GTX 780 Ti 3 GB | Gemma 3, Qwen | [Benchmark](benchmarks/chat/nvidia-geforce-gtx-780-ti/README.md) |

### Code Assistance

Benchmarks evaluating the ability of older GPUs to run models designed for programming and code generation.

| GPU | Model | Details |
|---|---|---|
| AMD Radeon R9 290X 4 GB | Qwen2.5-Coder 1.5B Instruct | [Benchmark](benchmarks/code/amd-radeon-r9-290x/Qwen2.5-Coder-1.5B-Instruct/README.md) |
| AMD Radeon R9 290X 4 GB | Qwen2.5-Coder 3B Instruct | [Benchmark](benchmarks/code/amd-radeon-r9-290x/Qwen2.5-Coder-3B-Instruct/README.md) |
| AMD Radeon R9 290X 4 GB | Qwen2.5-Coder 7B Instruct | [Benchmark](benchmarks/code/amd-radeon-r9-290x/Qwen2.5-Coder-7B-Instruct/README.md) |

No GTX 680 code-assistance benchmarks are currently documented.

### Image Generation

Benchmarks exploring local image generation on legacy graphics hardware.

| GPU | Model | Details |
|---|---|---|
| AMD Radeon R9 290X 4 GB | FLUX.2 Klein 4B Q4_0 | [Benchmark](benchmarks/image-generation/amd-radeon-r9-290x/flux-2-klein-4b-Q4_0/README.md) |

**NVIDIA GeForce GTX 680:** Image generation attempts were unsuccessful. No images could be generated with the tested software configuration.

## Tested Hardware

### AMD Radeon R9 290X – 4 GB GDDR5

An AMD GCN-based flagship GPU from 2013. Despite its age, it can run quantized LLMs and image-generation models using a Vulkan-based backend.

### NVIDIA GeForce GTX 680 – 4 GB GDDR5

An NVIDIA Kepler-based flagship GPU from 2012.

Its AI capabilities are significantly more limited due to its lack of compatibility with modern CUDA software stacks. The tested configuration relies on the Vulkan backend instead of CUDA.

Although it can run quantized LLMs, performance is not necessarily better than CPU-only execution. Image generation was unsuccessful with the tested configuration.

## Software Compatibility and Limitations

Legacy GPUs often require alternative execution backends and workarounds because they are no longer supported by current GPU computing software stacks.

- **AMD Radeon R9 290X:** Tested using Vulkan for GPU acceleration.
- **NVIDIA GeForce GTX 680:** Tested using Vulkan because of its limitations with modern CUDA support.
- **Vulkan:** Provides an alternative GPU acceleration path, but compatibility and performance depend on the GPU architecture, drivers, and application implementation.

The GTX 680 results demonstrate that having GPU acceleration available does not automatically translate into better AI performance. Backend compatibility, architecture support, and available VRAM are equally important.

## Benchmark Methodology

Each model has a dedicated README containing its configuration, testing methodology, and benchmark results.

Depending on the workload, benchmarks may include:

- CPU-only baseline measurements.
- GPU-assisted execution.
- Different context sizes and GPU layer configurations.
- VRAM utilization and memory limitations.
- Generation speed and practical performance.
- Model-specific settings and observations.

### Important Notes

- GPU configurations are optimized for the available VRAM rather than necessarily using identical GPU layer counts across tests.
- CPU-only baselines provide a reference for evaluating the benefit of GPU acceleration.
- Results should be interpreted in the context of the specific hardware, model quantization, software configuration, backend, and workload.
- A model successfully running does not necessarily mean it is practical for interactive use.
- Failed workloads are documented where relevant to illustrate hardware and software compatibility limitations.

## Repository Structure

```text
.
├── README.md
└── benchmarks
    ├── chat
    │   ├── amd-radeon-r9-290x
    │   └── nvidia-geforce-gtx-680
    ├── code
    │   └── amd-radeon-r9-290x
    └── image-generation
        └── amd-radeon-r9-290x
```

Each model directory contains its own `README.md` with detailed benchmark information.

## License

See [LICENSE](LICENSE).