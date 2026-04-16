# 📚 RAG & Knowledge

[← Back to Home](../index.md)

Retrieval-Augmented Generation (RAG) frameworks and knowledge base management tools.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Selection Guide](#selection-guide)
- [Quick Start](#quick-start)

---

## Overview

RAG tools enable LLMs to access external knowledge through:
- **Document Loading**: Parse PDFs, HTML, docs
- **Chunking & Indexing**: Split and embed documents
- **Retrieval**: Semantic search for relevant context
- **Generation**: Augment prompts with retrieved info

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | Data framework for LLM applications | ![GitHub stars](https://img.shields.io/github/stars/run-llama/llama_index?style=social) |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | Build context-aware LLM applications | ![GitHub stars](https://img.shields.io/github/stars/langchain-ai/langchain?style=social) |
| [unstructured-io/unstructured](https://github.com/Unstructured-IO/unstructured) | ETL for unstructured data (PDFs, images, etc.) | ![GitHub stars](https://img.shields.io/github/stars/Unstructured-IO/unstructured?style=social) |
| [Cinnamon/kotaemon](https://github.com/Cinnamon/kotaemon) | Open-source RAG-based document QA | ![GitHub stars](https://img.shields.io/github/stars/Cinnamon/kotaemon?style=social) |
| [embedchain/embedchain](https://github.com/embedchain/embedchain) | RAG framework in 3 lines of code | ![GitHub stars](https://img.shields.io/github/stars/embedchain/embedchain?style=social) |
| [getzep/zep](https://github.com/getzep/zep) | Long-term memory for AI assistants | ![GitHub stars](https://img.shields.io/github/stars/getzep/zep?style=social) |

---

## Selection Guide

### By Use Case

**🚀 Quick Prototyping**
- **LlamaIndex** - Simplest API, great docs
- **Embedchain** - 3 lines to get started
- **Kotaemon** - Ready-to-use UI

**🏢 Production Applications**
- **LlamaIndex** - Most mature ecosystem
- **LangChain** - Extensive integrations
- **Zep** - Enterprise memory management

**📄 Document Processing**
- **Unstructured** - Best document parsing
- **LlamaIndex** - 160+ data connectors
- **LangChain** - 100+ document loaders

**💬 Conversational AI**
- **Zep** - Persistent memory across sessions
- **LangChain** - Conversation chains
- **LlamaIndex** - Chat engines

### By Complexity

**Beginner**
- **Embedchain** - Minimal code
- **LlamaIndex** - High-level abstractions

**Intermediate**
- **LangChain** - Flexible chains
- **Kotaemon** - Customizable pipelines

**Advanced**
- **Custom RAG** - Full control
- **LlamaIndex Low-Level API** - Fine-grained optimization

---

## Quick Start

### LlamaIndex - Simple RAG

```bash
# Install
pip install llama-index
```

```python
from llama_index import VectorStoreIndex, SimpleDirectoryReader

# Load documents
documents = SimpleDirectoryReader("./data").load_data()

# Create index (embeds and stores)
index = VectorStoreIndex.from_documents(documents)

# Query
query_engine = index.as_query_engine()
response = query_engine.query("What is the main topic of these documents?")

print(response)
```

**That's it! LlamaIndex handles:**
- Document parsing
- Chunking
- Embedding (OpenAI by default)
- Vector storage (in-memory)
- Retrieval
- LLM generation

**With Custom Components:**
```python
from llama_index import VectorStoreIndex, ServiceContext
from llama_index.llms import Anthropic
from llama_index.embeddings import HuggingFaceEmbedding
from llama_index.vector_stores import QdrantVectorStore

# Custom LLM
llm = Anthropic(model="claude-3-sonnet-20240229")

# Custom embeddings
embed_model = HuggingFaceEmbedding(model_name="BAAI/bge-large-en-v1.5")

# Custom vector store
from qdrant_client import QdrantClient
client = QdrantClient(host="localhost", port=6333)
vector_store = QdrantVectorStore(client=client, collection_name="docs")

# Configure service context
service_context = ServiceContext.from_defaults(
    llm=llm,
    embed_model=embed_model
)

# Create index
index = VectorStoreIndex.from_documents(
    documents,
    service_context=service_context,
    vector_store=vector_store
)
```

### LangChain - Flexible RAG

```bash
# Install
pip install langchain langchain-community
```

```python
from langchain.document_loaders import PyPDFLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain.embeddings import OpenAIEmbeddings
from langchain.vectorstores import Chroma
from langchain.chains import RetrievalQA
from langchain.chat_models import ChatOpenAI

# 1. Load documents
loader = PyPDFLoader("document.pdf")
documents = loader.load()

# 2. Split into chunks
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200
)
texts = text_splitter.split_documents(documents)

# 3. Create embeddings and vector store
embeddings = OpenAIEmbeddings()
vectorstore = Chroma.from_documents(texts, embeddings)

# 4. Create retrieval chain
qa_chain = RetrievalQA.from_chain_type(
    llm=ChatOpenAI(model="gpt-4"),
    retriever=vectorstore.as_retriever(search_kwargs={"k": 5}),
    return_source_documents=True
)

# 5. Query
result = qa_chain({"query": "What is the main conclusion?"})
print(result["result"])
print(f"Sources: {result['source_documents']}")
```

### Unstructured - Document Parsing

```bash
# Install
pip install unstructured[all-docs]
```

```python
from unstructured.partition.auto import partition

# Automatically detect and parse any document type
elements = partition("document.pdf")

# Extract text from complex layouts
text = "\n".join([str(el) for el in elements])

# Preserve structure (titles, tables, etc.)
for element in elements:
    if element.category == "Title":
        print(f"## {element.text}")
    elif element.category == "NarrativeText":
        print(element.text)
    elif element.category == "Table":
        print(element.metadata.text_as_html)
```

**Supported Formats:**
- PDF, Word (.docx), PowerPoint (.pptx)
- HTML, XML, Markdown
- Images (OCR via Tesseract)
- Excel, CSV
- Email (.eml, .msg)

### Embedchain - 3-Line RAG

```bash
# Install
pip install embedchain
```

```python
from embedchain import App

# Create app
app = App()

# Add data sources
app.add("https://example.com/docs")
app.add("document.pdf")
app.add("Directory with files", data_type="directory")

# Query
response = app.query("What is this about?")
print(response)

# That's it! No configuration needed.
```

**Customization:**
```python
from embedchain import App

app = App.from_config(config={
    "llm": {
        "provider": "anthropic",
        "config": {"model": "claude-3-sonnet-20240229"}
    },
    "embedder": {
        "provider": "huggingface",
        "config": {"model": "BAAI/bge-base-en-v1.5"}
    },
    "vectordb": {
        "provider": "qdrant",
        "config": {"host": "localhost", "port": 6333}
    }
})
```

### Zep - Conversational Memory

```bash
# Install
pip install zep-python

# Run Zep server
docker run -d -p 8000:8000 ghcr.io/getzep/zep:latest
```

```python
from zep_python import ZepClient

# Initialize
client = ZepClient(base_url="http://localhost:8000")

# Create session
session_id = "user123_session"

# Add messages to memory
from zep_python.memory import Message

client.memory.add_memory(
    session_id=session_id,
    messages=[
        Message(role="user", content="I'm planning a trip to Paris"),
        Message(role="assistant", content="Great! When are you planning to go?"),
        Message(role="user", content="Next month")
    ]
)

# Search memory semantically
results = client.memory.search_memory(
    session_id=session_id,
    query="Where is the user traveling?"
)

print(results[0].message.content)  # "I'm planning a trip to Paris"

# Get conversation summary
summary = client.memory.get_session(session_id).summary
print(summary)  # "User is planning a trip to Paris next month"
```

---

## RAG Pipeline Deep Dive

### 1. **Document Loading**

```python
from llama_index import SimpleDirectoryReader
from langchain.document_loaders import (
    PyPDFLoader,
    UnstructuredMarkdownLoader,
    WebBaseLoader,
    GitHubIssuesLoader
)

# LlamaIndex - 160+ connectors
documents = SimpleDirectoryReader(
    input_dir="./docs",
    required_exts=[".pdf", ".docx", ".md"]
).load_data()

# LangChain - 100+ loaders
pdf_docs = PyPDFLoader("doc.pdf").load()
web_docs = WebBaseLoader("https://example.com").load()
github_issues = GitHubIssuesLoader(repo="owner/repo").load()
```

### 2. **Chunking Strategies**

```python
from langchain.text_splitter import (
    RecursiveCharacterTextSplitter,
    MarkdownTextSplitter,
    TokenTextSplitter
)

# Recursive (best for most cases)
splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200,  # Overlap to preserve context
    separators=["\n\n", "\n", ". ", " ", ""]
)

# Token-based (for LLM limits)
token_splitter = TokenTextSplitter(
    chunk_size=512,  # tokens, not characters
    chunk_overlap=50
)

# Semantic (preserve meaning)
from llama_index.node_parser import SentenceSplitter

semantic_splitter = SentenceSplitter(
    chunk_size=1024,
    chunk_overlap=20
)
```

**Best Practices:**
- Chunk size: 512-1000 tokens for most cases
- Overlap: 10-20% of chunk size
- Use semantic splitters for better coherence

### 3. **Embedding Models**

```python
# OpenAI (best quality, costs $)
from langchain.embeddings import OpenAIEmbeddings
embeddings = OpenAIEmbeddings(model="text-embedding-3-large")

# Open-source (free, good quality)
from langchain.embeddings import HuggingFaceEmbeddings
embeddings = HuggingFaceEmbeddings(
    model_name="BAAI/bge-large-en-v1.5"
)

# Cohere (multilingual)
from langchain.embeddings import CohereEmbeddings
embeddings = CohereEmbeddings(model="embed-multilingual-v3.0")
```

**Comparison:**

| Model | Dimensions | Quality | Cost | Speed |
|-------|------------|---------|------|-------|
| text-embedding-3-large | 3072 | Excellent | $0.13/1M | Fast |
| text-embedding-3-small | 1536 | Very Good | $0.02/1M | Fast |
| bge-large-en-v1.5 | 1024 | Good | Free | Medium |
| all-MiniLM-L6-v2 | 384 | Moderate | Free | Very Fast |

### 4. **Retrieval Strategies**

```python
# Basic semantic search
retriever = vectorstore.as_retriever(
    search_type="similarity",
    search_kwargs={"k": 5}  # Top 5 results
)

# MMR (Maximum Marginal Relevance) - diverse results
retriever = vectorstore.as_retriever(
    search_type="mmr",
    search_kwargs={"k": 5, "fetch_k": 20, "lambda_mult": 0.5}
)

# Similarity threshold
retriever = vectorstore.as_retriever(
    search_type="similarity_score_threshold",
    search_kwargs={"score_threshold": 0.8, "k": 5}
)

# Hybrid search (semantic + keyword)
from llama_index.retrievers import BM25Retriever, VectorIndexRetriever
from llama_index.retrievers import QueryFusionRetriever

vector_retriever = VectorIndexRetriever(index=vector_index)
bm25_retriever = BM25Retriever.from_defaults(nodes=nodes)

hybrid_retriever = QueryFusionRetriever(
    retrievers=[vector_retriever, bm25_retriever],
    similarity_top_k=5,
    mode="reciprocal_rerank"
)
```

### 5. **Reranking**

```python
# After retrieval, rerank for better results
from sentence_transformers import CrossEncoder

cross_encoder = CrossEncoder('cross-encoder/ms-marco-MiniLM-L-6-v2')

def rerank(query, documents, top_k=3):
    # Score query-document pairs
    pairs = [[query, doc.page_content] for doc in documents]
    scores = cross_encoder.predict(pairs)

    # Sort by score
    ranked_docs = sorted(
        zip(documents, scores),
        key=lambda x: x[1],
        reverse=True
    )

    return [doc for doc, score in ranked_docs[:top_k]]

# Usage
retrieved_docs = retriever.get_relevant_documents("query")
reranked_docs = rerank("query", retrieved_docs)
```

---

## Advanced RAG Patterns

### 1. **Multi-Query RAG**

```python
from langchain.retrievers.multi_query import MultiQueryRetriever

# Generate multiple queries from one question
multi_retriever = MultiQueryRetriever.from_llm(
    retriever=vectorstore.as_retriever(),
    llm=ChatOpenAI(temperature=0)
)

# "What is AI?" becomes:
# - "What is artificial intelligence?"
# - "Define AI"
# - "Explain artificial intelligence concepts"

results = multi_retriever.get_relevant_documents("What is AI?")
```

### 2. **Parent Document Retrieval**

```python
from langchain.retrievers import ParentDocumentRetriever
from langchain.storage import InMemoryStore

# Store full documents, but retrieve via small chunks
parent_splitter = RecursiveCharacterTextSplitter(chunk_size=2000)
child_splitter = RecursiveCharacterTextSplitter(chunk_size=400)

store = InMemoryStore()

retriever = ParentDocumentRetriever(
    vectorstore=vectorstore,
    docstore=store,
    child_splitter=child_splitter,
    parent_splitter=parent_splitter
)

# Searches small chunks, returns full parent documents
```

### 3. **Self-Query Retrieval**

```python
from langchain.retrievers.self_query.base import SelfQueryRetriever
from langchain.chains.query_constructor.base import AttributeInfo

# Metadata schema
metadata_field_info = [
    AttributeInfo(
        name="category",
        description="The category of the document",
        type="string"
    ),
    AttributeInfo(
        name="year",
        description="The year the document was written",
        type="integer"
    ),
]

retriever = SelfQueryRetriever.from_llm(
    llm=ChatOpenAI(),
    vectorstore=vectorstore,
    document_contents="Technical documentation",
    metadata_field_info=metadata_field_info
)

# Query: "Show me Python tutorials from 2024"
# Automatically filters: category="Python" AND year=2024
```

### 4. **Contextual Compression**

```python
from langchain.retrievers import ContextualCompressionRetriever
from langchain.retrievers.document_compressors import LLMChainExtractor

# Compress retrieved docs to only relevant parts
compressor = LLMChainExtractor.from_llm(llm=ChatOpenAI())

compression_retriever = ContextualCompressionRetriever(
    base_compressor=compressor,
    base_retriever=base_retriever
)

# Returns compressed, relevant excerpts instead of full chunks
```

---

## Prompt Engineering for RAG

### Basic RAG Prompt

```python
template = """Use the following context to answer the question.
If you cannot answer based on the context, say "I don't know".

Context:
{context}

Question: {question}

Answer:"""

from langchain import PromptTemplate

prompt = PromptTemplate(
    template=template,
    input_variables=["context", "question"]
)
```

### Advanced RAG Prompt

```python
template = """You are a helpful assistant answering questions based on provided context.

Instructions:
1. Only use information from the context below
2. If the context doesn't contain the answer, say "Based on the provided information, I cannot answer this question."
3. Cite specific parts of the context in your answer
4. If information conflicts, note the discrepancy

Context:
{context}

Question: {question}

Provide a clear, concise answer with citations:"""
```

### Chain-of-Thought RAG

```python
template = """Context:
{context}

Question: {question}

Let's solve this step by step:
1. What information from the context is relevant?
2. How does this information address the question?
3. What is the final answer?

Answer:"""
```

---

## Evaluation Metrics

### Retrieval Quality

```python
def retrieval_precision_at_k(retrieved_docs, relevant_doc_ids, k=5):
    """How many retrieved docs are relevant?"""
    retrieved_ids = [doc.metadata['id'] for doc in retrieved_docs[:k]]
    relevant_retrieved = set(retrieved_ids) & set(relevant_doc_ids)
    return len(relevant_retrieved) / k

def retrieval_recall_at_k(retrieved_docs, relevant_doc_ids, k=5):
    """How many relevant docs were retrieved?"""
    retrieved_ids = [doc.metadata['id'] for doc in retrieved_docs[:k]]
    relevant_retrieved = set(retrieved_ids) & set(relevant_doc_ids)
    return len(relevant_retrieved) / len(relevant_doc_ids)
```

### Generation Quality (RAGAS)

```python
from ragas import evaluate
from ragas.metrics import faithfulness, answer_relevancy

# Faithfulness: Is answer grounded in context?
# Answer Relevancy: Does answer address question?

results = evaluate(
    dataset,
    metrics=[faithfulness, answer_relevancy]
)

print(f"Faithfulness: {results['faithfulness']}")
print(f"Answer Relevancy: {results['answer_relevancy']}")
```

---

## Common Issues & Solutions

### 1. **Poor Retrieval Quality**

**Problem**: Irrelevant documents retrieved

**Solutions:**
```python
# 1. Better chunking
splitter = RecursiveCharacterTextSplitter(
    chunk_size=512,  # Smaller chunks
    chunk_overlap=100  # More overlap
)

# 2. Hybrid search
hybrid_retriever = QueryFusionRetriever(...)

# 3. Reranking
reranked = rerank(query, retrieved_docs)

# 4. Metadata filtering
retriever = vectorstore.as_retriever(
    search_kwargs={
        "filter": {"category": "technical"},
        "k": 10
    }
)
```

### 2. **Context Window Overflow**

**Problem**: Too much context for LLM

**Solutions:**
```python
# 1. Contextual compression
compression_retriever = ContextualCompressionRetriever(...)

# 2. Map-reduce
from langchain.chains.summarize import load_summarize_chain

chain = load_summarize_chain(
    llm,
    chain_type="map_reduce"  # Process chunks independently
)

# 3. Refine
chain = load_summarize_chain(
    llm,
    chain_type="refine"  # Iteratively refine answer
)
```

### 3. **Hallucinations**

**Problem**: LLM invents information

**Solutions:**
```python
# 1. Strict prompt
template = """ONLY use the context below. Do NOT use external knowledge.
If the answer is not in the context, respond: "I don't have enough information."

Context: {context}
Question: {question}"""

# 2. Lower temperature
llm = ChatOpenAI(temperature=0)

# 3. Validate with faithfulness metric
from ragas.metrics import faithfulness

score = faithfulness.measure(answer, context)
if score < 0.8:
    return "I'm not confident in this answer."
```

---

## Production Best Practices

### 1. **Caching**

```python
from langchain.cache import InMemoryCache, RedisCache
import langchain

# Cache LLM responses
langchain.llm_cache = InMemoryCache()

# Or persistent cache
langchain.llm_cache = RedisCache(redis_=redis_client)
```

### 2. **Monitoring**

```python
from langchain.callbacks import LangChainTracer

# Track all RAG operations
tracer = LangChainTracer()

qa_chain.run(
    "query",
    callbacks=[tracer]
)

# View in LangSmith dashboard
```

### 3. **Async Processing**

```python
import asyncio
from langchain.chains import RetrievalQA

async def aquery(question):
    return await qa_chain.arun(question)

# Process multiple queries concurrently
questions = ["Q1", "Q2", "Q3"]
results = await asyncio.gather(*[aquery(q) for q in questions])
```

---

## Related Resources

- [Vector Databases](vector-databases.md) - Storage backends
- [Agents & Orchestration](agents-orchestration.md) - RAG agents
- [Evaluation & Testing](evaluation-testing.md) - Test RAG quality
- [Observability](observability-monitoring.md) - Monitor RAG pipelines

---

[← Back to Home](../index.md) | [Next: Prompt Engineering →](prompt-engineering.md)
