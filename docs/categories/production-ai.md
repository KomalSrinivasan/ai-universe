# 🏭 Production AI

[← Back to Home](../index.md)

Production orchestration, workflow management, and enterprise AI platforms.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Selection Guide](#selection-guide)
- [Quick Start](#quick-start)

---

## Overview

Production AI tools provide:
- **Workflow Orchestration**: ML pipelines and DAGs
- **Feature Stores**: Centralized feature management
- **Model Registry**: Version and deploy models
- **Distributed Computing**: Scale ML workloads

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [ray-project/ray](https://github.com/ray-project/ray) | Distributed computing for AI/ML at scale | ![GitHub stars](https://img.shields.io/github/stars/ray-project/ray?style=social) |
| [prefecthq/prefect](https://github.com/prefecthq/prefect) | Modern workflow orchestration for data pipelines | ![GitHub stars](https://img.shields.io/github/stars/prefecthq/prefect?style=social) |
| [feast-dev/feast](https://github.com/feast-dev/feast) | Feature store for production ML | ![GitHub stars](https://img.shields.io/github/stars/feast-dev/feast?style=social) |
| [mlflow/mlflow](https://github.com/mlflow/mlflow) | Open source platform for ML lifecycle | ![GitHub stars](https://img.shields.io/github/stars/mlflow/mlflow?style=social) |
| [zenml-io/zenml](https://github.com/zenml-io/zenml) | MLOps framework to create reproducible pipelines | ![GitHub stars](https://img.shields.io/github/stars/zenml-io/zenml?style=social) |
| [kedro-org/kedro](https://github.com/kedro-org/kedro) | Production-ready data science framework | ![GitHub stars](https://img.shields.io/github/stars/kedro-org/kedro?style=social) |
| [metaflow/metaflow](https://github.com/Netflix/metaflow) | Build and manage data science projects (Netflix) | ![GitHub stars](https://img.shields.io/github/stars/Netflix/metaflow?style=social) |

---

## Selection Guide

### By Use Case

**🔄 Workflow Orchestration**
- **Prefect** - Modern, Python-first, cloud-native
- **Airflow** - Battle-tested, largest ecosystem
- **Metaflow** - Data science focused (Netflix)
- **Kedro** - Best practices built-in

**⚡ Distributed Computing**
- **Ray** - Best for AI/ML workloads
- **Dask** - Pandas/NumPy at scale
- **Spark** - Big data processing

**📊 Feature Management**
- **Feast** - Most popular, open-source
- **Tecton** - Managed, enterprise
- **Hopsworks** - End-to-end ML platform

**📦 Model Registry**
- **MLflow** - Simple, widely adopted
- **ZenML** - Pipeline-centric
- **Weights & Biases** - Experiment tracking++

### By Team Size

**Solo Developer**
- **MLflow** - Local tracking
- **Prefect** - Simple workflows
- **Ray** - Local parallelization

**Small Team (2-10)**
- **Prefect Cloud** - Managed orchestration
- **Feast** - Shared features
- **ZenML** - Collaborative pipelines

**Enterprise**
- **Ray Clusters** - Massive scale
- **Prefect Enterprise** - Advanced governance
- **Feast + Data Warehouse** - Production features

---

## Quick Start

### Ray - Distributed Computing

```bash
# Install
pip install ray[default]
```

```python
import ray

# Initialize
ray.init()

# Parallelize function
@ray.remote
def process_batch(batch):
    # Heavy computation
    return expensive_model.predict(batch)

# Run in parallel across cluster
futures = [process_batch.remote(batch) for batch in batches]
results = ray.get(futures)

# Ray automatically:
# - Distributes tasks
# - Handles failures
# - Manages resources
```

**Ray Serve - Model Serving:**
```python
from ray import serve
import ray

ray.init()
serve.start()

@serve.deployment
class LLMModel:
    def __init__(self):
        self.model = load_model("llama-2-7b")

    def __call__(self, request):
        prompt = request.query_params["prompt"]
        return self.model.generate(prompt)

LLMModel.deploy()

# Access at http://localhost:8000
```

**Ray Train - Distributed Training:**
```python
from ray.train.torch import TorchTrainer
from ray.air.config import ScalingConfig

def train_func():
    # Your PyTorch training code
    model = create_model()
    for epoch in range(10):
        train_epoch(model)

trainer = TorchTrainer(
    train_func,
    scaling_config=ScalingConfig(
        num_workers=4,  # 4 GPUs
        use_gpu=True
    )
)

trainer.fit()
```

### Prefect - Workflow Orchestration

```bash
# Install
pip install prefect
```

```python
from prefect import flow, task
from prefect.deployments import Deployment

@task
def extract_data():
    # Pull data from API
    return data

@task
def transform_data(data):
    # Clean and process
    return processed_data

@task
def load_to_database(data):
    # Store in database
    db.insert(data)

@flow
def etl_pipeline():
    data = extract_data()
    processed = transform_data(data)
    load_to_database(processed)

# Run locally
etl_pipeline()

# Deploy to Prefect Cloud
deployment = Deployment.build_from_flow(
    flow=etl_pipeline,
    name="daily-etl",
    schedule="0 0 * * *"  # Daily at midnight
)
deployment.apply()
```

**Error Handling:**
```python
from prefect import flow, task
from prefect.tasks import exponential_backoff

@task(retries=3, retry_delay_seconds=exponential_backoff(backoff_factor=2))
def unreliable_api_call():
    # Will retry with delays: 2s, 4s, 8s
    return api.fetch_data()

@flow
def robust_pipeline():
    try:
        data = unreliable_api_call()
    except Exception as e:
        # Fallback logic
        send_alert(e)
        data = load_cached_data()
    return process(data)
```

### Feast - Feature Store

```bash
# Install
pip install feast
```

**Define Features:**
```python
# feature_repo/features.py
from feast import Entity, FeatureView, Field, FileSource
from feast.types import Float32, Int64
from datetime import timedelta

# Define entity
user = Entity(name="user", join_keys=["user_id"])

# Define data source
user_features_source = FileSource(
    path="data/user_features.parquet",
    timestamp_field="event_timestamp"
)

# Define feature view
user_features = FeatureView(
    name="user_features",
    entities=[user],
    ttl=timedelta(days=1),
    schema=[
        Field(name="age", dtype=Int64),
        Field(name="lifetime_value", dtype=Float32),
        Field(name="embedding", dtype=Float32),
    ],
    source=user_features_source
)
```

**Use Features:**
```python
from feast import FeatureStore
import pandas as pd

# Initialize
store = FeatureStore(repo_path=".")

# Get online features (low latency)
features = store.get_online_features(
    features=["user_features:age", "user_features:lifetime_value"],
    entity_rows=[{"user_id": 1001}, {"user_id": 1002}]
).to_dict()

# Get historical features (training)
entity_df = pd.DataFrame({
    "user_id": [1001, 1002, 1003],
    "event_timestamp": ["2026-01-01", "2026-01-02", "2026-01-03"]
})

training_data = store.get_historical_features(
    entity_df=entity_df,
    features=["user_features:age", "user_features:lifetime_value"]
).to_df()
```

### MLflow - Experiment Tracking

```bash
# Install
pip install mlflow
```

```python
import mlflow
from sklearn.ensemble import RandomForestClassifier

# Start tracking
mlflow.set_experiment("my-experiment")

with mlflow.start_run():
    # Log parameters
    mlflow.log_param("n_estimators", 100)
    mlflow.log_param("max_depth", 5)

    # Train model
    model = RandomForestClassifier(n_estimators=100, max_depth=5)
    model.fit(X_train, y_train)

    # Log metrics
    accuracy = model.score(X_test, y_test)
    mlflow.log_metric("accuracy", accuracy)

    # Log model
    mlflow.sklearn.log_model(model, "model")

# View UI
# mlflow ui
# http://localhost:5000
```

**Model Registry:**
```python
# Register model
mlflow.register_model(
    model_uri="runs:/abc123/model",
    name="production-classifier"
)

# Promote to production
client = mlflow.tracking.MlflowClient()
client.transition_model_version_stage(
    name="production-classifier",
    version=3,
    stage="Production"
)

# Load in production
model = mlflow.pyfunc.load_model(
    model_uri="models:/production-classifier/Production"
)
predictions = model.predict(data)
```

### ZenML - MLOps Pipelines

```bash
# Install
pip install zenml
zenml init
```

```python
from zenml import pipeline, step
from zenml.integrations.mlflow.mlflow_utils import get_tracking_uri

@step
def load_data() -> pd.DataFrame:
    return pd.read_csv("data.csv")

@step
def train_model(data: pd.DataFrame) -> Any:
    model = train(data)
    return model

@step
def evaluate_model(model: Any, data: pd.DataFrame) -> float:
    return model.score(data)

@pipeline
def ml_pipeline():
    data = load_data()
    model = train_model(data)
    accuracy = evaluate_model(model, data)

# Run pipeline
ml_pipeline()

# Deploy to cloud
from zenml.integrations.gcp.orchestrators import VertexOrchestrator

orchestrator = VertexOrchestrator(
    project="my-gcp-project",
    location="us-central1"
)

ml_pipeline.run(orchestrator=orchestrator)
```

---

## Production Patterns

### 1. **Feature Pipeline (Feast + Ray)**

```python
import ray
from feast import FeatureStore

@ray.remote
def compute_user_features(user_batch):
    # Heavy computation
    features = calculate_embeddings(user_batch)
    return features

# Distributed feature computation
user_batches = chunk_users(all_users, batch_size=1000)
feature_futures = [compute_user_features.remote(batch) for batch in user_batches]
all_features = ray.get(feature_futures)

# Write to Feast
store = FeatureStore()
store.write_to_online_store("user_features", all_features)
```

### 2. **Model Training Pipeline (Prefect + MLflow)**

```python
from prefect import flow, task
import mlflow

@task
def prepare_data():
    return load_and_clean_data()

@task
def train_model(data):
    with mlflow.start_run():
        model = train(data)
        mlflow.log_metric("accuracy", evaluate(model))
        mlflow.sklearn.log_model(model, "model")
        return mlflow.active_run().info.run_id

@task
def deploy_model(run_id):
    mlflow.register_model(f"runs:/{run_id}/model", "production-model")

@flow(name="training-pipeline")
def ml_training_pipeline():
    data = prepare_data()
    run_id = train_model(data)
    deploy_model(run_id)

# Schedule daily
from prefect.deployments import Deployment

deployment = Deployment.build_from_flow(
    flow=ml_training_pipeline,
    name="daily-training",
    schedule="0 2 * * *"  # 2 AM daily
)
```

### 3. **Inference Pipeline (Ray Serve + Feast)**

```python
from ray import serve
from feast import FeatureStore

@serve.deployment
class PredictionService:
    def __init__(self):
        self.model = mlflow.pyfunc.load_model("models:/production-model/latest")
        self.feature_store = FeatureStore()

    async def __call__(self, user_id: int):
        # Get real-time features
        features = self.feature_store.get_online_features(
            features=["user_features:age", "user_features:ltv"],
            entity_rows=[{"user_id": user_id}]
        ).to_dict()

        # Predict
        prediction = self.model.predict(features)
        return {"user_id": user_id, "prediction": float(prediction[0])}

PredictionService.deploy()
```

### 4. **A/B Testing Pipeline**

```python
from prefect import flow, task
import mlflow

@task
def train_variant_a(data):
    with mlflow.start_run(run_name="variant-a"):
        model = train_with_hyperparams_a(data)
        mlflow.log_model(model, "model")
        return mlflow.active_run().info.run_id

@task
def train_variant_b(data):
    with mlflow.start_run(run_name="variant-b"):
        model = train_with_hyperparams_b(data)
        mlflow.log_model(model, "model")
        return mlflow.active_run().info.run_id

@task
def deploy_ab_test(run_a, run_b):
    # Deploy both models
    deploy_with_traffic_split(
        variant_a=run_a,
        variant_b=run_b,
        split={"a": 0.5, "b": 0.5}
    )

@flow
def ab_test_pipeline(data):
    run_a = train_variant_a(data)
    run_b = train_variant_b(data)
    deploy_ab_test(run_a, run_b)
```

---

## Monitoring Production Models

### 1. **Data Drift Detection**

```python
from evidently.report import Report
from evidently.metric_preset import DataDriftPreset

# Compare reference vs current data
report = Report(metrics=[DataDriftPreset()])
report.run(reference_data=train_data, current_data=production_data)

if report.as_dict()["metrics"][0]["result"]["dataset_drift"]:
    alert("Data drift detected - consider retraining")
    trigger_retraining_pipeline()
```

### 2. **Model Performance Tracking**

```python
import mlflow

# Log production metrics
with mlflow.start_run(run_name="production-monitoring"):
    daily_accuracy = calculate_accuracy(predictions, ground_truth)
    mlflow.log_metric("production_accuracy", daily_accuracy)

    # Alert if degradation
    if daily_accuracy < THRESHOLD:
        alert(f"Model accuracy dropped to {daily_accuracy}")
```

### 3. **Feature Freshness**

```python
from feast import FeatureStore

store = FeatureStore()

# Check feature freshness
feature_stats = store.get_feature_statistics("user_features")

for feature, stats in feature_stats.items():
    age_hours = (datetime.now() - stats["last_updated"]).hours

    if age_hours > 24:
        alert(f"Feature {feature} is {age_hours}h old")
```

---

## Scaling Strategies

### 1. **Horizontal Scaling (Ray)**

```python
# Local cluster
ray.init()

# Cloud cluster
ray.init(address="ray://my-cluster:10001")

# Auto-scaling cluster (KubeRay)
# Automatically scales from 1 to 100 nodes based on load
```

### 2. **Caching**

```python
from prefect import task
from prefect.tasks import task_input_hash
from datetime import timedelta

@task(cache_key_fn=task_input_hash, cache_expiration=timedelta(hours=1))
def expensive_computation(x):
    # Cached for 1 hour
    return heavy_processing(x)
```

### 3. **Batch Processing**

```python
# Don't: Process one at a time
for user in users:
    features = get_features(user)
    predict(features)

# Do: Batch processing
batches = chunk(users, batch_size=1000)
for batch in batches:
    features = get_features_batch(batch)
    predictions = predict_batch(features)
```

---

## Cost Optimization

### 1. **Spot Instances**

```python
# Ray on spot instances
from ray.autoscaler.sdk import configure_cluster

config = {
    "cluster_name": "my-cluster",
    "provider": {
        "type": "aws",
        "use_spot": True,  # 70% cost savings
        "spot_max_price": "auto"
    }
}
```

### 2. **Feature Reuse**

```python
# Feast materializes features to low-latency store
# Compute once, use many times

# Expensive: Compute embeddings for every prediction
embedding = embed_text(user.bio)  # 100ms

# Cheap: Precompute and store in Feast
embedding = feature_store.get("user_embedding", user_id)  # <1ms
```

### 3. **Smart Scheduling**

```python
# Run expensive jobs during off-peak hours
@flow
def expensive_pipeline():
    # Heavy training job

deployment = Deployment.build_from_flow(
    flow=expensive_pipeline,
    schedule="0 2 * * *"  # 2 AM when usage is low
)
```

---

## Best Practices

### 1. **Reproducibility**

```python
# MLflow tracks everything
with mlflow.start_run():
    mlflow.log_param("random_seed", 42)
    mlflow.log_param("library_version", sklearn.__version__)
    mlflow.log_artifact("config.yaml")
    mlflow.log_code("src/")  # Log entire codebase
```

### 2. **Testing Pipelines**

```python
import pytest
from prefect import flow

@flow
def data_pipeline():
    data = extract()
    assert data is not None, "Extraction failed"
    assert len(data) > 0, "No data extracted"

    processed = transform(data)
    assert processed.schema == EXPECTED_SCHEMA

    load(processed)

def test_pipeline():
    # Test with small data
    result = data_pipeline()
    assert result.success
```

### 3. **Gradual Rollouts**

```python
# Start with 5% traffic
deploy_model(model, traffic_percentage=0.05)

# Monitor for 24h
if no_errors_detected():
    # Increase to 50%
    update_traffic(0.5)

# Finally 100%
if still_healthy():
    update_traffic(1.0)
```

---

## Related Resources

- [Deployment & Serving](deployment-serving.md) - Model serving platforms
- [Observability](observability-monitoring.md) - Monitor production systems
- [Infrastructure](infrastructure.md) - Training infrastructure
- [Evaluation & Testing](evaluation-testing.md) - Test before deployment

---

[← Back to Home](../index.md) | [Next: Evaluation & Testing →](evaluation-testing.md)
