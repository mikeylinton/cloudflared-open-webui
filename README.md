# Cloudflared Open WebUI

## Setting Up Ollama on Your PC with AMD iGPU 780M

If you're using an AMD Ryzen 7000/8000 series CPU with an integrated 780M GPU and want to run Ollama with hardware acceleration, Linux and ROCm make it possible with a few configuration steps.

The following documentation was especially helpful in getting this working:
[Ollama with AMD iGPU 780M + ROCm Setup Guide](https://github.com/alexhegit/Playing-with-ROCm/blob/main/inference/LLM/Run_Ollama_with_AMD_iGPU780M-QuickStart.md)

For a guide to ROCm support for different iGPU/APU or dGPUs you can refer to [AMD GPU Usage](https://llvm.org/docs/AMDGPUUsage.html#processors)

## Initial Specs of SZBOX S7840 Gaming Mini PC

When initially purchased, the **SZBOX S7840 Gaming Mini PC** came with the following specifications:

| **Component** | **Specification** |
| - | - |
| **CPU** | Ryzen 7 8845HS |
| **RAM** | 16GB DDR5 5600MHz (2 x 8GB) |
| **Storage** | 512GB NVMe SSD (with 1 free NVMe slot) |
| **USB Ports** | USB4 support |
| **Networking** | 2.5G LAN, Wi-Fi 6 support |

## Benchmarks

### Benchmarking Commands

The following benchmarking commands were taken directly from the documentation I used during setup ([Ollama with AMD iGPU 780M + ROCm Setup Guide](https://github.com/alexhegit/Playing-with-ROCm/blob/main/inference/LLM/Run_Ollama_with_AMD_iGPU780M-QuickStart.md)):

```bash
OLLAMA_MODEL_NAME=tinyllama

ollama run $OLLAMA_MODEL_NAME "where was beethoven born?" --verbose

for run in {1..10}; do echo "where was beethoven born?" | ollama run $OLLAMA_MODEL_NAME --verbose 2>&1 >/dev/null | grep "eval rate:"; done
```


### Benchmarking Results

| **Model** | **Tokens/s** | **Total RAM** | **AUM (GB)** |
| - | - | - | - |
| **tinyllama** | 96.83 | 16 | 8 |
| **llama2:latest** | 19.15 | 16 | 8 |
| **llama3:8b**  | 17.08 | 16 | 8 |
| **qwen:1.8b**  | 61.44 | 16 | 8 |

I later decided to upgrade the memory to **64GB DDR5 5600MHz** (with the following specifications):

| **Component** | **Specification** |
| - | - |
| **New RAM Model** | Kingston FURY Impact KF556S40IBK2-64  |
| **Capacity** | 64GB (2 x 32GB) |
| **Speed** | 5600 MHz |

Although the results are very simmilar...

| **Model** | **Tokens/s** | **Total RAM** | **AUM (GB)** |
| - | - | - | - |
| **tinyllama** | 97.64 | 64 | 16 |
| **llama2:latest** | 19.42 | 64 | 16 |
| **llama3:8b**  | 16.87 | 64 | 16 |
| **qwen:1.8b**  | 62.51 | 64 | 16 |

Additionally AUM can only be increased up to 16GB in my case, so 32GB memory with 16GB AUM would have probably been enough.

> **Note**: The Tokens/s values represent the average from the benchmark runs.
