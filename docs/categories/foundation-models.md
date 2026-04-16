# 🤖 Foundation Models

[← Back to Home](../README.md)

Leading open-source LLMs, vision models, and multimodal systems (2026).

---

## 📋 Table of Contents
- [Overview](#overview)
- [Model List](#model-list)
- [Selection Guide](#selection-guide)
- [Performance Benchmarks](#performance-benchmarks)

---

## Overview

Foundation models are the core of modern AI applications. This curated list includes the top open-source models of 2026, selected based on:
- **Performance benchmarks** (HumanEval, SWE-bench, MMLU)
- **License** (Apache 2.0, MIT preferred)
- **Community adoption** (GitHub stars, downloads)
- **Production readiness**

---

## Model List

| Repo | Description | Stars |
|------|-------------|-------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | State-of-the-art ML models for PyTorch, TensorFlow, and JAX | ![GitHub stars](https://img.shields.io/github/stars/huggingface/transformers?style=social) |
| [QwenLM/Qwen2.5](https://github.com/QwenLM/Qwen2.5) | Premier multilingual model (29+ languages), 235B MoE with 22B active - Apache 2.0 | ![GitHub stars](https://img.shields.io/github/stars/QwenLM/Qwen2.5?style=social) |
| [deepseek-ai/DeepSeek-V3](https://github.com/deepseek-ai/DeepSeek-V3) | 685B MoE activating 37B per token, beats GPT-5 on reasoning - MIT license | ![GitHub stars](https://img.shields.io/github/stars/deepseek-ai/DeepSeek-V3?style=social) |
| [meta-llama/llama](https://github.com/meta-llama/llama) | Llama 4 foundation models (16B-400B params) for general reasoning | ![GitHub stars](https://img.shields.io/github/stars/meta-llama/llama?style=social) |
| [mistralai/mistral-src](https://github.com/mistralai/mistral-src) | Mistral Large - optimized for speed and efficiency, runs on mobile | ![GitHub stars](https://img.shields.io/github/stars/mistralai/mistral-src?style=social) |
| [THUDM/GLM-4](https://github.com/THUDM/GLM-4) | GLM-4 (744B) - S-tier model, 94.2% HumanEval, 73.8% SWE-bench | ![GitHub stars](https://img.shields.io/github/stars/THUDM/GLM-4?style=social) |
| [google/gemma](https://github.com/google/gemma) | Gemma 4 (26B) - frontier intelligence at laptop scale, 85 tokens/sec on consumer hardware | ![GitHub stars](https://img.shields.io/github/stars/google/gemma?style=social) |
| [openai/whisper](https://github.com/openai/whisper) | Robust speech recognition via large-scale weak supervision | ![GitHub stars](https://img.shields.io/github/stars/openai/whisper?style=social) |

---

## Selection Guide

### By Use Case

**🎯 General Purpose & Reasoning**
- **Qwen 2.5** - Best for multilingual tasks (29+ languages), Apache 2.0 license
- **DeepSeek V3** - Best for reasoning tasks, beats GPT-5, MIT license
- **Llama 4** - Established ecosystem, wide adoption, 16B-400B variants

**⚡ Speed & Efficiency**
- **Mistral Large** - Runs on mobile devices, sub-500ms response times
- **Gemma 4** - 85 tokens/sec on consumer hardware, laptop-optimized

**💻 Consumer Hardware**
- **Gemma 4 26B** - Runs on single RTX 4090 (24GB VRAM)
- **Llama 3.2 8B** - Best for 8-16GB VRAM setups

**🔧 Coding & Development**
- **GLM-4** - 94.2% HumanEval, 73.8% SWE-bench
- **Qwen 2.5 Coder** - Dominates coding benchmarks at every size

**🌍 Multilingual**
- **Qwen 2.5** - Premier choice for 29+ languages
- **GLM-4** - Strong bilingual (English/Chinese) support

---

## Performance Benchmarks

### HumanEval (Code Generation)
1. GLM-4: 94.2%
2. Qwen 2.5 Coder: 92.8%
3. DeepSeek V3: 91.5%

### SWE-bench (Real-world Coding)
1. GLM-4: 73.8%
2. Qwen 2.5: 69.2%
3. DeepSeek V3: 67.4%

### MMLU (General Knowledge)
1. DeepSeek V3: 89.7%
2. Qwen 2.5: 88.3%
3. Llama 4: 87.1%

---

## License Comparison

| Model | License | Commercial Use | Restrictions |
|-------|---------|----------------|--------------|
| Qwen 2.5 | Apache 2.0 | ✅ Full | None |
| DeepSeek V3 | MIT | ✅ Full | None |
| Gemma 4 | Custom (Permissive) | ✅ Full | Terms of Use apply |
| Llama 4 | Custom | ⚠️ Limited | 700M+ user restriction |
| GLM-4 | Custom | ✅ Full | Attribution required |
| Mistral | Apache 2.0 | ✅ Full | None |

---

## Quick Deployment

### Using Ollama (Easiest)
```bash
# Gemma 4
ollama run gemma4

# Qwen 2.5
ollama run qwen2.5

# Llama 4
ollama run llama4
```

### Using vLLM (Production)
```bash
pip install vllm
vllm serve QwenLM/Qwen2.5-72B
```

### Using LM Studio (GUI)
Download from [lmstudio.ai](https://lmstudio.ai) - best for non-developers

---

## Related Resources

- [Infrastructure](infrastructure.md) - Serving and optimization tools
- [Deployment & Serving](deployment-serving.md) - Production deployment
- [Developer Tools](developer-tools.md) - AI coding assistants

---

[← Back to Home](../README.md) | [Next: Infrastructure →](infrastructure.md)
