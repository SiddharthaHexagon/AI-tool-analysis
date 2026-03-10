# 🔍 RAG Cheat Sheet
### Retrieval-Augmented Generation — Complete Reference

> **RAG = Retriever + Generator** | Reduce hallucinations · Stay up-to-date · No retraining needed

---

## Table of Contents

1. [What is RAG?](#1-what-is-rag)
2. [Full RAG Pipeline](#2-full-rag-pipeline)
3. [Chunking Strategies](#3-chunking-strategies)
4. [Embedding Models](#4-embedding-models)
5. [Retrieval Methods](#5-retrieval-methods)
6. [Generation & Prompting](#6-generation--prompting)
7. [Advanced RAG Patterns](#7-advanced-rag-patterns)
8. [Vector Databases](#8-vector-databases)
9. [Evaluation Framework](#9-evaluation-framework)
10. [Tooling Ecosystem](#10-tooling-ecosystem)
11. [Tips & Common Pitfalls](#11-tips--common-pitfalls)

---

## 1. What is RAG?

**Retrieval-Augmented Generation** grounds LLM responses in external, verifiable knowledge retrieved at query time — without retraining.

### Core Idea
```
User Query → Embed Query → Search Vector DB → Retrieve Top-K Chunks
           → Inject into Prompt → LLM Generates Grounded Answer
```

### RAG vs Alternatives

| Method | Pros | Cons | Best For |
|---|---|---|---|
| Prompt Engineering | Zero cost, instant | Limited to model's training knowledge | Simple Q&A on known topics |
| Fine-tuning | Learns style, format, tone | Expensive, data goes stale | Style adaptation, structured output |
| **RAG** | **Live data, citable, low cost** | Retrieval latency, chunking complexity | Knowledge-intensive tasks |
| RAG + Fine-tuning | Best of both worlds | Most complex setup | Enterprise production systems |

### When to Use RAG

**✅ Use RAG when:**
- Knowledge changes frequently (news, docs, policies)
- Working with private/internal documents
- Need source attribution and citations
- Domain-specific Q&A over large corpora
- Multiple heterogeneous knowledge bases
- Cost-sensitive (vs full fine-tuning)

**❌ Skip RAG when:**
- Task is purely creative/generative with no facts needed
- Knowledge is static, small, and already in training data
- Latency is ultra-critical (< 100ms hard requirement)
- Query never requires external context

### Architecture Overview

```
[Raw Docs] → [Chunker] → [Embedder] → [Vector Store]
                                            ↑ index
[User Query] → [Query Embedder] → [ANN Search] → [Re-ranker]
                                                      ↓
                                              [LLM Generator]
                                                      ↓
                                               [Final Answer]
```

---

## 2. Full RAG Pipeline

### 🔴 Offline (Indexing) Pipeline

| Step | Stage | Description | Key Tools |
|---|---|---|---|
| 01 | **Document Loading** | Ingest from PDFs, HTML, S3, DBs, APIs, web crawlers | `PyPDFLoader`, `UnstructuredLoader`, `WebBaseLoader` |
| 02 | **Pre-processing** | Remove boilerplate, fix encoding, OCR scans, normalize whitespace | `Unstructured`, `pdfplumber`, `pytesseract` |
| 03 | **Chunking** | Split docs into segments with overlap | `RecursiveCharacterTextSplitter` |
| 04 | **Embedding** | Convert each chunk to a dense vector | `OpenAIEmbeddings`, `HuggingFaceEmbeddings` |
| 05 | **Indexing** | Store vectors + metadata in vector DB | `Pinecone.upsert()`, `Chroma.add()` |

**Indexing Tips:**
- Preserve metadata: title, date, URL, author, section heading
- Handle auth/versioning for private document sources
- Tables → markdown or pipe-delimited text for better embedding
- Batch embed 100–1000 chunks per API call (10–100x cost saving)

### 🟢 Online (Query) Pipeline

| Step | Stage | Description | Key Tools |
|---|---|---|---|
| Q1 | **Query Processing** | Rewrite, expand, or decompose the user query | `HyDE`, `MultiQueryRetriever` |
| Q2 | **Retrieval** | Find top-k semantically similar chunks via ANN | `similarity_search(k=5)` |
| Q3 | **Re-ranking** | Cross-encoder rescores top-k for precision | `CohereRerank`, `BGEReranker` |
| Q4 | **Context Assembly** | Format chunks into prompt, order by relevance | `PromptTemplate`, `ChatPromptTemplate` |
| Q5 | **Generation** | LLM generates answer grounded in context | `ChatOpenAI`, `Anthropic Claude` |
| Q6 | **Post-processing** | Validate, parse, add citations, cache response | `output_parsers`, `guardrails` |

**Query Pipeline Tips:**
- Apply metadata filters **before** vector search for 10–100x speedup
- Put most relevant chunks **first or last** in prompt (avoid "lost in middle")
- Set similarity score threshold (e.g., cosine > 0.7) to filter irrelevant results
- Cache frequent queries with semantic similarity matching

---

## 3. Chunking Strategies

### Strategy Comparison

| Strategy | Tag | Best For | Chunk Size |
|---|---|---|---|
| Fixed-Size | SIMPLE | Uniform plain text, prototyping | 256–512 tokens |
| Recursive Splitting | DEFAULT | Most production systems | 256–1024 tokens |
| Semantic Chunking | SMART | Long-form articles, research papers | Variable |
| Document-Aware | STRUCTURED | Markdown, HTML, technical manuals | Section-based |
| Parent-Child | ADVANCED | High precision + full context needed | Child: 150–300, Parent: 1500–2000 |
| Agentic (Proposition) | SOTA | Medical, legal, high-stakes Q&A | 1 fact per chunk |

### Detailed Breakdown

#### Fixed-Size Chunking
```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size=512,
    chunk_overlap=64   # ~12% overlap
)
```
- ✅ Deterministic, very fast
- ❌ Splits mid-sentence, no semantic awareness

#### Recursive Character Splitting *(Recommended Default)*
```python
RecursiveCharacterTextSplitter(
    separators=["\n\n", "\n", ".", " ", ""],
    chunk_size=512,
    chunk_overlap=50
)
```
- ✅ Respects natural text boundaries (paragraphs → sentences → words)
- ❌ Still no semantic awareness

#### Semantic Chunking
```python
from langchain_experimental.text_splitter import SemanticChunker

splitter = SemanticChunker(
    embeddings=embed_model,
    breakpoint_threshold_type="percentile"  # or "std_dev"
)
```
- ✅ Splits at topic shifts via embedding cosine distance spikes
- ❌ Slow (embeds every sentence), variable chunk sizes

#### Document-Aware Chunking
```python
from langchain.text_splitter import MarkdownHeaderTextSplitter

splitter = MarkdownHeaderTextSplitter(
    headers_to_split_on=[("##", "H2"), ("###", "H3")]
)
```
- ✅ Preserves document hierarchy, tables and code stay intact
- ❌ Requires clean structured input

#### Parent-Child Chunking *(Production Recommended)*
```python
from langchain.retrievers import ParentDocumentRetriever

retriever = ParentDocumentRetriever(
    vectorstore=vectorstore,
    docstore=store,
    child_splitter=small_splitter,    # 150–300 tokens, indexed
    parent_splitter=big_splitter,     # 1500–2000 tokens, returned
)
```
- ✅ Precise retrieval + rich context for LLM
- ❌ Requires parent-child mapping store

### Chunk Size Selection Guide

| Size (tokens) | Label | Use Case | Trade-off |
|---|---|---|---|
| 64–128 | Micro | Dense retrieval, very specific facts | High precision, low context |
| 256–512 | Standard | General Q&A, conversational RAG | **Balanced — recommended default** |
| 512–1024 | Large | Summarization, long-form analysis | More context, less precision |
| 1024+ | Full Sections | Document-level understanding | Use with Parent-Child pattern |

> 💡 **Rule of thumb:** Overlap should be 10–20% of chunk size. Always store the original chunk text alongside its vector.

---

## 4. Embedding Models

### How Embeddings Work
- Text → fixed-size dense vector (768–3072 dimensions)
- Semantically similar texts → nearby vectors in high-dimensional space
- Retrieval = find vectors closest to query vector via cosine similarity

### Key Rules
| Rule | Why It Matters |
|---|---|
| **Use the same model for indexing & querying** | Embedding spaces are not universal — mixing models breaks retrieval |
| **Match model to your domain** | Legal/medical/code domains benefit from specialized models |
| **Normalize vectors** | Required if using dot-product similarity |
| **Batch your embedding calls** | Send 100–1000 chunks per API call (100x cost reduction) |
| **Re-embed on model upgrade** | Must re-index entire corpus when changing embedding model |
| **Check max token limit** | Most models cap at 512–8192 tokens — truncation loses information |

### Embedding Model Comparison

| Model | Dims | Max Tokens | MTEB Score | Cost | Best For |
|---|---|---|---|---|---|
| `text-embedding-3-large` | 3072 | 8191 | 64.6 | $0.13/1M | General production |
| `text-embedding-3-small` | 1536 | 8191 | 62.3 | $0.02/1M | Cost-sensitive apps |
| `voyage-3` | 1024 | 32000 | 67.1 | $0.06/1M | Long documents |
| `cohere-embed-v3` | 1024 | 512 | 64.5 | $0.10/1M | Multilingual |
| `BAAI/bge-large-en` | 1024 | 512 | 63.9 | Free (local) | On-prem / privacy |
| `nomic-embed-text` | 768 | 8192 | 62.4 | Free (local) | Local dev / open source |
| `intfloat/e5-large-v2` | 1024 | 512 | 62.3 | Free (local) | Instruction-following |

> 💡 `voyage-3` and `text-embedding-3-large` lead MTEB. For local/private: `BAAI/bge-large-en` is the strongest open-source option.

---

## 5. Retrieval Methods

### Core Retrieval Types

#### Dense Retrieval (Semantic)
- Embed query + docs with same model → find nearest neighbors via ANN
- **Algorithms:** HNSW (best quality/speed), IVF-Flat (large-scale), ScaNN, Annoy
- ✅ Semantic similarity, handles paraphrasing
- ❌ Misses exact keywords, out-of-vocabulary terms

#### Sparse Retrieval (Keyword — BM25)
- TF-IDF / BM25 keyword matching, inverted index
- **Parameters:** `k1=1.2–2.0` (term saturation), `b=0.75` (length normalization)
- ✅ Exact matches, rare terms, product codes, names
- ❌ No semantic understanding

#### Hybrid Retrieval *(Best Practice)*
- Combine dense + sparse scores via **Reciprocal Rank Fusion (RRF)**
- `RRF score = Σ 1 / (k + rank_i)` where `k=60` is standard
- ✅ Most robust across all query types
- Implementation: Weaviate, Qdrant, and Pinecone all support native hybrid search

```python
# RRF Fusion (manual)
def rrf_fusion(dense_results, sparse_results, k=60):
    scores = {}
    for rank, doc in enumerate(dense_results):
        scores[doc.id] = scores.get(doc.id, 0) + 1 / (k + rank + 1)
    for rank, doc in enumerate(sparse_results):
        scores[doc.id] = scores.get(doc.id, 0) + 1 / (k + rank + 1)
    return sorted(scores.items(), key=lambda x: x[1], reverse=True)
```

### Query Transformation Techniques

| Technique | Description | Impact |
|---|---|---|
| **HyDE** | Ask LLM to write a fake answer → embed it → retrieve | 🔴 High |
| **Multi-Query** | LLM rewrites query N ways → retrieve per query → merge+dedup | 🔴 High |
| **Step-Back Prompting** | Ask abstract version first to retrieve higher-level context | 🟡 Medium |
| **Query Decomposition** | Break multi-hop question into sub-questions, answer each | 🟡 Medium |
| **RAG-Fusion** | Multi-query + RRF reranking of all results | 🔴 High |

```python
# Multi-Query Retriever (LangChain)
from langchain.retrievers.multi_query import MultiQueryRetriever

retriever = MultiQueryRetriever.from_llm(
    retriever=vectorstore.as_retriever(),
    llm=llm
)
```

### Re-ranking

Re-rank top-k ANN results with a cross-encoder before passing to LLM.
**Pattern:** Retrieve top-20 → Rerank → Pass top-5 to LLM

| Re-ranker | Type | Note |
|---|---|---|
| Cohere Rerank | Managed API | Best managed, 1-liner integration, ~$1/1000 calls |
| `BAAI/bge-reranker-large` | Open Source | Best local option (HuggingFace) |
| ColBERT / ColPali | Late Interaction | High precision, GPU recommended |
| MonoT5 | Seq2Seq | Flexible, HuggingFace |
| LLM-as-judge | LLM scoring | Most accurate, most expensive |

---

## 6. Generation & Prompting

### RAG System Prompt Template

```
SYSTEM:
You are a helpful assistant. Answer ONLY using the provided context below.

Rules:
1. Only use information explicitly stated in the context
2. If the context is insufficient, respond: "I don't have enough information to answer this."
3. Cite sources using [Source N] inline format
4. Never extrapolate, assume, or make up facts

Context:
[Source 1]: {chunk_1_text}
[Source 2]: {chunk_2_text}
[Source 3]: {chunk_3_text}

Question: {user_query}
```

### Context Window Strategies

| Problem | Description | Fix |
|---|---|---|
| **Lost in the Middle** | LLMs attend more to start/end of context | Sort by relevance; put top chunk first |
| **Context Overflow** | Too many chunks exceed window limit | Rerank + keep top-5; use contextual compression |
| **Contradictory Chunks** | Multiple docs disagree on same fact | Add timestamps in metadata; instruct to prefer latest |
| **Irrelevant Padding** | Low-relevance chunks dilute the signal | Set cosine similarity threshold > 0.7 |

### LLM Parameters for RAG

| Parameter | Recommended Value | Reason |
|---|---|---|
| `temperature` | 0.0–0.3 | Lower = more faithful to context |
| `max_tokens` | 256–1024 | Balance completeness vs cost |
| `top_p` | 0.9 | Moderate nucleus sampling |
| `frequency_penalty` | 0.0–0.3 | Reduce repetition in long answers |
| `stream` | `true` | Better UX for longer generations |

### Model Selection for RAG

| Model | Context Window | Best For |
|---|---|---|
| GPT-4o | 128k | Reasoning, complex multi-hop RAG |
| Claude 3.5 Sonnet | 200k | Long documents, high accuracy |
| Gemini 1.5 Pro | 1M | Massive document ingestion |
| Llama 3.1 70B | 128k | On-prem / private data |
| Mistral 7B | 32k | Fast, low-cost baseline |
| Command R+ (Cohere) | 128k | RAG-optimized by design |

### Citation Patterns

```python
# JSON citation output
prompt = """Answer the question and cite sources as JSON:
{"answer": "...", "sources": ["source_id_1", "source_id_2"]}

Context: {context}
Question: {question}"""

# Inline citation
prompt = """Answer using [N] inline citations.
Example: "The policy changed in 2023 [1], affecting all employees [2]."
"""
```

---

## 7. Advanced RAG Patterns

### Self-RAG
Model decides **when** to retrieve (reflection token `[Retrieve]`), evaluates doc relevance (ISREL), answer support (ISSUP), and output usefulness (ISUSE).
- ✅ Eliminates unnecessary retrieval, self-corrects poor generations
- ⚡ High complexity — requires specially fine-tuned model

### CRAG (Corrective RAG)
Evaluates retrieval quality with a scoring model. If score is below threshold → falls back to web search. If ambiguous → combines internal + web knowledge.
- ✅ Handles incomplete or stale indexed data automatically
- ⚡ Medium complexity — needs web search integration

### GraphRAG
Builds a knowledge graph from documents (entities = nodes, relations = edges). Queries both graph (structured) and vectors (semantic) simultaneously.
- ✅ Multi-hop reasoning, entity relationships, global document understanding
- ⚡ Very high complexity — graph construction is expensive

```python
# Microsoft GraphRAG
pip install graphrag
graphrag index --root ./data
graphrag query --root ./data --method global "What are the main themes?"
```

### Agentic RAG
RAG as one tool in a ReAct / function-calling agent loop. Agent decides: retrieve, web search, query DB, or execute code.

```python
tools = [
    Tool(name="vector_search", func=retriever.get_relevant_documents),
    Tool(name="web_search", func=search.run),
    Tool(name="sql_query", func=db.run),
]
agent = initialize_agent(tools, llm, agent=AgentType.OPENAI_FUNCTIONS)
```

### Modular RAG
Swap any component (retriever, re-ranker, reader, memory) independently. Standard I/O interfaces like microservices.
- **Modules:** Search, Memory, Fusion, Task Adapter
- ✅ Mix and match components per domain without rebuilding

### Multi-Modal RAG
Index and retrieve across text, images, tables, and charts using vision models.
- **Text:** standard embedding pipeline
- **Images:** CLIP / ColPali for embedding
- **Tables:** serialize to markdown or structure-aware encoding
- **Answer:** vision LLM (GPT-4o, Claude 3.5) for image Q&A

### Parent-Child / Hierarchical RAG
Index small child chunks for precise vector retrieval, but return larger parent chunks to the LLM for full context.
```
Child chunk (150–300 tokens) → indexed in vector DB
Parent chunk (1500–2000 tokens) → stored in docstore, returned to LLM
```

---

## 8. Vector Databases

### Comparison Table

| Database | Type | ANN Algo | Hybrid Search | Filtering | Scale | Pricing |
|---|---|---|---|---|---|---|
| **Pinecone** | Managed SaaS | Proprietary | ✅ | ✅ Rich | 10B+ vectors | Pay-as-go |
| **Weaviate** | Open / Cloud | HNSW | ✅ Native | ✅ GraphQL | Billions | Free + cloud |
| **Qdrant** | Open / Cloud | HNSW (Rust) | ✅ | ✅ Payload filters | Billions | Free + cloud |
| **Milvus** | Open / Cloud | IVF/HNSW | ✅ | ✅ Scalar | Trillions | Free + Zilliz |
| **Chroma** | Open Source | HNSW | ~Partial | ✅ Metadata | Millions | Free |
| **pgvector** | Postgres ext | IVFFlat/HNSW | ✅ + Full-Text | ✅ SQL | 10M–1B | DB cost only |
| **FAISS** | Library | IVF/HNSW/PQ | ❌ | ❌ | Billions (GPU) | Free |
| **Redis VSS** | In-memory | HNSW / Flat | ✅ | ✅ RediSearch | Millions | Redis pricing |

### HNSW Index Parameters

| Parameter | Recommended Value | Effect |
|---|---|---|
| `M` | 16–64 | Connections per node. Higher = better recall + more RAM |
| `ef_construction` | 100–400 | Build-time beam width. Higher = better index, slower build |
| `ef_search` | 50–200 | Query-time beam width. Higher = better recall, slower queries |
| `distance_metric` | cosine / dot / l2 | Must match your embedding model |
| `max_elements` | 1.5× expected | Pre-allocate with buffer |

### Metadata Filtering Best Practices

Always apply filters **before** vector search (pre-filtering), not after.

```python
# Qdrant pre-filter example
results = client.search(
    collection_name="docs",
    query_vector=query_embedding,
    query_filter=Filter(
        must=[
            FieldCondition(key="dept", match=MatchValue(value="legal")),
            FieldCondition(key="date", range=DatetimeRange(gte="2024-01-01")),
        ]
    ),
    limit=10,
)
```

**Common filter fields to store:**
- `date` / `created_at` — recency filtering
- `doc_type` — contract, policy, report
- `department` / `team` — multi-tenant isolation
- `language` — multilingual corpora
- `security_level` — access control in RAG
- `source_url` — traceability

---

## 9. Evaluation Framework

### Retrieval Metrics

| Metric | Description | Target | Tool |
|---|---|---|---|
| **Context Recall** | % of ground-truth facts covered by retrieved docs | > 0.90 | RAGAS |
| **Context Precision** | % of retrieved docs that are actually relevant | > 0.80 | RAGAS |
| **MRR** | Mean Reciprocal Rank — position of first relevant result | > 0.70 | Custom |
| **NDCG@k** | Normalized Discounted Cumulative Gain at rank k | > 0.75 | BEIR |
| **Hit Rate@k** | Did at least 1 relevant doc appear in top-k? | > 0.90 | Custom |

### Generation Metrics

| Metric | Description | Target | Tool |
|---|---|---|---|
| **Faithfulness** | Is the answer fully supported by context? | > 0.90 | RAGAS |
| **Answer Relevance** | Does the answer address the question? | > 0.85 | RAGAS |
| **Hallucination Rate** | % of answers with unsupported claims | < 5% | G-Eval |
| **Exact Match (EM)** | Answer exactly matches gold standard | Task-specific | SQuAD-style |
| **ROUGE-L** | Recall-oriented summary quality | > 0.40 | Standard NLP |

### System Metrics

| Metric | Description | Target |
|---|---|---|
| **E2E Latency** | Total query → response time | < 3s (P95) |
| **Retrieval Latency** | ANN search + reranking time | < 200ms |
| **Cost per Query** | Embedding + LLM + DB costs | Define per budget |
| **Cache Hit Rate** | % of queries served from semantic cache | > 20% |
| **Throughput (QPS)** | Max queries/second under load | SLA-defined |

### RAGAS Quick Start

```python
from ragas import evaluate
from ragas.metrics import (
    faithfulness,
    answer_relevancy,
    context_recall,
    context_precision,
)
from datasets import Dataset

# Required fields: question, answer, contexts, ground_truth
dataset = Dataset.from_dict({
    "question": ["What is RAG?"],
    "answer": ["RAG is Retrieval-Augmented Generation..."],
    "contexts": [["RAG combines retrieval with generation..."]],
    "ground_truth": ["Retrieval-Augmented Generation (RAG)..."],
})

result = evaluate(
    dataset,
    metrics=[faithfulness, answer_relevancy, context_recall, context_precision],
)
print(result)
```

### Recommended Evaluation Datasets

| Dataset | Focus | Size |
|---|---|---|
| BEIR Benchmark | 18 heterogeneous retrieval tasks | Various |
| MSMARCO | Passage retrieval | 8.8M passages |
| Natural Questions | Google search Q&A on Wikipedia | 300K |
| HotpotQA | Multi-hop reasoning (2+ docs required) | 113K |
| TriviaQA | Trivia with web + Wikipedia evidence | 650K |
| **Your own golden set** ⭐ | Domain-specific labeled Q&A pairs | 50–200 |

> 💡 Always create a **domain-specific golden evaluation set** of 50–200 hand-labeled Q&A pairs from your actual data. It's the most reliable signal for your specific use case.

---

## 10. Tooling Ecosystem

### Orchestration Frameworks

| Framework | Description | Best For |
|---|---|---|
| **LangChain** | Most popular. LCEL, agents, 100+ integrations | Full-stack RAG apps |
| **LlamaIndex** | Data-centric, best for complex indexing & query engines | Data-heavy pipelines |
| **Haystack** | Pipeline-first, production NLP | Enterprise production |
| **LangGraph** | Stateful agent graphs, multi-step workflows | Agentic RAG |
| **DSPy** | Programmatic prompting, auto-optimizes pipelines | Optimization-focused |

### Document Processing

| Tool | Purpose |
|---|---|
| **Unstructured.io** | Parse PDFs, PPT, HTML, DOCX, images → clean text |
| **Docling (IBM)** | Advanced PDF/DOCX layout preservation + tables |
| **Marker** | PDF → Markdown with LaTeX, tables, code blocks |
| **PyMuPDF (fitz)** | Fast PDF text extraction preserving layout |
| **LlamaParse** | LLM-powered premium document parsing |

### Monitoring & Observability

| Tool | Description |
|---|---|
| **LangSmith** | LangChain-native tracing, eval, dataset management |
| **Arize Phoenix** | Open-source LLM observability + RAG evals |
| **Traceloop** | OpenTelemetry-based LLM tracing |
| **Weights & Biases** | Experiment tracking for LLM + RAG evals |
| **Helicone** | Proxy + analytics for OpenAI/Anthropic API calls |

### Reference Production Stack (2025)

| Layer | Recommended Choice | Alternative |
|---|---|---|
| **Ingestion** | Docling + Unstructured.io | PyMuPDF, LlamaParse |
| **Chunking** | LlamaIndex SemanticChunker | RecursiveCharacterTextSplitter |
| **Embedding** | `text-embedding-3-large` | `BAAI/bge-large-en` (local) |
| **Vector DB** | Qdrant or Weaviate | pgvector (for Postgres shops) |
| **Retrieval** | Hybrid (BM25 + Dense) + Cohere Rerank | BGE Reranker (local) |
| **LLM** | Claude 3.5 Sonnet / GPT-4o | Llama 3.1 70B (private) |
| **Orchestration** | LangChain / LlamaIndex | Haystack |
| **Evaluation** | RAGAS + LangSmith | Arize Phoenix |
| **Observability** | LangSmith | Traceloop |

---

## 11. Tips & Common Pitfalls

### ✅ Best Practices

- **Filter before searching** — Apply metadata filters pre-vector-search for 10–100x speedup
- **Always re-rank in production** — Cross-encoder reranking dramatically improves precision
- **Include source metadata** — Store title, date, URL, section with every chunk
- **Semantic caching** — Cache frequent/similar queries to reduce cost and latency
- **Tune chunk size per domain** — Code needs smaller chunks than prose; legal docs need larger
- **Test retrieval independently** — Evaluate retriever before evaluating end-to-end
- **Use overlap** — 10–20% chunk overlap prevents context boundary cuts
- **Golden eval set** — Build 50–200 labeled Q&A pairs from your domain

### ⚠️ Common Mistakes

- **Chunking mid-sentence** — Always use overlap and sentence-aware splitters
- **Mixing embedding models** — Index and query must use identical model
- **Too many chunks in context** — Stuffing 15+ chunks dilutes signal; use top-5 after reranking
- **Ignoring embedding model quality** — Choosing cheap model degrades retrieval significantly
- **No score threshold** — Retrieve with a minimum similarity score to filter irrelevant docs
- **No metadata** — Without metadata you can't filter, trace, or do time-aware retrieval
- **Fixed chunk size everywhere** — Different content types need different strategies

### ❌ Hard Don'ts

- **Don't** skip evaluation — "It seems to work" is not production-ready
- **Don't** put all documents in one namespace/collection — organize by domain/tenant
- **Don't** ignore the "lost in the middle" problem for long context
- **Don't** use temperature > 0.5 for factual RAG — increases hallucination
- **Don't** forget to handle the "no answer" case — instruct model to say "I don't know"
- **Don't** neglect index updates — stale indexes return outdated or missing information

---

## Quick Reference Card

```
CHUNK SIZE:     256–512 tokens (default) | 10–20% overlap
TOP-K:          Retrieve 20 → Rerank → Pass top-5 to LLM
SIMILARITY:     Filter below cosine 0.70
TEMPERATURE:    0.0–0.3 for factual RAG
EVAL:           Faithfulness > 0.9 | Context Recall > 0.9
LATENCY:        Retrieval < 200ms | E2E < 3s P95
EMBEDDING:      Same model for index & query — always
HYBRID:         BM25 + Dense via RRF (k=60) = best default
```

---

*RAG Cheat Sheet — 2025 | Covers: LangChain · LlamaIndex · RAGAS · Weaviate · Qdrant · Pinecone · OpenAI · Cohere · HuggingFace*
