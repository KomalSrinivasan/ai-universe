# 🎯 Quick Reference Guide

[← Back to Home](../README.md)

Find the right AI tools for your use case quickly.

---

## 🔍 Find Tools by Use Case

### "I want to build a chatbot"
1. **Choose a model**: [Qwen 2.5](../categories/foundation-models.md#qwen-25) or [Llama 4](../categories/foundation-models.md#llama-4)
2. **Add memory**: [mem0](../categories/agents-orchestration.md#mem0)
3. **Deploy**: [Ollama](../categories/deployment-serving.md#ollama) (local) or [vLLM](../categories/deployment-serving.md#vllm) (production)
4. **Monitor**: [Langfuse](../categories/observability-monitoring.md#langfuse)

### "I want to build a RAG application"
1. **Vector DB**: [Qdrant](../categories/vector-databases.md#qdrant) or [Chroma](../categories/vector-databases.md#chroma)
2. **Framework**: [LlamaIndex](../categories/rag-knowledge.md#llamaindex)
3. **Embeddings**: Use Transformers from [HuggingFace](../categories/foundation-models.md#transformers)
4. **Monitor**: [Helicone](../categories/observability-monitoring.md#helicone)

### "I want an AI coding assistant"
1. **IDE Extension**: [Continue](../categories/developer-tools.md#continue) or [Cline](../categories/developer-tools.md#cline)
2. **CLI Tool**: [Aider](../categories/developer-tools.md#aider) or [Plandex](../categories/developer-tools.md#plandex)
3. **Skills**: Browse [SkillsMP.com](https://skillsmp.com) for 66,500+ skills

### "I need to fine-tune a model"
1. **Framework**: [Unsloth](../categories/infrastructure.md#unsloth) (2-5x faster)
2. **Dataset Tool**: [Argilla](../categories/datasets-data-tools.md#argilla)
3. **Training**: [PyTorch Lightning](../categories/infrastructure.md#lightning)
4. **Track**: [Weights & Biases](../categories/observability-monitoring.md#wandb)

### "I want to build AI agents"
1. **Framework**: [LangChain](../categories/agents-orchestration.md#langchain) or [AutoGen](../categories/agents-orchestration.md#autogen)
2. **Tools**: [MCP Servers](../categories/mcp-servers.md)
3. **Memory**: [mem0](../categories/agents-orchestration.md#mem0)
4. **Monitor**: [LangSmith](../categories/observability-monitoring.md#langsmith)

### "I need to evaluate my LLM"
1. **Framework**: [lm-evaluation-harness](../categories/evaluation-testing.md#lm-harness)
2. **LLM-specific**: [DeepEval](../categories/evaluation-testing.md#deepeval)
3. **Monitor**: [Langfuse](../categories/observability-monitoring.md#langfuse)

---

## 💻 Find Tools by Hardware

### "I have a laptop (8-16GB RAM)"
- **Model**: Llama 3.2 8B, Gemma 4 (quantized)
- **Serving**: Ollama
- **Vector DB**: Chroma (embedded mode)

### "I have a gaming PC (RTX 4090, 24GB VRAM)"
- **Model**: Gemma 4 26B, Qwen 2.5 32B
- **Serving**: vLLM or Ollama
- **Vector DB**: Qdrant

### "I have cloud/server access"
- **Model**: Any (DeepSeek V3, Qwen 2.5 235B)
- **Serving**: vLLM, TGI
- **Vector DB**: Milvus, Weaviate

---

## 🎯 Find Tools by Experience Level

### Beginner
**Just starting? Go here:**
1. Install [Ollama](https://ollama.com) - Easiest way to run models
2. Try [Continue](../categories/developer-tools.md#continue) for coding help
3. Use [Chroma](../categories/vector-databases.md#chroma) for vector search

### Intermediate
**Have some experience? Try:**
1. [LangChain](../categories/agents-orchestration.md#langchain) for building agents
2. [Qdrant](../categories/vector-databases.md#qdrant) for better performance
3. [Langfuse](../categories/observability-monitoring.md#langfuse) for monitoring

### Advanced
**Production-ready stack:**
1. [vLLM](../categories/deployment-serving.md#vllm) for serving
2. [Milvus](../categories/vector-databases.md#milvus) for scale
3. [Ray](../categories/production-ai.md#ray) for distributed computing
4. [Langfuse](../categories/observability-monitoring.md#langfuse) + [OpenLIT](../categories/observability-monitoring.md#openlit)

---

## 🏢 Find Tools by Company Stage

### Solo Developer / Prototype
- **Model**: Ollama + Gemma 4
- **Framework**: LangChain
- **Vector DB**: Chroma
- **Monitor**: Helicone (free tier)

### Startup (< 50 users)
- **Model**: Cloud API or self-hosted Qwen 2.5
- **Framework**: LangChain or LlamaIndex
- **Vector DB**: Qdrant
- **Monitor**: Langfuse
- **Deploy**: BentoML

### Scale-up (50-10K users)
- **Model**: vLLM serving Qwen 2.5 or DeepSeek V3
- **Vector DB**: Qdrant or Weaviate
- **Monitor**: Langfuse + LangSmith
- **Deploy**: Kubernetes + vLLM
- **Workflow**: Prefect

### Enterprise (10K+ users)
- **Model**: Multi-region vLLM deployment
- **Vector DB**: Milvus (distributed)
- **Monitor**: Full observability stack
- **Deploy**: Ray + Kubeflow
- **Workflow**: Prefect or Airflow

---

## 📊 Decision Matrix

### Vector Database Choice

| If you need... | Choose... |
|----------------|-----------|
| Fastest setup | Chroma |
| Best filtering | Qdrant |
| Massive scale (billions of vectors) | Milvus |
| Hybrid search | Weaviate |
| SQL integration | pgvector |

### LLM Observability

| If you need... | Choose... |
|----------------|-----------|
| Full-featured, free tier | Langfuse |
| Fastest setup (15 min) | Helicone |
| Deep LangChain integration | LangSmith |
| OpenTelemetry standard | OpenLIT |

### Deployment Platform

| If you need... | Choose... |
|----------------|-----------|
| Highest throughput | vLLM |
| Easiest local setup | Ollama |
| Production-grade SDK | BentoML |
| HuggingFace ecosystem | Text Generation Inference |

---

## 🚀 Quick Start Paths

### Path 1: Build a ChatGPT Clone (Weekend Project)
```
Day 1:
- Install Ollama
- Pull Qwen 2.5 model
- Set up basic chat interface

Day 2:
- Add Langfuse for monitoring
- Deploy with BentoML
```

### Path 2: Build RAG Application (1 Week)
```
Week Plan:
Day 1-2: Set up Chroma + embed documents
Day 3-4: Integrate LlamaIndex
Day 5: Add chat interface
Day 6: Set up monitoring (Langfuse)
Day 7: Deploy and test
```

### Path 3: Production AI System (1 Month)
```
Week 1: Infrastructure (vLLM + Qdrant)
Week 2: Application logic (LangChain)
Week 3: Monitoring & evaluation
Week 4: Testing & deployment (Kubernetes)
```

---

## 🔗 External Resources

- [SkillsMP.com](https://skillsmp.com) - 66,500+ AI agent skills
- [MCP.so](https://mcp.so) - 20,100+ MCP servers
- [Hugging Face](https://huggingface.co) - 230K+ datasets & models

---

[← Back to Home](../README.md)
