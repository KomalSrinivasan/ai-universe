# ⚙️ Infrastructure

[← Back to Home](../index.md)

Training, inference optimization, and systems for scaling AI workloads.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Selection Guide](#selection-guide)
- [Quick Start](#quick-start)

---

## Overview

Infrastructure tools power the training and serving of modern AI models. This collection includes frameworks for:
- **Training**: Distributed training, optimization, fine-tuning
- **Inference**: Efficient model serving, quantization
- **Scalability**: Multi-GPU, distributed systems

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | Deep learning framework powering most modern LLMs | ![GitHub stars](https://img.shields.io/github/stars/pytorch/pytorch?style=social) |
| [Lightning-AI/pytorch-lightning](https://github.com/Lightning-AI/pytorch-lightning) | High-level PyTorch training framework | ![GitHub stars](https://img.shields.io/github/stars/Lightning-AI/pytorch-lightning?style=social) |
| [ggerganov/llama.cpp](https://github.com/ggerganov/llama.cpp) | LLM inference in pure C/C++ for CPU and edge devices | ![GitHub stars](https://img.shields.io/github/stars/ggerganov/llama.cpp?style=social) |
| [microsoft/DeepSpeed](https://github.com/microsoft/DeepSpeed) | Distributed training system for trillion-parameter models | ![GitHub stars](https://img.shields.io/github/stars/microsoft/DeepSpeed?style=social) |
| [unslothai/unsloth](https://github.com/unslothai/unsloth) | 2-5x faster LLM fine-tuning with 80% less memory | ![GitHub stars](https://img.shields.io/github/stars/unslothai/unsloth?style=social) |
| [huggingface/trl](https://github.com/huggingface/trl) | Transformer reinforcement learning for RLHF | ![GitHub stars](https://img.shields.io/github/stars/huggingface/trl?style=social) |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | High-throughput and memory-efficient LLM serving | ![GitHub stars](https://img.shields.io/github/stars/vllm-project/vllm?style=social) |

---

## Selection Guide

### By Use Case

**🎯 Training From Scratch**
- **PyTorch** - Industry standard, best ecosystem
- **Lightning** - High-level abstraction, best practices built-in
- **DeepSpeed** - For massive models (>100B parameters)

**⚡ Fine-Tuning**
- **Unsloth** - Fastest, most memory-efficient (2-5x speedup)
- **TRL** - For RLHF and preference learning
- **Lightning** - For production-grade fine-tuning pipelines

**🚀 Inference & Serving**
- **vLLM** - Best throughput, production-grade
- **llama.cpp** - CPU/edge deployment, quantization
- **Lightning** - End-to-end deployment

**📊 Distributed Training**
- **DeepSpeed** - Largest models, ZeRO optimization
- **Lightning** - Multi-GPU, multi-node made easy
- **PyTorch DDP** - Built-in distributed training

---

## Quick Start

### Training with PyTorch Lightning

```python
import pytorch_lightning as pl
from transformers import AutoModelForCausalLM

class LLMFineTuner(pl.LightningModule):
    def __init__(self):
        super().__init__()
        self.model = AutoModelForCausalLM.from_pretrained("model-name")

    def training_step(self, batch, batch_idx):
        outputs = self.model(**batch)
        return outputs.loss

trainer = pl.Trainer(accelerator="gpu", devices=4)
trainer.fit(model)
```

### Fine-Tuning with Unsloth

```python
from unsloth import FastLanguageModel

model, tokenizer = FastLanguageModel.from_pretrained(
    model_name = "unsloth/llama-3-8b",
    max_seq_length = 2048,
    load_in_4bit = True,
)

# 2-5x faster training!
trainer = SFTTrainer(model=model, ...)
trainer.train()
```

### Inference with vLLM

```bash
pip install vllm

python -m vllm.entrypoints.openai.api_server \
    --model meta-llama/Llama-2-7b-hf \
    --tensor-parallel-size 4
```

### CPU Inference with llama.cpp

```bash
# Build
git clone https://github.com/ggerganov/llama.cpp
cd llama.cpp && make

# Run
./main -m models/llama-2-7b.gguf -p "Hello, world!"
```

---

## Performance Comparison

### Training Speed (Llama 7B, Single GPU)

| Framework | Tokens/sec | Memory (GB) |
|-----------|------------|-------------|
| PyTorch (baseline) | 1000 | 24 |
| Lightning | 1050 | 23 |
| Unsloth | 2500 | 12 |
| DeepSpeed ZeRO-3 | 1200 | 16 |

### Inference Throughput (Llama 7B)

| Framework | Tokens/sec | Latency (ms) |
|-----------|------------|--------------|
| Transformers | 50 | 200 |
| vLLM | 250 | 40 |
| llama.cpp (CPU) | 30 | 333 |
| llama.cpp (Metal) | 120 | 83 |

---

## Related Resources

- [Foundation Models](foundation-models.md) - Choose a model to train
- [Deployment & Serving](deployment-serving.md) - Production deployment
- [Observability](observability-monitoring.md) - Monitor training runs

---

[← Back to Home](../index.md) | [Next: Agents & Orchestration →](agents-orchestration.md)
