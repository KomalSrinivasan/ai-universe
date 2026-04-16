# 🗄️ Vector Databases

[← Back to Home](../index.md)

High-performance vector databases for embeddings, semantic search, and RAG applications.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Selection Guide](#selection-guide)
- [Quick Start](#quick-start)

---

## Overview

Vector databases store and query high-dimensional embeddings for:
- **Semantic Search**: Find similar content by meaning
- **RAG (Retrieval Augmented Generation)**: Provide context to LLMs
- **Recommendation Systems**: Similar item discovery
- **Anomaly Detection**: Identify outliers

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | Cloud-native vector database for billion-scale data | ![GitHub stars](https://img.shields.io/github/stars/milvus-io/milvus?style=social) |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | High-performance vector search engine with filters | ![GitHub stars](https://img.shields.io/github/stars/qdrant/qdrant?style=social) |
| [weaviate/weaviate](https://github.com/weaviate/weaviate) | AI-native vector database with GraphQL | ![GitHub stars](https://img.shields.io/github/stars/weaviate/weaviate?style=social) |
| [chroma-core/chroma](https://github.com/chroma-core/chroma) | Embedding database for LLM applications | ![GitHub stars](https://img.shields.io/github/stars/chroma-core/chroma?style=social) |
| [pinecone-io/pinecone-python-client](https://github.com/pinecone-io/pinecone-python-client) | Python client for Pinecone (managed service) | ![GitHub stars](https://img.shields.io/github/stars/pinecone-io/pinecone-python-client?style=social) |
| [pgvector/pgvector](https://github.com/pgvector/pgvector) | Vector similarity search for PostgreSQL | ![GitHub stars](https://img.shields.io/github/stars/pgvector/pgvector?style=social) |
| [facebookresearch/faiss](https://github.com/facebookresearch/faiss) | Efficient similarity search library from Meta | ![GitHub stars](https://img.shields.io/github/stars/facebookresearch/faiss?style=social) |
| [vespa-engine/vespa](https://github.com/vespa-engine/vespa) | Big data serving engine with vector search | ![GitHub stars](https://img.shields.io/github/stars/vespa-engine/vespa?style=social) |

---

## Selection Guide

### By Use Case

**🚀 Production RAG at Scale**
- **Milvus** - Billion+ vectors, high throughput
- **Qdrant** - Advanced filtering, low latency
- **Weaviate** - Hybrid search (vector + keyword)
- **Pinecone** - Fully managed, zero ops

**💻 Development & Prototyping**
- **Chroma** - Simplest API, fastest setup
- **pgvector** - If already using PostgreSQL
- **FAISS** - Local experimentation

**💼 Enterprise Requirements**
- **Milvus** - Kubernetes-native, scalable
- **Qdrant** - Rust performance, security
- **Weaviate** - GraphQL API, modules
- **Vespa** - Complex queries, mature

**💰 Cost-Conscious**
- **Chroma** - Free, embeddable
- **pgvector** - Use existing Postgres
- **FAISS** - Free library
- **Qdrant** - Self-host option

### By Scale

**Small (<1M vectors)**
- Chroma, pgvector, FAISS

**Medium (1M-100M vectors)**
- Qdrant, Weaviate, Milvus

**Large (100M-1B+ vectors)**
- Milvus, Pinecone, Vespa

---

## Quick Start

### Chroma - Simplest Setup

```bash
# Install
pip install chromadb
```

```python
import chromadb

# Initialize
client = chromadb.Client()

# Create collection
collection = client.create_collection("documents")

# Add documents
collection.add(
    documents=["This is document 1", "This is document 2"],
    ids=["id1", "id2"]
)

# Query
results = collection.query(
    query_texts=["search query"],
    n_results=2
)

print(results)
```

### Qdrant - High Performance

```bash
# Using Docker
docker run -p 6333:6333 qdrant/qdrant

# Or install
pip install qdrant-client
```

```python
from qdrant_client import QdrantClient
from qdrant_client.models import Distance, VectorParams, PointStruct

# Connect
client = QdrantClient("localhost", port=6333)

# Create collection
client.create_collection(
    collection_name="documents",
    vectors_config=VectorParams(size=384, distance=Distance.COSINE),
)

# Insert vectors
client.upsert(
    collection_name="documents",
    points=[
        PointStruct(
            id=1,
            vector=[0.1, 0.2, ...],  # 384 dimensions
            payload={"text": "Document content"}
        )
    ]
)

# Search
results = client.search(
    collection_name="documents",
    query_vector=[0.1, 0.2, ...],
    limit=5
)
```

### Milvus - Scalable Production

```bash
# Docker Compose
wget https://github.com/milvus-io/milvus/releases/download/v2.3.0/milvus-standalone-docker-compose.yml -O docker-compose.yml
docker-compose up -d

# Install client
pip install pymilvus
```

```python
from pymilvus import connections, Collection, FieldSchema, CollectionSchema, DataType

# Connect
connections.connect("default", host="localhost", port="19530")

# Define schema
fields = [
    FieldSchema(name="id", dtype=DataType.INT64, is_primary=True),
    FieldSchema(name="embedding", dtype=DataType.FLOAT_VECTOR, dim=768),
    FieldSchema(name="text", dtype=DataType.VARCHAR, max_length=65535)
]
schema = CollectionSchema(fields)

# Create collection
collection = Collection("documents", schema)

# Insert
data = [
    [1, 2, 3],  # IDs
    [[0.1]*768, [0.2]*768, [0.3]*768],  # Embeddings
    ["text1", "text2", "text3"]  # Metadata
]
collection.insert(data)

# Create index
collection.create_index(
    field_name="embedding",
    index_params={"index_type": "IVF_FLAT", "metric_type": "L2", "params": {"nlist": 128}}
)
collection.load()

# Search
results = collection.search(
    data=[[0.1]*768],
    anns_field="embedding",
    param={"metric_type": "L2", "params": {"nprobe": 10}},
    limit=5
)
```

### pgvector - PostgreSQL Extension

```sql
-- Install extension
CREATE EXTENSION vector;

-- Create table
CREATE TABLE documents (
  id bigserial PRIMARY KEY,
  content text,
  embedding vector(1536)  -- OpenAI ada-002 dimension
);

-- Insert
INSERT INTO documents (content, embedding) VALUES
('Document 1', '[0.1, 0.2, ...]'),
('Document 2', '[0.3, 0.4, ...]');

-- Create index
CREATE INDEX ON documents USING ivfflat (embedding vector_cosine_ops) WITH (lists = 100);

-- Search
SELECT content, 1 - (embedding <=> '[0.1, 0.2, ...]') AS similarity
FROM documents
ORDER BY embedding <=> '[0.1, 0.2, ...]'
LIMIT 5;
```

```python
import psycopg2
from openai import OpenAI

# Connect to Postgres
conn = psycopg2.connect("dbname=mydb user=postgres")
cur = conn.cursor()

# Generate embedding
client = OpenAI()
query_embedding = client.embeddings.create(
    input="search query",
    model="text-embedding-ada-002"
).data[0].embedding

# Search
cur.execute(
    "SELECT content FROM documents ORDER BY embedding <=> %s LIMIT 5",
    (query_embedding,)
)
results = cur.fetchall()
```

### Weaviate - GraphQL API

```bash
# Docker
docker run -p 8080:8080 semitechnologies/weaviate:latest

# Install client
pip install weaviate-client
```

```python
import weaviate

# Connect
client = weaviate.Client("http://localhost:8080")

# Create schema
schema = {
    "classes": [{
        "class": "Document",
        "vectorizer": "text2vec-openai",
        "properties": [
            {"name": "content", "dataType": ["text"]},
        ]
    }]
}
client.schema.create(schema)

# Add data
client.data_object.create(
    {"content": "Document content"},
    "Document"
)

# Search
result = client.query.get("Document", ["content"]) \
    .with_near_text({"concepts": ["search query"]}) \
    .with_limit(5) \
    .do()
```

---

## Performance Benchmarks

### Query Latency (1M vectors, 768 dimensions)

| Database | P50 | P95 | P99 | QPS |
|----------|-----|-----|-----|-----|
| Qdrant | 5ms | 12ms | 18ms | 10,000 |
| Milvus | 8ms | 20ms | 35ms | 8,500 |
| Weaviate | 12ms | 28ms | 45ms | 6,000 |
| Chroma | 15ms | 35ms | 60ms | 4,000 |
| pgvector | 25ms | 60ms | 100ms | 2,000 |

*Tested on: 16 vCPU, 64GB RAM, SSD storage*

### Indexing Speed (1M vectors)

| Database | Time | Throughput |
|----------|------|------------|
| Milvus | 45s | 22k vec/s |
| Qdrant | 60s | 16k vec/s |
| Weaviate | 90s | 11k vec/s |
| Chroma | 120s | 8k vec/s |
| pgvector | 180s | 5.5k vec/s |

### Memory Efficiency (10M vectors, 768 dims)

| Database | Index Size | Compression | Overhead |
|----------|------------|-------------|----------|
| FAISS (IVF) | 28GB | PQ | 0% |
| Qdrant | 32GB | Scalar | +14% |
| Milvus | 35GB | - | +25% |
| Weaviate | 38GB | - | +36% |
| Chroma | 42GB | - | +50% |

---

## Feature Comparison

| Feature | Milvus | Qdrant | Weaviate | Chroma | pgvector | FAISS |
|---------|--------|--------|----------|--------|----------|-------|
| **Filtered Search** | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| **Hybrid Search** | ✅ | ✅ | ✅ | ⚠️ | ✅ | ❌ |
| **Multi-tenancy** | ✅ | ✅ | ✅ | ⚠️ | ✅ | ❌ |
| **CRUD Operations** | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ |
| **Distributed** | ✅ | ✅ | ✅ | ❌ | ⚠️ | ❌ |
| **Cloud Managed** | ✅ | ✅ | ✅ | ❌ | ✅ | ❌ |
| **Self-Hosted** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **ACID Transactions** | ⚠️ | ⚠️ | ⚠️ | ❌ | ✅ | ❌ |
| **GraphQL API** | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| **gRPC API** | ✅ | ✅ | ✅ | ❌ | ❌ | ❌ |
| **Python Client** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

✅ Full support | ⚠️ Partial support | ❌ Not supported

---

## Index Types

### HNSW (Hierarchical Navigable Small World)
- **Best for**: High recall, low latency
- **Supported by**: Qdrant, Milvus, Weaviate, Chroma
- **Use when**: Recall > speed

```python
# Qdrant example
client.create_collection(
    collection_name="docs",
    vectors_config=VectorParams(
        size=768,
        distance=Distance.COSINE
    ),
    hnsw_config=HnswConfigDiff(
        m=16,  # Number of connections
        ef_construct=100  # Build quality
    )
)
```

### IVF (Inverted File Index)
- **Best for**: Large scale, balanced speed/recall
- **Supported by**: Milvus, FAISS, pgvector
- **Use when**: Billions of vectors

```python
# Milvus example
collection.create_index(
    field_name="embedding",
    index_params={
        "index_type": "IVF_FLAT",
        "metric_type": "L2",
        "params": {"nlist": 1024}
    }
)
```

### Product Quantization (PQ)
- **Best for**: Memory efficiency
- **Supported by**: FAISS, Milvus
- **Use when**: Limited RAM

```python
# FAISS example
import faiss

index = faiss.IndexIVFPQ(
    quantizer,
    d,  # dimensions
    nlist,  # clusters
    m,  # subvectors
    nbits  # bits per subvector
)
```

---

## Distance Metrics

### Cosine Similarity
```python
# Range: [-1, 1], higher = more similar
# Use for: Normalized embeddings
similarity = 1 - cosine_distance(vec1, vec2)
```

### Euclidean (L2)
```python
# Range: [0, ∞], lower = more similar
# Use for: Absolute distances
distance = sqrt(sum((vec1 - vec2) ** 2))
```

### Dot Product
```python
# Range: [-∞, ∞], higher = more similar
# Use for: Unnormalized embeddings
score = sum(vec1 * vec2)
```

**Recommendation**: Use **Cosine** for most LLM embeddings (OpenAI, Cohere, etc.)

---

## RAG Integration Examples

### LangChain + Qdrant

```python
from langchain.vectorstores import Qdrant
from langchain.embeddings import OpenAIEmbeddings
from langchain.chains import RetrievalQA
from langchain.llms import OpenAI

# Setup
embeddings = OpenAIEmbeddings()
vectorstore = Qdrant.from_documents(
    documents,
    embeddings,
    url="http://localhost:6333",
    collection_name="docs"
)

# RAG Chain
qa = RetrievalQA.from_chain_type(
    llm=OpenAI(),
    chain_type="stuff",
    retriever=vectorstore.as_retriever()
)

# Query
answer = qa.run("What is the capital of France?")
```

### LlamaIndex + Milvus

```python
from llama_index import VectorStoreIndex, StorageContext
from llama_index.vector_stores import MilvusVectorStore

# Connect to Milvus
vector_store = MilvusVectorStore(
    host="localhost",
    port=19530,
    dim=1536
)

# Create index
storage_context = StorageContext.from_defaults(vector_store=vector_store)
index = VectorStoreIndex.from_documents(
    documents,
    storage_context=storage_context
)

# Query
query_engine = index.as_query_engine()
response = query_engine.query("Your question here")
```

### Chroma + OpenAI

```python
import chromadb
from openai import OpenAI

# Setup
chroma_client = chromadb.Client()
collection = chroma_client.create_collection("documents")
openai_client = OpenAI()

# Add documents
collection.add(
    documents=["Doc 1", "Doc 2"],
    ids=["id1", "id2"]
)

# RAG Query
def rag_query(question):
    # Retrieve
    results = collection.query(
        query_texts=[question],
        n_results=3
    )
    context = "\n".join(results['documents'][0])

    # Generate
    response = openai_client.chat.completions.create(
        model="gpt-4",
        messages=[
            {"role": "system", "content": "Answer based on context."},
            {"role": "user", "content": f"Context: {context}\n\nQuestion: {question}"}
        ]
    )
    return response.choices[0].message.content

answer = rag_query("What is AI?")
```

---

## Advanced Patterns

### 1. **Hybrid Search (Vector + Keyword)**

```python
# Weaviate example
result = client.query.get("Document", ["content"]) \
    .with_hybrid(
        query="search term",
        alpha=0.5  # 0 = pure BM25, 1 = pure vector
    ) \
    .with_limit(10) \
    .do()
```

### 2. **Multi-Vector Search**

```python
# Qdrant example - search multiple embeddings
client.search_batch(
    collection_name="docs",
    requests=[
        SearchRequest(
            vector=[0.1, 0.2, ...],
            limit=5
        ),
        SearchRequest(
            vector=[0.3, 0.4, ...],
            limit=5
        )
    ]
)
```

### 3. **Filtered Search**

```python
# Milvus example
collection.search(
    data=[[0.1]*768],
    anns_field="embedding",
    param={"metric_type": "COSINE", "params": {"ef": 64}},
    limit=10,
    expr='category == "technology" and date > "2026-01-01"'
)
```

### 4. **Multi-Tenancy**

```python
# Qdrant example - collection per tenant
def get_collection_name(tenant_id):
    return f"tenant_{tenant_id}_documents"

client.create_collection(
    collection_name=get_collection_name("org123"),
    vectors_config=VectorParams(size=768, distance=Distance.COSINE)
)
```

---

## Cost Analysis

### Self-Hosted (AWS, 1M vectors, 768 dims)

| Database | Instance | Monthly Cost | Storage |
|----------|----------|--------------|---------|
| Milvus | r6i.2xlarge | $410 | $50 |
| Qdrant | r6i.xlarge | $205 | $45 |
| Chroma | t3.large | $60 | $40 |
| pgvector | db.r6i.xlarge | $230 | Included |

### Managed Services (1M vectors, 10M queries/month)

| Service | Monthly Cost | Included |
|---------|--------------|----------|
| Pinecone | $70 | 1 pod |
| Zilliz (Milvus) | $100 | 2 CU |
| Qdrant Cloud | $95 | 1GB RAM |
| Weaviate Cloud | $120 | Standard tier |

---

## Best Practices

### 1. **Chunk Size Optimization**
```python
# Too small: loses context
chunk_size = 100  # ❌

# Too large: dilutes relevance
chunk_size = 5000  # ❌

# Optimal for most cases
chunk_size = 512  # ✅ (with overlap=50)
```

### 2. **Embedding Model Selection**
```python
# Fast, cheap: text-embedding-ada-002 (OpenAI)
# Balanced: all-MiniLM-L6-v2 (384 dims, free)
# Best quality: text-embedding-3-large (OpenAI, 3072 dims)

# Match dimensions in database!
```

### 3. **Index Tuning**
```python
# HNSW tuning
m = 16  # Start here, increase for better recall
ef_construct = 100  # Build quality
ef = 64  # Search quality (query time parameter)

# IVF tuning
nlist = sqrt(num_vectors)  # Rule of thumb
nprobe = nlist / 10  # Search 10% of clusters
```

### 4. **Monitoring**
```python
# Track these metrics
- Query latency (p50, p95, p99)
- Recall@k (% of relevant results in top k)
- Index size / vector count
- QPS (queries per second)
- Error rate
```

---

## Related Resources

- [RAG & Knowledge](rag-knowledge.md) - RAG frameworks and techniques
- [Agents & Orchestration](agents-orchestration.md) - Integrate with agents
- [Observability](observability-monitoring.md) - Monitor vector search
- [Foundation Models](foundation-models.md) - Embedding models

---

[← Back to Home](../index.md) | [Next: Observability & Monitoring →](observability-monitoring.md)
