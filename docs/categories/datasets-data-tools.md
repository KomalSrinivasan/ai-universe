# 📦 Datasets & Data Tools

[← Back to Home](../index.md)

Tools for creating, managing, and curating datasets for LLM training, fine-tuning, and evaluation.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Selection Guide](#selection-guide)
- [Quick Start](#quick-start)

---

## Overview

Dataset tools enable:
- **Synthetic Data Generation**: Create training data with LLMs
- **Data Annotation**: Label and curate datasets
- **Dataset Management**: Version, store, and share datasets
- **Data Quality**: Cleaning, deduplication, filtering

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [argilla-io/argilla](https://github.com/argilla-io/argilla) | Collaboration platform for AI engineers and domain experts | ![GitHub stars](https://img.shields.io/github/stars/argilla-io/argilla?style=social) |
| [confident-ai/deepeval](https://github.com/confident-ai/deepeval) | LLM evaluation framework with synthetic data generation | ![GitHub stars](https://img.shields.io/github/stars/confident-ai/deepeval?style=social) |
| [gretelai/gretel-synthetics](https://github.com/gretelai/gretel-synthetics) | Generate synthetic datasets with privacy guarantees | ![GitHub stars](https://img.shields.io/github/stars/gretelai/gretel-synthetics?style=social) |
| [microsoft/promptbase](https://github.com/microsoft/promptbase) | Manage and version prompts and datasets | ![GitHub stars](https://img.shields.io/github/stars/microsoft/promptbase?style=social) |
| [huggingface/datasets](https://github.com/huggingface/datasets) | Fast, efficient dataset library for ML | ![GitHub stars](https://img.shields.io/github/stars/huggingface/datasets?style=social) |
| [cleanlab/cleanlab](https://github.com/cleanlab/cleanlab) | Find and fix label errors in datasets | ![GitHub stars](https://img.shields.io/github/stars/cleanlab/cleanlab?style=social) |
| [bytewax/bytewax](https://github.com/bytewax/bytewax) | Python stream processing for real-time data | ![GitHub stars](https://img.shields.io/github/stars/bytewax/bytewax?style=social) |

---

## Selection Guide

### By Use Case

**🏷️ Data Annotation**
- **Argilla** - Best UI, team collaboration
- **Label Studio** (not listed - proprietary focus)
- **Prodigy** (Spacy ecosystem)

**🤖 Synthetic Data**
- **DeepEval** - LLM-specific test cases
- **Gretel Synthetics** - Privacy-preserving
- **GPT-4/Claude** - Custom generation scripts

**📊 Dataset Management**
- **HuggingFace Datasets** - Largest ecosystem
- **PromptBase** - Prompt versioning
- **DVC** - Version control for data

**🔍 Data Quality**
- **Cleanlab** - Find label errors
- **Great Expectations** - Data validation
- **Argilla** - Human-in-the-loop curation

### By Team Size

**Solo Developer**
- **HuggingFace Datasets** - Ready-to-use
- **DeepEval** - Quick synthetic data
- **Cleanlab** - Automated quality

**Small Team (2-10)**
- **Argilla** - Collaborative annotation
- **PromptBase** - Shared prompts
- **Gretel** - Synthetic data at scale

**Enterprise**
- **Argilla Enterprise** - Advanced features
- **HuggingFace Hub** - Private datasets
- **Custom infrastructure** - Full control

---

## Quick Start

### Argilla - Annotation Platform

```bash
# Install
pip install argilla

# Run server (Docker)
docker run -d --name argilla -p 6900:6900 argilla/argilla-quickstart:latest

# Or use cloud: https://argilla.io
```

```python
import argilla as rg

# Initialize
rg.init(api_url="http://localhost:6900", api_key="admin.apikey")

# Create dataset for text classification
dataset = rg.FeedbackDataset(
    fields=[
        rg.TextField(name="text"),
    ],
    questions=[
        rg.LabelQuestion(
            name="sentiment",
            labels=["positive", "negative", "neutral"]
        ),
    ]
)

# Add records
dataset.add_records([
    rg.FeedbackRecord(
        fields={"text": "This product is amazing!"}
    ),
    rg.FeedbackRecord(
        fields={"text": "Terrible experience."}
    )
])

# Push to Argilla
dataset.push_to_argilla("sentiment-analysis")

# Team annotates via UI
# Then retrieve annotated data
annotated = rg.load("sentiment-analysis")
```

### DeepEval - Synthetic Test Data

```bash
# Install
pip install deepeval
```

```python
from deepeval.synthesizer import Synthesizer
from deepeval.dataset import Golden

# Initialize
synthesizer = Synthesizer(
    model="gpt-4"
)

# Generate synthetic test cases
goldens = synthesizer.generate_goldens_from_docs(
    document_paths=["./docs"],
    num_goldens=50,
    include_expected_output=True
)

# Each golden contains:
# - input: Test question
# - expected_output: Ground truth answer
# - context: Source document chunks

# Use for evaluation
from deepeval.metrics import AnswerRelevancy

metric = AnswerRelevancy()
for golden in goldens:
    score = metric.measure(
        output=model_response,
        expected_output=golden.expected_output
    )
```

### Gretel Synthetics - Privacy-Safe Data

```bash
# Install
pip install gretel-synthetics
```

```python
from gretel_synthetics.batch import DataFrameBatch
import pandas as pd

# Load sensitive data
df = pd.read_csv("customer_data.csv")

# Configure synthetic model
config = {
    "epochs": 100,
    "learning_rate": 0.001,
    "vocab_size": 20000,
    "privacy_filters": True,  # Remove PII
    "differential_privacy": {
        "enabled": True,
        "epsilon": 8.0  # Privacy budget
    }
}

# Train and generate
batch = DataFrameBatch(df, config)
batch.train()

# Generate synthetic data
synthetic_df = batch.generate(num_records=10000)

# Synthetic data:
# - Maintains statistical properties
# - Removes PII
# - Differential privacy guarantees
```

### HuggingFace Datasets

```python
from datasets import load_dataset, Dataset

# Load popular datasets
squad = load_dataset("squad")
glue = load_dataset("glue", "mrpc")

# Load your own
dataset = Dataset.from_dict({
    "text": ["Example 1", "Example 2"],
    "label": [0, 1]
})

# Preprocess
def tokenize(examples):
    return tokenizer(examples["text"], padding=True, truncation=True)

tokenized = dataset.map(tokenize, batched=True)

# Save and share
dataset.push_to_hub("username/dataset-name")

# Version control
dataset.save_to_disk("./my_dataset_v1")
```

### Cleanlab - Find Label Errors

```python
from cleanlab.classification import CleanLearning
from sklearn.linear_model import LogisticRegression

# Your noisy labeled data
X_train, y_train = load_data()

# Train with automatic error detection
clf = CleanLearning(LogisticRegression())
clf.fit(X_train, y_train)

# Find label errors
label_errors = clf.get_label_issues()

# Review and fix
for idx in label_errors:
    print(f"Sample {idx}:")
    print(f"  Data: {X_train[idx]}")
    print(f"  Given label: {y_train[idx]}")
    print(f"  Suggested: {clf.predict([X_train[idx]])[0]}")

# For LLMs - use embeddings
from sentence_transformers import SentenceTransformer

model = SentenceTransformer('all-MiniLM-L6-v2')
embeddings = model.encode(texts)

clf = CleanLearning(LogisticRegression())
clf.fit(embeddings, labels)
errors = clf.get_label_issues()
```

---

## Synthetic Data Generation Patterns

### 1. **Question-Answer Pairs**

```python
from openai import OpenAI

client = OpenAI()

def generate_qa_pairs(document, num_pairs=10):
    prompt = f"""Generate {num_pairs} question-answer pairs from this document:

{document}

Format:
Q: <question>
A: <answer>
"""

    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )

    # Parse and structure
    qa_pairs = parse_qa_response(response.choices[0].message.content)
    return qa_pairs

# Use for RAG evaluation
qa_dataset = []
for doc in documents:
    qa_dataset.extend(generate_qa_pairs(doc))
```

### 2. **Few-Shot Examples**

```python
def generate_training_examples(task_description, seed_examples, num_examples=100):
    prompt = f"""Task: {task_description}

Examples:
{format_examples(seed_examples)}

Generate {num_examples} more examples following the same pattern."""

    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}],
        temperature=0.8  # Higher for diversity
    )

    return parse_examples(response.choices[0].message.content)

# Example: Sentiment analysis
examples = generate_training_examples(
    task_description="Classify sentiment as positive, negative, or neutral",
    seed_examples=[
        {"text": "I love this!", "label": "positive"},
        {"text": "This is terrible", "label": "negative"},
    ],
    num_examples=1000
)
```

### 3. **Data Augmentation**

```python
def augment_text(text, methods=["paraphrase", "backtranslation"]):
    augmented = []

    if "paraphrase" in methods:
        prompt = f"Paraphrase this 5 different ways:\n{text}"
        response = client.chat.completions.create(
            model="gpt-3.5-turbo",
            messages=[{"role": "user", "content": prompt}]
        )
        augmented.extend(parse_paraphrases(response.choices[0].message.content))

    if "backtranslation" in methods:
        # Translate to French and back to English
        french = translate(text, "fr")
        english = translate(french, "en")
        augmented.append(english)

    return augmented

# Expand small dataset
expanded_dataset = []
for text, label in original_dataset:
    expanded_dataset.append((text, label))
    for aug_text in augment_text(text):
        expanded_dataset.append((aug_text, label))
```

### 4. **Adversarial Examples**

```python
def generate_adversarial(text, label, model):
    prompt = f"""Generate text that:
1. Should be labeled as: {label}
2. But is likely to fool this classifier: {model.description}
3. Is similar to: {text}

Generate 5 challenging examples."""

    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )

    return parse_examples(response.choices[0].message.content)

# Use to find model weaknesses
adversarial_set = []
for text, label in test_set:
    adversarial_set.extend(generate_adversarial(text, label, classifier))
```

---

## Popular Public Datasets

### LLM Training & Fine-Tuning

| Dataset | Description | Size | License |
|---------|-------------|------|---------|
| **C4** | Common Crawl cleaned | 750GB | ODC-BY |
| **The Pile** | Diverse text dataset | 825GB | MIT |
| **RedPajama** | LLaMA recreation | 1.2TB | Apache 2.0 |
| **ROOTS** | Multilingual (59 langs) | 1.6TB | Various |
| **Dolma** | Open pre-training corpus | 3TB | ODC-BY |

### Instruction Tuning

| Dataset | Examples | Type | License |
|---------|----------|------|---------|
| **Alpaca** | 52K | Instruction-following | CC BY-NC 4.0 |
| **ShareGPT** | 90K | Conversations | Non-commercial |
| **FLAN** | 1.8M | Multi-task | Apache 2.0 |
| **OpenOrca** | 4.2M | GPT-4 augmented | MIT |
| **UltraChat** | 1.5M | Multi-turn dialogues | MIT |

### Evaluation

| Benchmark | Tasks | Focus | Link |
|-----------|-------|-------|------|
| **MMLU** | 57 | Knowledge | HF: hendrycks/mmlu |
| **BBH** | 23 | Reasoning | HF: lukaemon/bbh |
| **TruthfulQA** | 817 | Truthfulness | HF: truthful_qa |
| **HumanEval** | 164 | Coding | HF: openai_humaneval |
| **GSM8K** | 8.5K | Math | HF: gsm8k |

### RAG & Knowledge

| Dataset | Documents | Domain | Link |
|---------|-----------|--------|------|
| **Wikipedia** | 6.4M | General | HF: wikipedia |
| **arXiv** | 2.3M | Academic | Kaggle |
| **PubMed** | 35M | Medical | NIH |
| **GitHub Code** | 115M | Programming | Google BigQuery |

---

## Data Quality Checklist

### 1. **Deduplication**
```python
from datasets import load_dataset

dataset = load_dataset("your_dataset")

# Exact duplicates
deduplicated = dataset.unique("text")

# Near duplicates (using MinHash)
from datasketch import MinHash, MinHashLSH

lsh = MinHashLSH(threshold=0.9, num_perm=128)
# ... implement near-duplicate detection
```

### 2. **PII Removal**
```python
import presidio_analyzer
import presidio_anonymizer

analyzer = presidio_analyzer.AnalyzerEngine()
anonymizer = presidio_anonymizer.AnonymizerEngine()

def remove_pii(text):
    results = analyzer.analyze(text, language='en')
    anonymized = anonymizer.anonymize(text, results)
    return anonymized.text

# Apply to dataset
dataset = dataset.map(lambda x: {"text": remove_pii(x["text"])})
```

### 3. **Quality Filtering**
```python
def quality_filter(example):
    text = example["text"]

    # Minimum length
    if len(text) < 100:
        return False

    # Language detection
    if detect_language(text) != "en":
        return False

    # No excessive repetition
    if has_repetition(text, threshold=0.3):
        return False

    # Toxicity check
    if is_toxic(text):
        return False

    return True

filtered_dataset = dataset.filter(quality_filter)
```

### 4. **Balance Check**
```python
from collections import Counter

# Check label distribution
label_counts = Counter(dataset["label"])
print(label_counts)

# Rebalance if needed
from imblearn.over_sampling import SMOTE

# For classification datasets
X_resampled, y_resampled = SMOTE().fit_resample(X, y)
```

---

## Dataset Versioning

### DVC (Data Version Control)

```bash
# Install
pip install dvc

# Initialize
dvc init

# Track dataset
dvc add data/training_set.csv

# Commit
git add data/training_set.csv.dvc .gitignore
git commit -m "Add training dataset v1"

# Store remotely
dvc remote add -d storage s3://mybucket/dvc-storage
dvc push

# Later: Retrieve specific version
git checkout v1.0
dvc pull
```

### HuggingFace Hub Versioning

```python
from datasets import load_dataset

# Upload with version tag
dataset.push_to_hub(
    "username/dataset-name",
    commit_message="v2.0: Added 10k examples",
    revision="v2.0"
)

# Load specific version
dataset_v1 = load_dataset("username/dataset-name", revision="v1.0")
dataset_v2 = load_dataset("username/dataset-name", revision="v2.0")
```

---

## Annotation Workflows

### Active Learning with Argilla

```python
import argilla as rg
from transformers import pipeline

# Initial model
classifier = pipeline("text-classification", model="distilbert-base")

# Predict on unlabeled pool
predictions = []
for text in unlabeled_pool:
    pred = classifier(text)[0]
    predictions.append({
        "text": text,
        "prediction": pred["label"],
        "confidence": pred["score"]
    })

# Send low-confidence samples to Argilla
uncertain = [p for p in predictions if p["confidence"] < 0.6]

dataset = rg.FeedbackDataset.from_argilla("annotation-queue")
dataset.add_records([
    rg.FeedbackRecord(fields={"text": item["text"]})
    for item in uncertain
])
dataset.push_to_argilla("annotation-queue")

# Humans annotate uncertain cases
# Then retrain model with new labels
```

---

## Cost Optimization

### Synthetic Data vs Human Annotation

| Method | Cost per Example | Quality | Scale |
|--------|------------------|---------|-------|
| GPT-4 Generation | $0.02 | Good | Unlimited |
| GPT-3.5 Generation | $0.001 | Moderate | Unlimited |
| Expert Annotation | $5-$20 | Excellent | Limited |
| Crowd Annotation | $0.10-$0.50 | Variable | High |
| Hybrid (Synthetic + Review) | $0.20 | Very Good | High |

**Recommendation**: Generate with GPT-4, review with humans (10% sample)

---

## Best Practices

### 1. **Diverse Data Sources**
```python
# Mix multiple sources
combined = concatenate_datasets([
    web_crawl,
    books,
    academic_papers,
    conversations,
    code_repos
])
```

### 2. **Held-Out Test Sets**
```python
# Never train on test data!
train_test_split = dataset.train_test_split(test_size=0.1, seed=42)
train = train_test_split["train"]
test = train_test_split["test"]

# Save test set separately
test.save_to_disk("./test_set_final")
# Never modify after creation!
```

### 3. **Document Everything**
```yaml
# dataset_card.yaml
dataset_name: "My Dataset"
version: "1.0.0"
creation_date: "2026-04-17"
size: "100k examples"
languages: ["en"]
license: "MIT"
sources:
  - "Web crawl (30%)"
  - "Synthetic GPT-4 (50%)"
  - "Human annotations (20%)"
preprocessing:
  - "Deduplication"
  - "PII removal"
  - "Quality filtering"
splits:
  train: 80000
  validation: 10000
  test: 10000
```

---

## Related Resources

- [Evaluation & Testing](evaluation-testing.md) - Test with your datasets
- [Observability](observability-monitoring.md) - Monitor data quality
- [Agents & Orchestration](agents-orchestration.md) - Automate data pipelines
- [Production AI](production-ai.md) - Deploy data pipelines

---

[← Back to Home](../index.md) | [Next: Deployment & Serving →](deployment-serving.md)
