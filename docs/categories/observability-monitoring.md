# 📊 Observability & Monitoring

[← Back to Home](../index.md)

Tools for tracking, debugging, and optimizing LLM applications and AI systems.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Selection Guide](#selection-guide)
- [Quick Start](#quick-start)

---

## Overview

Observability tools provide visibility into AI systems through:
- **LLM Tracing**: Track every model call and token usage
- **Cost Monitoring**: Measure and optimize API spend
- **Performance**: Latency, throughput, error rates
- **Debugging**: Prompt engineering and chain analysis
- **Analytics**: User patterns and model behavior

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [langfuse/langfuse](https://github.com/langfuse/langfuse) | Open-source LLM engineering platform | ![GitHub stars](https://img.shields.io/github/stars/langfuse/langfuse?style=social) |
| [Helicone/helicone](https://github.com/Helicone/helicone) | Open-source LLM observability for developers | ![GitHub stars](https://img.shields.io/github/stars/Helicone/helicone?style=social) |
| [wandb/wandb](https://github.com/wandb/wandb) | Experiment tracking for ML and LLMs | ![GitHub stars](https://img.shields.io/github/stars/wandb/wandb?style=social) |
| [openlit/openlit](https://github.com/openlit/openlit) | OpenTelemetry-native LLM observability | ![GitHub stars](https://img.shields.io/github/stars/openlit/openlit?style=social) |
| [whylabs/whylogs](https://github.com/whylabs/whylogs) | Data and ML monitoring library | ![GitHub stars](https://img.shields.io/github/stars/whylabs/whylogs?style=social) |
| [gantman/phoenix](https://github.com/Arize-ai/phoenix) | ML observability in a notebook | ![GitHub stars](https://img.shields.io/github/stars/Arize-ai/phoenix?style=social) |
| [traceloop/openllmetry](https://github.com/traceloop/openllmetry) | OpenTelemetry for LLMs | ![GitHub stars](https://img.shields.io/github/stars/traceloop/openllmetry?style=social) |

**Note**: LangSmith (from LangChain) is also popular but partially proprietary.

---

## Selection Guide

### By Use Case

**🔍 LLM Application Debugging**
- **Langfuse** - Best traces, prompt management
- **Helicone** - Simple integration, fast
- **OpenLit** - OpenTelemetry compatible
- **LangSmith** - If using LangChain

**💰 Cost Optimization**
- **Langfuse** - Detailed cost tracking per user
- **Helicone** - Real-time cost alerts
- **OpenLIT** - Token usage analytics

**📈 Experiment Tracking**
- **Weights & Biases** - Gold standard for ML
- **Langfuse** - Prompt versioning
- **Phoenix** - Notebook-based analysis

**🏢 Enterprise Compliance**
- **Langfuse** - Self-hosted, GDPR compliant
- **OpenLit** - Open standards, portable
- **WhyLogs** - Data privacy focused

### By Team Size

**Solo Developer**
- **Helicone** - Fastest setup
- **OpenLit** - Free, comprehensive
- **Langfuse Cloud** - Free tier

**Small Team (2-10)**
- **Langfuse** - Team collaboration
- **W&B** - Experiment management
- **Helicone** - Cost tracking

**Enterprise**
- **Langfuse Self-Hosted** - Full control
- **W&B Teams** - Advanced features
- **OpenLit** - Custom infrastructure

---

## Quick Start

### Langfuse - Comprehensive Observability

```bash
# Install
pip install langfuse

# Or use cloud: https://cloud.langfuse.com
```

```python
from langfuse import Langfuse
from openai import OpenAI

# Initialize
langfuse = Langfuse(
    public_key="pk-...",
    secret_key="sk-...",
    host="https://cloud.langfuse.com"  # or self-hosted URL
)

# Wrap OpenAI client
openai = OpenAI()

# Create trace
trace = langfuse.trace(name="chat-completion")

# Track generation
generation = trace.generation(
    name="openai-call",
    model="gpt-4",
    input={"prompt": "What is AI?"},
)

response = openai.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "What is AI?"}]
)

# Update with response
generation.end(
    output=response.choices[0].message.content,
    usage={
        "prompt_tokens": response.usage.prompt_tokens,
        "completion_tokens": response.usage.completion_tokens,
        "total_tokens": response.usage.total_tokens
    }
)
```

**LangChain Integration:**
```python
from langfuse.callback import CallbackHandler

# Add to chain
handler = CallbackHandler(
    public_key="pk-...",
    secret_key="sk-..."
)

llm = OpenAI(callbacks=[handler])
chain = LLMChain(llm=llm, prompt=prompt, callbacks=[handler])
chain.run("query")
```

### Helicone - Simple Proxy

```bash
# Install
npm install @helicone/helicone
```

```python
from openai import OpenAI

# Just change the base URL!
client = OpenAI(
    api_key="your-openai-key",
    base_url="https://oai.helicone.ai/v1",
    default_headers={
        "Helicone-Auth": "Bearer YOUR_HELICONE_API_KEY"
    }
)

# Use normally - automatically tracked
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Hello!"}],
    # Optional: Add metadata
    extra_headers={
        "Helicone-User-Id": "user123",
        "Helicone-Session-Id": "session456",
        "Helicone-Property-Environment": "production"
    }
)
```

**Cost Tracking:**
```python
# Helicone automatically calculates costs
# View in dashboard: helicone.ai/dashboard

# Set budget alerts
# Settings → Alerts → Budget threshold
```

### Weights & Biases - Experiment Tracking

```bash
# Install
pip install wandb
```

```python
import wandb
from openai import OpenAI

# Initialize
wandb.init(
    project="llm-experiments",
    config={
        "model": "gpt-4",
        "temperature": 0.7,
        "max_tokens": 1000
    }
)

client = OpenAI()

# Run experiment
for prompt in test_prompts:
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}],
        temperature=wandb.config.temperature
    )

    # Log metrics
    wandb.log({
        "prompt_length": len(prompt),
        "response_length": len(response.choices[0].message.content),
        "tokens_used": response.usage.total_tokens,
        "cost": response.usage.total_tokens * 0.00003  # GPT-4 pricing
    })

# Finish
wandb.finish()
```

### OpenLit - OpenTelemetry Native

```bash
# Install
pip install openlit
```

```python
import openlit
from openai import OpenAI

# Auto-instrument (monitors all OpenAI calls)
openlit.init(
    otlp_endpoint="http://localhost:4318"  # Your OTLP collector
)

# Use OpenAI normally - automatically traced
client = OpenAI()
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Hello!"}]
)

# Metrics sent to your observability stack:
# - Prometheus
# - Grafana
# - Jaeger
# - Any OTLP-compatible backend
```

**Supported Frameworks:**
- OpenAI, Anthropic, Cohere, HuggingFace
- LangChain, LlamaIndex
- ChromaDB, Pinecone, Qdrant

### Phoenix - Notebook Analysis

```python
import phoenix as px
from phoenix.trace.openai import OpenAIInstrumentor

# Launch Phoenix
session = px.launch_app()

# Instrument OpenAI
OpenAIInstrumentor().instrument()

# Run your LLM code
from openai import OpenAI
client = OpenAI()
response = client.chat.completions.create(...)

# View traces in notebook
px.active_session().view()

# Or open UI
# http://localhost:6006
```

---

## Feature Comparison

| Feature | Langfuse | Helicone | W&B | OpenLit | Phoenix |
|---------|----------|----------|-----|---------|---------|
| **LLM Tracing** | ✅ | ✅ | ⚠️ | ✅ | ✅ |
| **Cost Tracking** | ✅ | ✅ | ⚠️ | ✅ | ⚠️ |
| **Prompt Management** | ✅ | ⚠️ | ❌ | ❌ | ❌ |
| **A/B Testing** | ✅ | ⚠️ | ✅ | ❌ | ❌ |
| **User Analytics** | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ |
| **Self-Hosted** | ✅ | ✅ | ⚠️ | ✅ | ✅ |
| **Cloud Option** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **Real-time** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Annotations** | ✅ | ⚠️ | ✅ | ❌ | ✅ |
| **OpenTelemetry** | ⚠️ | ❌ | ❌ | ✅ | ✅ |

✅ Full support | ⚠️ Partial support | ❌ Not supported

---

## Metrics to Track

### 1. **Cost Metrics**
```python
# Track per request
cost_per_request = (prompt_tokens * input_price +
                   completion_tokens * output_price)

# Track per user
monthly_cost_by_user = sum(costs) group by user_id

# Track per feature
cost_by_feature = sum(costs) group by feature_tag

# Set alerts
if monthly_cost > budget:
    send_alert()
```

### 2. **Performance Metrics**
```python
# Latency
time_to_first_token  # Streaming
total_response_time

# Throughput
requests_per_second
tokens_per_second

# Error rate
error_rate = errors / total_requests
```

### 3. **Quality Metrics**
```python
# User feedback
user_rating  # 1-5 stars
thumbs_up_down

# Model behavior
hallucination_rate
refusal_rate  # Safety refusals
average_response_length
```

### 4. **Token Metrics**
```python
# Usage
total_tokens = prompt_tokens + completion_tokens
tokens_per_user
tokens_per_session

# Efficiency
output_input_ratio = completion_tokens / prompt_tokens
```

---

## Advanced Patterns

### 1. **Prompt Versioning (Langfuse)**

```python
from langfuse import Langfuse

langfuse = Langfuse()

# Create prompt template
langfuse.create_prompt(
    name="summarization",
    prompt="Summarize this text in {{max_words}} words:\n\n{{text}}",
    version=1
)

# Use in production
prompt = langfuse.get_prompt("summarization", version=1)
formatted = prompt.compile(max_words=50, text=document)

# Later: Deploy v2
langfuse.create_prompt(
    name="summarization",
    prompt="Provide a {{length}} summary of:\n\n{{text}}",
    version=2
)

# A/B test versions
```

### 2. **Session Tracking**

```python
# Langfuse example
trace = langfuse.trace(
    name="customer-support-chat",
    user_id="user123",
    session_id="session456",
    metadata={
        "channel": "web",
        "product": "premium"
    }
)

# Track entire conversation
for turn in conversation:
    generation = trace.generation(
        name=f"turn-{turn.id}",
        input=turn.user_message,
        output=turn.assistant_message
    )
```

### 3. **Cost Alerts (Helicone)**

```python
# Set up webhooks for budget alerts
# Dashboard → Settings → Webhooks

# Receive POST when threshold crossed
{
  "alert_type": "budget_exceeded",
  "threshold": 1000,
  "current_spend": 1250,
  "period": "monthly"
}
```

### 4. **Custom Metrics (W&B)**

```python
import wandb

# Log custom evaluation metrics
wandb.log({
    "accuracy": evaluate_accuracy(predictions),
    "coherence": evaluate_coherence(responses),
    "toxicity": evaluate_toxicity(responses),
    "custom_metric": your_metric_function()
})

# Compare across runs
wandb.log({"metric": value}, step=iteration)
```

---

## Self-Hosting Guide

### Langfuse (Docker)

```bash
# Clone
git clone https://github.com/langfuse/langfuse
cd langfuse

# Configure
cp .env.example .env
# Edit .env with database credentials

# Run
docker-compose up -d

# Access at http://localhost:3000
```

### Helicone (Docker)

```bash
docker run -d \
  -p 3000:3000 \
  -e DATABASE_URL=postgresql://... \
  -e OPENAI_API_KEY=your-key \
  helicone/helicone:latest
```

### OpenLit (with Grafana)

```yaml
# docker-compose.yml
version: '3'
services:
  otel-collector:
    image: otel/opentelemetry-collector
    ports:
      - "4318:4318"
    volumes:
      - ./otel-config.yaml:/etc/otel-collector-config.yaml

  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml

  grafana:
    image: grafana/grafana
    ports:
      - "3001:3000"
    environment:
      - GF_AUTH_ANONYMOUS_ENABLED=true
```

---

## Dashboard Examples

### Cost Dashboard (Langfuse)
```
┌─────────────────────────────────┐
│ Monthly Cost: $2,450            │
│ Budget: $3,000 (82% used)       │
├─────────────────────────────────┤
│ Top Users by Cost:              │
│ 1. user@company.com   $450      │
│ 2. team@company.com   $320      │
│ 3. dev@company.com    $180      │
├─────────────────────────────────┤
│ Cost by Model:                  │
│ GPT-4:           $1,800 (73%)   │
│ Claude Sonnet:     $500 (20%)   │
│ GPT-3.5:           $150 (7%)    │
└─────────────────────────────────┘
```

### Performance Dashboard
```
┌─────────────────────────────────┐
│ Latency (p50/p95/p99)           │
│ 450ms / 1.2s / 2.5s             │
├─────────────────────────────────┤
│ Throughput: 150 req/min         │
│ Error Rate: 0.3%                │
├─────────────────────────────────┤
│ Token Usage:                    │
│ Input:  1.2M tokens             │
│ Output: 800K tokens             │
│ Total:  2.0M tokens             │
└─────────────────────────────────┘
```

---

## Best Practices

### 1. **Tag Everything**
```python
# User context
trace.update(
    user_id="user123",
    metadata={
        "plan": "enterprise",
        "org": "acme-corp",
        "region": "us-west"
    }
)

# Feature tracking
generation.update(
    tags=["feature:summarization", "version:v2", "experiment:prompt-A"]
)
```

### 2. **Sample Strategically**
```python
# Don't log everything in production
import random

if random.random() < 0.1:  # 10% sampling
    log_to_observability(trace)

# But always log errors and slow requests
if response_time > threshold or error:
    log_to_observability(trace)
```

### 3. **Annotate for Quality**
```python
# Collect user feedback
trace.score(
    name="user_rating",
    value=4,  # 1-5 stars
    comment="Helpful but verbose"
)

# Use for fine-tuning
low_rated_traces = langfuse.get_traces(
    filter="user_rating < 3"
)
```

### 4. **Monitor Costs in Real-Time**
```python
# Set up alerts
def check_budget():
    today_spend = get_daily_cost()
    if today_spend > DAILY_BUDGET:
        alert_team()
        # Optional: Pause non-critical features
        disable_feature("summarization")

# Run hourly
schedule.every().hour.do(check_budget)
```

---

## Integration Examples

### LangChain + Langfuse

```python
from langchain.chat_models import ChatOpenAI
from langchain.chains import LLMChain
from langfuse.callback import CallbackHandler

handler = CallbackHandler(
    public_key="pk-...",
    secret_key="sk-...",
    session_id="session123",
    user_id="user456"
)

llm = ChatOpenAI(callbacks=[handler])
chain = LLMChain(llm=llm, prompt=prompt, callbacks=[handler])
result = chain.run("query")
```

### LlamaIndex + Helicone

```python
from llama_index import ServiceContext, VectorStoreIndex
from llama_index.llms import OpenAI

# Configure OpenAI with Helicone
llm = OpenAI(
    api_base="https://oai.helicone.ai/v1",
    additional_kwargs={
        "headers": {
            "Helicone-Auth": "Bearer YOUR_KEY"
        }
    }
)

service_context = ServiceContext.from_defaults(llm=llm)
index = VectorStoreIndex.from_documents(docs, service_context=service_context)
```

### OpenAI + W&B

```python
import wandb
from wandb.integration.openai import autolog

# Auto-log all OpenAI calls
autolog({"project": "gpt-4-analysis"})

# Now just use OpenAI normally
client = OpenAI()
response = client.chat.completions.create(...)

# Metrics automatically logged to W&B
```

---

## Troubleshooting

### High Costs

```python
# Identify expensive operations
expensive_traces = langfuse.get_traces(
    filter="total_cost > 1.0",  # > $1 per request
    order_by="total_cost DESC"
)

# Common causes:
# 1. Long context windows → Use RAG to reduce
# 2. High temperature → Lower for deterministic tasks
# 3. Unnecessary calls → Cache results
# 4. Wrong model → Use GPT-3.5 where possible
```

### Slow Responses

```python
# Find slow traces
slow_traces = langfuse.get_traces(
    filter="latency > 5000",  # > 5 seconds
    order_by="latency DESC"
)

# Optimize:
# 1. Use streaming for better UX
# 2. Cache frequent queries
# 3. Use faster models (Claude Haiku, GPT-3.5)
# 4. Parallelize independent LLM calls
```

### Missing Data

```python
# Check instrumentation
assert langfuse.trace_id is not None

# Verify network
langfuse.flush()  # Force send buffered traces

# Check sampling rate
langfuse.sample_rate = 1.0  # 100% for debugging
```

---

## Related Resources

- [Agents & Orchestration](agents-orchestration.md) - Monitor agent behavior
- [Vector Databases](vector-databases.md) - Track vector search performance
- [Developer Tools](developer-tools.md) - Debug AI coding assistants
- [Production AI](production-ai.md) - Production deployment patterns

---

[← Back to Home](../index.md) | [Next: Datasets & Data Tools →](datasets-data-tools.md)
