# 🚀 Deployment & Serving

[← Back to Home](../index.md)

Production-ready platforms and tools for deploying and serving LLMs at scale.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Selection Guide](#selection-guide)
- [Quick Start](#quick-start)

---

## Overview

Deployment platforms provide:
- **Model Serving**: High-performance inference APIs
- **Quantization**: Reduce model size and cost
- **Scalability**: Auto-scaling and load balancing
- **Edge Deployment**: Run on CPUs, mobile, browsers

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | High-throughput and memory-efficient LLM serving | ![GitHub stars](https://img.shields.io/github/stars/vllm-project/vllm?style=social) |
| [ollama/ollama](https://github.com/ollama/ollama) | Run LLMs locally with ease | ![GitHub stars](https://img.shields.io/github/stars/ollama/ollama?style=social) |
| [huggingface/text-generation-inference](https://github.com/huggingface/text-generation-inference) | Production-ready LLM serving from HuggingFace | ![GitHub stars](https://img.shields.io/github/stars/huggingface/text-generation-inference?style=social) |
| [ggerganov/llama.cpp](https://github.com/ggerganov/llama.cpp) | LLM inference in C/C++ for CPU and edge | ![GitHub stars](https://img.shields.io/github/stars/ggerganov/llama.cpp?style=social) |
| [bentoml/OpenLLM](https://github.com/bentoml/OpenLLM) | Open platform for operating LLMs in production | ![GitHub stars](https://img.shields.io/github/stars/bentoml/OpenLLM?style=social) |
| [skypilot-org/skypilot](https://github.com/skypilot-org/skypilot) | Run LLMs on any cloud with one command | ![GitHub stars](https://img.shields.io/github/stars/skypilot-org/skypilot?style=social) |
| [neuralmagic/nm-vllm](https://github.com/neuralmagic/nm-vllm) | Optimized vLLM with sparsity support | ![GitHub stars](https://img.shields.io/github/stars/neuralmagic/nm-vllm?style=social) |
| [triton-inference-server/server](https://github.com/triton-inference-server/server) | NVIDIA's production inference serving | ![GitHub stars](https://img.shields.io/github/stars/triton-inference-server/server?style=social) |

---

## Selection Guide

### By Use Case

**☁️ Cloud Production**
- **vLLM** - Best throughput and efficiency
- **Text Generation Inference** - HuggingFace ecosystem
- **BentoML** - MLOps platform
- **Triton** - Multi-model, enterprise

**💻 Local Development**
- **Ollama** - Easiest setup, Mac/Windows/Linux
- **llama.cpp** - Maximum compatibility
- **OpenLLM** - Python-native

**📱 Edge/Mobile**
- **llama.cpp** - CPU optimized
- **ONNX Runtime** - Cross-platform
- **MLC LLM** - Mobile and WebGPU

**💰 Cost Optimization**
- **vLLM** - PagedAttention memory savings
- **llama.cpp** - Quantization (4-bit, 8-bit)
- **NeuralMagic** - Sparse models

### By Scale

**Small (<100 req/min)**
- Ollama, llama.cpp, OpenLLM

**Medium (100-1000 req/min)**
- vLLM, Text Generation Inference

**Large (1000+ req/min)**
- vLLM + multi-GPU
- Triton + orchestration
- SkyPilot + cloud scaling

---

## Quick Start

### vLLM - Production Serving

```bash
# Install
pip install vllm

# Serve model
python -m vllm.entrypoints.openai.api_server \
    --model meta-llama/Llama-2-7b-chat-hf \
    --tensor-parallel-size 2 \  # Use 2 GPUs
    --max-model-len 4096

# API compatible with OpenAI
curl http://localhost:8000/v1/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "meta-llama/Llama-2-7b-chat-hf",
        "prompt": "What is AI?",
        "max_tokens": 100
    }'
```

**Python Client:**
```python
from openai import OpenAI

# Point to vLLM server
client = OpenAI(
    api_key="EMPTY",
    base_url="http://localhost:8000/v1"
)

response = client.chat.completions.create(
    model="meta-llama/Llama-2-7b-chat-hf",
    messages=[
        {"role": "user", "content": "Explain quantum computing"}
    ]
)

print(response.choices[0].message.content)
```

### Ollama - Local Models

```bash
# Install (Mac)
brew install ollama

# Or Linux
curl -fsSL https://ollama.com/install.sh | sh

# Run model
ollama run llama2

# Or specific model
ollama run codellama:13b

# API server (runs automatically)
curl http://localhost:11434/api/generate -d '{
  "model": "llama2",
  "prompt": "Why is the sky blue?"
}'
```

**Python Client:**
```python
import ollama

# Chat
response = ollama.chat(
    model='llama2',
    messages=[
        {'role': 'user', 'content': 'Why is the sky blue?'}
    ]
)
print(response['message']['content'])

# Streaming
for chunk in ollama.chat(
    model='llama2',
    messages=[{'role': 'user', 'content': 'Tell me a story'}],
    stream=True
):
    print(chunk['message']['content'], end='')
```

### Text Generation Inference (TGI)

```bash
# Docker
docker run --gpus all --shm-size 1g -p 8080:80 \
    ghcr.io/huggingface/text-generation-inference:latest \
    --model-id meta-llama/Llama-2-7b-chat-hf \
    --num-shard 2 \  # Multi-GPU
    --max-total-tokens 4096

# Or with quantization
docker run --gpus all -p 8080:80 \
    ghcr.io/huggingface/text-generation-inference:latest \
    --model-id TheBloke/Llama-2-7B-Chat-GPTQ \
    --quantize gptq
```

**Python Client:**
```python
from huggingface_hub import InferenceClient

client = InferenceClient(model="http://localhost:8080")

# Generate
text = client.text_generation(
    prompt="What is the capital of France?",
    max_new_tokens=100
)

# Stream
for token in client.text_generation(
    prompt="Write a poem about AI",
    max_new_tokens=200,
    stream=True
):
    print(token, end='')
```

### llama.cpp - CPU Inference

```bash
# Build
git clone https://github.com/ggerganov/llama.cpp
cd llama.cpp
make

# Download GGUF model
wget https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGUF/resolve/main/llama-2-7b-chat.Q4_K_M.gguf

# Run
./main -m llama-2-7b-chat.Q4_K_M.gguf -p "What is AI?" -n 128

# API server
./server -m llama-2-7b-chat.Q4_K_M.gguf --port 8080
```

**Python Binding:**
```python
from llama_cpp import Llama

# Load model
llm = Llama(
    model_path="./llama-2-7b-chat.Q4_K_M.gguf",
    n_ctx=2048,  # Context window
    n_threads=8  # CPU cores
)

# Generate
output = llm(
    "Q: What is AI? A:",
    max_tokens=100,
    stop=["Q:", "\n"],
    echo=True
)

print(output['choices'][0]['text'])
```

### BentoML - Production Platform

```python
# bentofile.yaml
service: "llm_service.py:svc"
python:
  packages:
    - vllm
    - transformers

# llm_service.py
import bentoml
from vllm import LLM

@bentoml.service
class LLMService:
    def __init__(self):
        self.llm = LLM(model="meta-llama/Llama-2-7b-chat-hf")

    @bentoml.api
    def generate(self, prompt: str) -> str:
        outputs = self.llm.generate([prompt])
        return outputs[0].outputs[0].text
```

```bash
# Build
bentoml build

# Serve locally
bentoml serve llm_service:latest

# Deploy to cloud
bentoml containerize llm_service:latest
docker push myregistry/llm_service:latest

# Or deploy to BentoCloud
bentoml deploy llm_service:latest
```

### SkyPilot - Multi-Cloud

```yaml
# llama.yaml
resources:
  cloud: aws  # or gcp, azure
  accelerators: A100:2
  disk_size: 512

setup: |
  pip install vllm

run: |
  python -m vllm.entrypoints.openai.api_server \
    --model meta-llama/Llama-2-70b-chat-hf \
    --tensor-parallel-size 2
```

```bash
# Launch
sky launch llama.yaml

# Auto-scale
sky autoscale llama.yaml --min-nodes 1 --max-nodes 5

# Spot instances (cheaper)
sky launch llama.yaml --use-spot
```

---

## Performance Benchmarks

### Throughput (Llama 2 7B, A100 GPU)

| Framework | Tokens/sec | Batch Size | Latency (P50) |
|-----------|------------|------------|---------------|
| vLLM | 4,200 | 128 | 15ms |
| TGI | 3,800 | 96 | 18ms |
| Triton | 3,500 | 64 | 20ms |
| BentoML | 3,200 | 64 | 22ms |
| Transformers (baseline) | 800 | 8 | 80ms |

### Memory Efficiency (Llama 2 70B)

| Method | GPU Memory | GPUs Needed | Cost/Hour |
|--------|------------|-------------|-----------|
| FP16 (baseline) | 140GB | 2× A100 (80GB) | $6.00 |
| vLLM (PagedAttention) | 90GB | 2× A100 (80GB) | $6.00 |
| GPTQ 4-bit | 40GB | 1× A100 (80GB) | $3.00 |
| AWQ 4-bit | 38GB | 1× A100 (80GB) | $3.00 |
| llama.cpp Q4_K_M | 35GB | 1× A100 (80GB) | $3.00 |

### CPU Performance (Llama 2 7B)

| Quantization | Size | RAM | Tokens/sec (16 cores) |
|--------------|------|-----|----------------------|
| FP16 | 13GB | 16GB | 2 |
| Q8 | 7GB | 8GB | 5 |
| Q4_K_M | 4GB | 6GB | 10 |
| Q4_K_S | 3.5GB | 5GB | 12 |
| Q3_K_M | 3GB | 4GB | 15 |

---

## Quantization Guide

### GGUF Formats (llama.cpp)

```
Q2_K - 2.5-3.0 bpw (bits per weight) - Smallest, lowest quality
Q3_K_S - ~3.5 bpw - Small, low quality
Q3_K_M - ~3.9 bpw - Medium quality
Q4_K_S - ~4.0 bpw - Small, reasonable quality
Q4_K_M - ~4.8 bpw - Recommended (best quality/size)
Q5_K_S - ~5.0 bpw - Large, better quality
Q5_K_M - ~5.5 bpw - Large, very good quality
Q6_K - ~6.0 bpw - Very large, excellent quality
Q8_0 - ~8.5 bpw - Huge, best quality
```

**Recommendation**: Start with Q4_K_M, use Q5_K_M if quality issues

### GPTQ (GPU Quantization)

```python
from transformers import AutoModelForCausalLM

# Load GPTQ model (4-bit)
model = AutoModelForCausalLM.from_pretrained(
    "TheBloke/Llama-2-7B-Chat-GPTQ",
    device_map="auto",
    trust_remote_code=False,
    revision="main"
)

# Inference
inputs = tokenizer("Hello", return_tensors="pt").to("cuda")
outputs = model.generate(**inputs)
```

### AWQ (Activation-aware Weight Quantization)

```python
from awq import AutoAWQForCausalLM

# Load AWQ model
model = AutoAWQForCausalLM.from_quantized(
    "TheBloke/Llama-2-7B-Chat-AWQ",
    fuse_layers=True
)

# 2-3x faster than GPTQ with similar quality
```

---

## Scaling Patterns

### 1. **Vertical Scaling (Bigger GPU)**

```yaml
# Single large GPU
Model: Llama 2 70B
GPU: A100 80GB
Quantization: 4-bit GPTQ
Batch Size: 32
Throughput: ~1000 tokens/sec
Cost: $3/hour
```

### 2. **Horizontal Scaling (Multi-GPU)**

```python
# vLLM with tensor parallelism
python -m vllm.entrypoints.openai.api_server \
    --model meta-llama/Llama-2-70b-chat-hf \
    --tensor-parallel-size 4 \  # Split across 4 GPUs
    --pipeline-parallel-size 1

# Model sharded across GPUs
# Linear scaling up to 8 GPUs
```

### 3. **Load Balancing (Multiple Replicas)**

```yaml
# Kubernetes deployment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: llm-serving
spec:
  replicas: 4  # 4 instances
  template:
    spec:
      containers:
      - name: vllm
        image: vllm/vllm-openai:latest
        resources:
          limits:
            nvidia.com/gpu: 1

---
apiVersion: v1
kind: Service
metadata:
  name: llm-service
spec:
  type: LoadBalancer
  selector:
    app: llm-serving
  ports:
  - port: 8000
```

### 4. **Auto-Scaling**

```python
# SkyPilot auto-scale
sky launch llm.yaml \
    --min-nodes 2 \
    --max-nodes 10 \
    --scale-up-threshold 0.7 \  # CPU/GPU usage
    --scale-down-timeout 300  # 5 min cooldown
```

---

## API Optimization

### 1. **Batching**

```python
# vLLM automatic batching
# Just send concurrent requests!

import asyncio
from openai import AsyncOpenAI

client = AsyncOpenAI(
    api_key="EMPTY",
    base_url="http://localhost:8000/v1"
)

async def generate(prompt):
    response = await client.chat.completions.create(
        model="llama-2-7b",
        messages=[{"role": "user", "content": prompt}]
    )
    return response.choices[0].message.content

# vLLM automatically batches these
results = await asyncio.gather(*[
    generate(f"Prompt {i}") for i in range(100)
])
```

### 2. **Streaming**

```python
# Better UX with streaming
for chunk in client.chat.completions.create(
    model="llama-2-7b",
    messages=[{"role": "user", "content": "Write an essay"}],
    stream=True
):
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end='')
```

### 3. **Caching**

```python
# Prompt caching (vLLM)
import hashlib
from functools import lru_cache

@lru_cache(maxsize=1000)
def cached_generate(prompt_hash, prompt):
    return llm.generate(prompt)

prompt = "Explain quantum computing"
prompt_hash = hashlib.md5(prompt.encode()).hexdigest()
result = cached_generate(prompt_hash, prompt)
```

---

## Monitoring & Debugging

### vLLM Metrics

```python
# Enable Prometheus metrics
python -m vllm.entrypoints.openai.api_server \
    --model llama-2-7b \
    --enable-metrics

# Metrics at http://localhost:8000/metrics

# Key metrics:
# - vllm:num_requests_running
# - vllm:gpu_cache_usage_perc
# - vllm:avg_generation_throughput_toks_per_s
# - vllm:avg_time_to_first_token_seconds
```

### Ollama Logs

```bash
# View logs
ollama logs

# Specific model
ollama logs llama2

# Debug mode
OLLAMA_DEBUG=1 ollama run llama2
```

### Health Checks

```python
# vLLM health endpoint
import requests

response = requests.get("http://localhost:8000/health")
assert response.status_code == 200

# Check model is loaded
response = requests.get("http://localhost:8000/v1/models")
models = response.json()
assert "llama-2-7b" in [m["id"] for m in models["data"]]
```

---

## Cost Optimization Strategies

### 1. **Right-Sizing**

```
Don't use Llama 2 70B when 7B suffices!

Task: Simple Q&A
❌ Llama 2 70B: $0.01/1k tokens
✅ Llama 2 7B: $0.002/1k tokens
Savings: 80%

Task: Complex reasoning
✅ Llama 2 70B or Claude Opus
```

### 2. **Spot Instances**

```bash
# SkyPilot with spot
sky launch llm.yaml --use-spot

# AWS A100: $3/hr → $0.90/hr (70% savings)
# Automatic failover if preempted
```

### 3. **Batch Processing**

```python
# Don't: 1000 sequential requests
for prompt in prompts:
    generate(prompt)  # $10, 10 minutes

# Do: Single batched request
generate_batch(prompts)  # $3, 2 minutes
```

### 4. **Quantization**

```
Llama 2 70B FP16: 2× A100 80GB = $6/hour
Llama 2 70B GPTQ 4-bit: 1× A100 80GB = $3/hour

Savings: 50% with minimal quality loss
```

---

## Best Practices

### 1. **Model Selection**
```python
# Decision tree
if task == "simple_classification":
    model = "distilbert-base"  # Small, fast, cheap
elif task == "general_chat":
    model = "llama-2-7b"  # Good quality, reasonable cost
elif task == "complex_reasoning":
    model = "llama-2-70b"  # or Claude Opus via API
elif task == "code_generation":
    model = "codellama-13b"  # Specialized
```

### 2. **Context Management**
```python
# Don't: Send entire chat history every time
messages = all_previous_messages + [new_message]  # ❌ Expensive

# Do: Sliding window or summarization
messages = recent_messages[-5:] + [new_message]  # ✅ Efficient
```

### 3. **Error Handling**
```python
from tenacity import retry, stop_after_attempt, wait_exponential

@retry(
    stop=stop_after_attempt(3),
    wait=wait_exponential(multiplier=1, min=4, max=10)
)
def robust_generate(prompt):
    try:
        return llm.generate(prompt)
    except Exception as e:
        logger.error(f"Generation failed: {e}")
        raise
```

---

## Related Resources

- [Infrastructure](infrastructure.md) - Training and optimization
- [Observability](observability-monitoring.md) - Monitor serving metrics
- [Production AI](production-ai.md) - Production patterns
- [Vector Databases](vector-databases.md) - RAG deployments

---

[← Back to Home](../index.md) | [Next: Production AI →](production-ai.md)
