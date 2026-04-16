# 🧪 Evaluation & Testing

[← Back to Home](../index.md)

Frameworks and benchmarks for evaluating and testing LLM applications.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Selection Guide](#selection-guide)
- [Quick Start](#quick-start)

---

## Overview

Evaluation tools provide:
- **Automated Testing**: Unit tests for LLM outputs
- **Benchmarking**: Compare models on standardized tasks
- **Quality Metrics**: Measure accuracy, relevance, safety
- **Regression Testing**: Catch degradations

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [confident-ai/deepeval](https://github.com/confident-ai/deepeval) | LLM evaluation framework with 14+ metrics | ![GitHub stars](https://img.shields.io/github/stars/confident-ai/deepeval?style=social) |
| [EleutherAI/lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) | Standard framework for LLM evaluation (200+ tasks) | ![GitHub stars](https://img.shields.io/github/stars/EleutherAI/lm-evaluation-harness?style=social) |
| [openai/evals](https://github.com/openai/evals) | Evaluation framework and registry from OpenAI | ![GitHub stars](https://img.shields.io/github/stars/openai/evals?style=social) |
| [patronus-ai/patronus](https://github.com/explodinggradients/ragas) | RAG assessment framework (RAGAS) | ![GitHub stars](https://img.shields.io/github/stars/explodinggradients/ragas?style=social) |
| [langchain-ai/langsmith-sdk](https://github.com/langchain-ai/langsmith-sdk) | LangChain evaluation and testing (partially open) | ![GitHub stars](https://img.shields.io/github/stars/langchain-ai/langsmith-sdk?style=social) |
| [microsoft/promptflow](https://github.com/microsoft/promptflow) | Evaluation and testing for LLM apps | ![GitHub stars](https://img.shields.io/github/stars/microsoft/promptflow?style=social) |

---

## Selection Guide

### By Use Case

**📊 General LLM Evaluation**
- **LM Evaluation Harness** - Academic benchmarks
- **DeepEval** - Production testing
- **OpenAI Evals** - Custom evaluations

**🔍 RAG-Specific**
- **RAGAS** - RAG evaluation metrics
- **DeepEval** - RAG test cases
- **LangSmith** - End-to-end tracing

**⚡ Unit Testing**
- **DeepEval** - Pytest integration
- **PromptFlow** - Flow testing
- **LangSmith** - Dataset testing

**🏆 Benchmarking**
- **LM Evaluation Harness** - 200+ standard tasks
- **OpenAI Evals** - Custom benchmarks
- **HELM** - Holistic evaluation

### By Team Size

**Solo Developer**
- **DeepEval** - Quick setup
- **RAGAS** - RAG focus
- **LM Harness** - Benchmark models

**Small Team (2-10)**
- **LangSmith** - Collaborative testing
- **PromptFlow** - Visual workflows
- **DeepEval** - CI/CD integration

**Enterprise**
- **Custom framework** - Specific needs
- **LangSmith Enterprise** - Team features
- **PromptFlow + Azure** - Full stack

---

## Quick Start

### DeepEval - Production Testing

```bash
# Install
pip install deepeval
```

```python
from deepeval import assert_test
from deepeval.metrics import AnswerRelevancyMetric, FaithfulnessMetric
from deepeval.test_case import LLMTestCase

def test_customer_support_bot():
    # Define test case
    test_case = LLMTestCase(
        input="How do I reset my password?",
        actual_output="You can reset your password by clicking 'Forgot Password' on the login page.",
        expected_output="Guide user to password reset flow",
        context=["Password reset documentation", "Login page help"]
    )

    # Define metrics
    relevancy_metric = AnswerRelevancyMetric(threshold=0.7)
    faithfulness_metric = FaithfulnessMetric(threshold=0.8)

    # Assert
    assert_test(test_case, [relevancy_metric, faithfulness_metric])

# Run with pytest
# pytest test_llm.py
```

**Available Metrics:**
```python
from deepeval.metrics import (
    AnswerRelevancyMetric,  # Is answer relevant to question?
    FaithfulnessMetric,  # Is answer grounded in context?
    ContextualRelevancyMetric,  # Is retrieved context relevant?
    HallucinationMetric,  # Does output contain hallucinations?
    ToxicityMetric,  # Is output toxic?
    BiasMetric,  # Does output show bias?
    GEval,  # Custom criteria evaluation
)
```

**Synthetic Data for Testing:**
```python
from deepeval.synthesizer import Synthesizer

synthesizer = Synthesizer()

# Generate test cases from docs
test_cases = synthesizer.generate_goldens_from_docs(
    document_paths=["./docs"],
    num_goldens=50
)

# Each has: input, expected_output, context
for test_case in test_cases:
    # Run your RAG pipeline
    actual_output = rag_pipeline(test_case.input)

    # Evaluate
    metric = AnswerRelevancyMetric()
    score = metric.measure(
        test_case=LLMTestCase(
            input=test_case.input,
            actual_output=actual_output,
            expected_output=test_case.expected_output
        )
    )
```

### LM Evaluation Harness - Benchmarking

```bash
# Install
pip install lm-eval
```

```bash
# Evaluate on MMLU (knowledge benchmark)
lm_eval --model hf \
    --model_args pretrained=meta-llama/Llama-2-7b-hf \
    --tasks mmlu \
    --batch_size 8

# Multiple tasks
lm_eval --model hf \
    --model_args pretrained=meta-llama/Llama-2-7b-hf \
    --tasks hendrycks_ethics,truthfulqa,gsm8k \
    --output_path results/

# Custom model (API)
lm_eval --model openai-chat-completions \
    --model_args model=gpt-4 \
    --tasks mmlu
```

**Python API:**
```python
from lm_eval import evaluator

results = evaluator.simple_evaluate(
    model="hf",
    model_args="pretrained=meta-llama/Llama-2-7b-hf",
    tasks=["mmlu", "hellaswag", "arc_challenge"],
    batch_size=8
)

print(f"MMLU Score: {results['results']['mmlu']['acc']}")
print(f"HellaSwag: {results['results']['hellaswag']['acc_norm']}")
```

**200+ Available Tasks:**
- **Knowledge**: MMLU, TriviaQA, NaturalQuestions
- **Reasoning**: BBH, GSM8K, ARC
- **Code**: HumanEval, MBPP
- **Safety**: ToxiGen, CrowS-Pairs
- **Truthfulness**: TruthfulQA

### RAGAS - RAG Evaluation

```bash
# Install
pip install ragas
```

```python
from ragas import evaluate
from ragas.metrics import (
    faithfulness,
    answer_relevancy,
    context_precision,
    context_recall
)
from datasets import Dataset

# Your RAG outputs
data = {
    "question": ["What is the capital of France?"],
    "answer": ["Paris is the capital of France."],
    "contexts": [["France is a country in Europe. Its capital is Paris."]],
    "ground_truth": ["Paris"]
}

dataset = Dataset.from_dict(data)

# Evaluate
results = evaluate(
    dataset,
    metrics=[
        faithfulness,
        answer_relevancy,
        context_precision,
        context_recall
    ]
)

print(results)
# {
#   "faithfulness": 0.95,
#   "answer_relevancy": 0.92,
#   "context_precision": 0.88,
#   "context_recall": 0.90
# }
```

**Metrics Explained:**
- **Faithfulness**: Is answer grounded in retrieved context?
- **Answer Relevancy**: Does answer address the question?
- **Context Precision**: Is retrieved context relevant?
- **Context Recall**: Did we retrieve all relevant info?

### OpenAI Evals

```bash
# Install
git clone https://github.com/openai/evals
cd evals
pip install -e .
```

```bash
# Run existing eval
oaieval gpt-3.5-turbo my-eval

# Create custom eval
# evals/registry/evals/my-eval.yaml
my-eval:
  class: evals.elsuite.basic.match:Match
  args:
    samples_jsonl: my-samples.jsonl
```

**Custom Evaluation:**
```python
# my-eval.py
import evals
from evals.api import CompletionFn

class CustomEval(evals.Eval):
    def eval_sample(self, sample, *args):
        prompt = sample["input"]
        expected = sample["ideal"]

        # Get model output
        result = self.completion_fn(
            prompt=prompt,
            temperature=0.0
        )

        # Custom scoring logic
        score = self.calculate_score(result, expected)

        return evals.record.record_match(
            correct=score > 0.8,
            expected=expected,
            picked=result
        )
```

---

## Key Metrics

### 1. **Accuracy-Based**

```python
# Exact Match
def exact_match(prediction, reference):
    return prediction.strip().lower() == reference.strip().lower()

# F1 Score (token overlap)
def f1_score(prediction, reference):
    pred_tokens = set(prediction.split())
    ref_tokens = set(reference.split())

    if len(pred_tokens) == 0 or len(ref_tokens) == 0:
        return 0

    precision = len(pred_tokens & ref_tokens) / len(pred_tokens)
    recall = len(pred_tokens & ref_tokens) / len(ref_tokens)

    if precision + recall == 0:
        return 0

    return 2 * (precision * recall) / (precision + recall)

# BLEU Score (n-gram overlap)
from nltk.translate.bleu_score import sentence_bleu

bleu = sentence_bleu([reference.split()], prediction.split())
```

### 2. **Semantic Similarity**

```python
from sentence_transformers import SentenceTransformer, util

model = SentenceTransformer('all-MiniLM-L6-v2')

def semantic_similarity(text1, text2):
    emb1 = model.encode(text1)
    emb2 = model.encode(text2)
    return util.cos_sim(emb1, emb2).item()

# Usage
score = semantic_similarity(
    "Paris is the capital of France",
    "The capital of France is Paris"
)
# 0.95 (very similar despite different wording)
```

### 3. **LLM-as-Judge**

```python
from openai import OpenAI

client = OpenAI()

def llm_judge(question, answer, criteria="accuracy and helpfulness"):
    prompt = f"""Evaluate this answer on {criteria}.
Question: {question}
Answer: {answer}

Provide:
1. Score (1-10)
2. Reasoning

Format:
Score: X
Reasoning: ...
"""

    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )

    # Parse score and reasoning
    output = response.choices[0].message.content
    score = extract_score(output)
    reasoning = extract_reasoning(output)

    return score, reasoning
```

### 4. **Safety Metrics**

```python
# Toxicity (using Detoxify)
from detoxify import Detoxify

model = Detoxify('original')

def toxicity_score(text):
    results = model.predict(text)
    return results['toxicity']

# PII Detection
import re

def contains_pii(text):
    patterns = {
        'email': r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b',
        'phone': r'\b\d{3}[-.]?\d{3}[-.]?\d{4}\b',
        'ssn': r'\b\d{3}-\d{2}-\d{4}\b',
    }

    for pii_type, pattern in patterns.items():
        if re.search(pattern, text):
            return True, pii_type

    return False, None
```

---

## CI/CD Integration

### GitHub Actions

```yaml
# .github/workflows/llm-tests.yml
name: LLM Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.9

    - name: Install dependencies
      run: |
        pip install deepeval pytest

    - name: Run LLM tests
      env:
        OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
      run: |
        pytest tests/test_llm.py

    - name: Upload results
      uses: actions/upload-artifact@v2
      with:
        name: test-results
        path: test-results/
```

### Pre-commit Hooks

```yaml
# .pre-commit-config.yaml
repos:
  - repo: local
    hooks:
      - id: llm-quality-check
        name: LLM Quality Check
        entry: python scripts/quality_check.py
        language: python
        pass_filenames: false
```

```python
# scripts/quality_check.py
import sys
from deepeval.metrics import HallucinationMetric

def check_prompt_quality(prompt_file):
    with open(prompt_file) as f:
        prompts = f.readlines()

    metric = HallucinationMetric()

    for prompt in prompts:
        # Test prompt for potential issues
        score = test_prompt(prompt, metric)
        if score < 0.8:
            print(f"⚠️  Low quality prompt detected: {prompt[:50]}...")
            sys.exit(1)

    print("✅ All prompts passed quality check")

if __name__ == "__main__":
    check_prompt_quality("prompts.txt")
```

---

## Regression Testing

### Dataset-Based Testing

```python
import pytest
from deepeval import assert_test
from deepeval.test_case import LLMTestCase
from deepeval.metrics import AnswerRelevancyMetric

# Load golden dataset
import pandas as pd
golden_dataset = pd.read_csv("golden_dataset.csv")

@pytest.mark.parametrize("row", golden_dataset.itertuples())
def test_against_golden_set(row):
    # Run your LLM
    actual_output = my_rag_pipeline(row.question)

    # Compare against golden answer
    test_case = LLMTestCase(
        input=row.question,
        actual_output=actual_output,
        expected_output=row.golden_answer,
        context=row.context
    )

    metric = AnswerRelevancyMetric(threshold=0.8)
    assert_test(test_case, [metric])
```

### Version Comparison

```python
# Compare model versions
def compare_versions(test_cases, model_v1, model_v2):
    results = []

    for test in test_cases:
        output_v1 = model_v1.generate(test.input)
        output_v2 = model_v2.generate(test.input)

        score_v1 = evaluate(output_v1, test.expected)
        score_v2 = evaluate(output_v2, test.expected)

        results.append({
            "test": test.input,
            "v1_score": score_v1,
            "v2_score": score_v2,
            "change": score_v2 - score_v1
        })

    # Flag regressions
    regressions = [r for r in results if r["change"] < -0.1]
    improvements = [r for r in results if r["change"] > 0.1]

    print(f"Regressions: {len(regressions)}")
    print(f"Improvements: {len(improvements)}")

    return results
```

---

## Benchmark Leaderboards

### Popular Benchmarks (2026)

| Benchmark | Focus | Tasks | Top Score | Model |
|-----------|-------|-------|-----------|-------|
| **MMLU** | Knowledge | 57 | 89.5% | GPT-4.5 |
| **BBH** | Reasoning | 23 | 92.3% | Claude Opus 4 |
| **HumanEval** | Coding | 164 | 96.2% | GPT-4.5 |
| **GSM8K** | Math | 8.5K | 98.1% | Gemini Ultra 2 |
| **TruthfulQA** | Truthfulness | 817 | 87.4% | Claude Opus 4 |
| **HellaSwag** | Commonsense | 10K | 95.6% | GPT-4.5 |

### Running Benchmarks

```python
from lm_eval import evaluator

# Comprehensive benchmark suite
benchmark_tasks = [
    "mmlu",
    "bbh",
    "hellaswag",
    "arc_challenge",
    "truthfulqa",
    "gsm8k"
]

results = evaluator.simple_evaluate(
    model="hf",
    model_args="pretrained=meta-llama/Llama-2-70b-hf",
    tasks=benchmark_tasks,
    num_fewshot=5
)

# Generate report
for task, metrics in results['results'].items():
    print(f"{task}: {metrics['acc']:.2%}")
```

---

## A/B Testing

### Statistical Significance

```python
from scipy import stats
import numpy as np

def ab_test(variant_a_scores, variant_b_scores, alpha=0.05):
    """
    H0: Both variants perform equally
    H1: Variants perform differently
    """
    # T-test
    t_stat, p_value = stats.ttest_ind(variant_a_scores, variant_b_scores)

    # Reject H0 if p < alpha
    significant = p_value < alpha

    # Effect size (Cohen's d)
    mean_diff = np.mean(variant_b_scores) - np.mean(variant_a_scores)
    pooled_std = np.sqrt((np.std(variant_a_scores)**2 + np.std(variant_b_scores)**2) / 2)
    cohens_d = mean_diff / pooled_std

    return {
        "p_value": p_value,
        "significant": significant,
        "effect_size": cohens_d,
        "winner": "B" if mean_diff > 0 else "A"
    }

# Usage
variant_a_scores = [0.82, 0.85, 0.79, 0.88, 0.83]  # Old model
variant_b_scores = [0.87, 0.90, 0.85, 0.91, 0.89]  # New model

result = ab_test(variant_a_scores, variant_b_scores)

if result["significant"]:
    print(f"✅ Variant {result['winner']} is significantly better")
    print(f"Effect size: {result['effect_size']:.3f}")
else:
    print("⚠️  No significant difference detected")
```

---

## Best Practices

### 1. **Diverse Test Sets**
```python
# Don't test on training distribution only
test_sets = {
    "in_distribution": normal_queries,
    "edge_cases": unusual_queries,
    "adversarial": tricky_queries,
    "multilingual": non_english_queries
}

for name, test_set in test_sets.items():
    score = evaluate(model, test_set)
    print(f"{name}: {score}")
```

### 2. **Human Evaluation**
```python
# LLM metrics aren't perfect - use human eval
import random

# Sample 100 random outputs for human review
sampled = random.sample(all_outputs, 100)

# Use tool like Argilla for annotation
import argilla as rg

dataset = rg.FeedbackDataset.from_huggingface("my-eval-set")
dataset.push_to_argilla("human-evaluation")

# Team annotates, then:
annotated = rg.load("human-evaluation")
human_accuracy = calculate_agreement(annotated)
```

### 3. **Continuous Monitoring**
```python
# Track metrics over time
from datetime import datetime

def log_daily_metrics():
    test_results = run_evaluation_suite()

    mlflow.log_metrics({
        "accuracy": test_results["accuracy"],
        "latency_p95": test_results["latency_p95"],
        "cost_per_query": test_results["cost"]
    }, step=datetime.now().timestamp())

# Run daily
schedule.every().day.at("02:00").do(log_daily_metrics)
```

---

## Related Resources

- [Datasets & Data Tools](datasets-data-tools.md) - Create test datasets
- [Observability](observability-monitoring.md) - Monitor in production
- [Production AI](production-ai.md) - Deploy tested models
- [RAG & Knowledge](rag-knowledge.md) - RAG-specific testing

---

[← Back to Home](../index.md) | [Next: RAG & Knowledge →](rag-knowledge.md)
