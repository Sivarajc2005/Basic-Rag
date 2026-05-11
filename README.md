# 📘 Basic RAG PDF Pipeline

A beginner-friendly Retrieval-Augmented Generation (RAG) notebook built using Python, LangChain, Hugging Face embeddings, and ChromaDB.

This project demonstrates how to:

* Load a PDF document
* Split the document into chunks
* Convert text chunks into embeddings
* Store embeddings inside a vector database
* Perform semantic similarity search on the PDF

---

# 🚀 Project Workflow

The notebook follows this RAG pipeline:

```text
PDF Document
     ↓
Document Loader
     ↓
Text Chunking
     ↓
Embeddings Creation
     ↓
Vector Database (ChromaDB)
     ↓
Similarity Search
     ↓
Relevant Context Retrieved
```

---

# 🛠️ Technologies Used

* Python
* LangChain
* ChromaDB
* Hugging Face Sentence Transformers
* PyPDF

---

# 📂 Project Structure

```text
basic-rag/
│
├── document.ipynb          # Main notebook
├── chroma_db/              # Persisted vector database
├── pdf/
│   └── Designing Machine Learning Systems.pdf
└── README.md
```

---

# 📦 Installation

Create a virtual environment:

```bash
python -m venv .venv
```

Activate the environment:

### Windows

```bash
.venv\Scripts\activate
```

### Mac/Linux

```bash
source .venv/bin/activate
```

Install required packages:

```bash
pip install langchain
pip install langchain-community
pip install langchain-text-splitters
pip install chromadb
pip install sentence-transformers
pip install pypdf
```

Or install everything together:

```bash
pip install langchain langchain-community langchain-text-splitters chromadb sentence-transformers pypdf
```

---

# 📥 Step 1 — Load PDF

The notebook uses `PyPDFLoader` from LangChain to load the PDF document.

```python
from langchain_community.document_loaders import PyPDFLoader

loadPDF = PyPDFLoader(r"D:\learn RAG\basic rag\pdf\Designing Machine Learning Systems.pdf")
document = loadPDF.load()
```

This converts the PDF into LangChain document objects.

---

# ✂️ Step 2 — Split the Document into Chunks

Large documents are divided into smaller chunks for better embedding and retrieval.

```python
from langchain_text_splitters import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=50
)

chunks = splitter.split_documents(document)
```

### Why Chunking?

Chunking helps:

* Improve retrieval accuracy
* Reduce token usage
* Make embeddings more meaningful
* Handle large PDFs efficiently

---

# 🧠 Step 3 — Generate Embeddings

The notebook uses Hugging Face embeddings.

```python
from langchain_community.embeddings import HuggingFaceEmbeddings

embedding_model = HuggingFaceEmbeddings(
    model_name="sentence-transformers/all-MiniLM-L6-v2"
)
```

### Model Used

`sentence-transformers/all-MiniLM-L6-v2`

This is a lightweight and fast sentence embedding model.

---

# 🗄️ Step 4 — Store Embeddings in ChromaDB

```python
from langchain_community.vectorstores import Chroma

vector_db = Chroma.from_documents(
    documents=chunks,
    embedding=embedding_model,
    persist_directory="chroma_db"
)
```

The vector database stores:

* Document chunks
* Embeddings
* Metadata

---

# 💾 Step 5 — Persist the Database

```python
vector_db.persist()
```

This saves the embeddings locally so they can be reused later.

---

# 🔍 Step 6 — Perform Similarity Search

```python
query = "What is this PDF about?"

results = vector_db.similarity_search(query, k=10)

for result in results:
    print(result.page_content)
```

The vector database retrieves the most semantically relevant chunks related to the query.

---

# 📚 What You Learn From This Project

This notebook teaches the foundation of modern RAG systems:

* Document ingestion
* Text chunking strategies
* Embedding generation
* Vector databases
* Semantic search
* LangChain workflow

---

# ⚠️ Common Errors

## 1. ONNX Runtime Error

If you get:

```text
onnxruntime has no wheel for your Python version
```

Use:

* Python 3.11
* Python 3.12
* Python 3.13

Avoid older Python versions when using the latest embedding packages.

---

## 2. Windows Path Error

Use raw string paths:

```python
r"D:\folder\file.pdf"
```

or double backslashes:

```python
"D:\\folder\\file.pdf"
```

---

# 🔮 Future Improvements

You can extend this project by adding:

* LLM integration
* Conversational memory
* Streamlit frontend
* FastAPI backend
* Hybrid search
* Metadata filtering
* Multi-PDF support
* Chat with PDF functionality

---

# 🎯 Next Step

The next logical step is building a complete:

```text
Chat With PDF Application
```

using:

* LangChain
* ChromaDB
* OpenAI / Ollama / Gemini
* Streamlit or React frontend

---

# 👨‍💻 Author

Built as a beginner RAG learning project using LangChain and ChromaDB.
