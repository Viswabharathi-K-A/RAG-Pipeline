📚 Retrieval-Augmented Generation (RAG) Pipeline
PDF → Chunks → Embeddings → Vector DB → LLM

This project implements a complete Retrieval-Augmented Generation (RAG) pipeline inside a single Jupyter Notebook:
notebooks/RAG_pipeline.ipynb.

The notebook demonstrates the full workflow:

📄 Load PDFs

✂️ Split text into chunks

🤖 Generate embeddings

🗄️ Store them in ChromaDB

🔍 Convert query to embeddings

📈 Retrieve relevant chunks using cosine similarity

🧠 Use Groq LLM (llama-3.1-8b-instant) for grounded answers

This is a simple, transparent, and educational implementation of RAG.

📁 Project Structure
.
├── data/
│   ├── pdfs/                 # Input PDF documents
│   └── vector_store/         # ChromaDB persistent storage
│
├── notebooks/
│   └── RAG_pipeline.ipynb    # Complete RAG pipeline in one notebook
│
├── requirements.txt
└── README.md


Everything—PDF loading, chunking, embeddings, vector storage, retrieval, and LLM answering—is implemented inside one notebook.

🔧 Pipeline Breakdown
1️⃣ PDF Loading (📄 → 📝)

PDFs in data/pdfs/ are loaded using PyMuPDF or PyPDF, and raw text is extracted for processing.

2️⃣ Text Chunking (✂️ → 📦)

Uses RecursiveCharacterTextSplitter to break large text into meaningful chunks.

Default settings:

chunk_size = 1000

chunk_overlap = 200

Chunking improves context retrieval and reduces information loss.

3️⃣ Embedding Generation (🧬)

A SentenceTransformers model (e.g., all-MiniLM-L6-v2) converts:

Document chunks → embedding vectors

Query → vector representation

Both use the same embedding model to ensure consistent similarity scoring.

4️⃣ Vector Store (🗄️ ChromaDB)

Stores embeddings and metadata persistently in:

data/vector_store/


Stored items include:

Chunk text

Embedding vector

Metadata (file name, page number, etc.)

5️⃣ Retrieval (🔍 Cosine Similarity)

The notebook implements a custom similarity-based retriever:

Embed the query

Compute cosine similarity against all chunk embeddings

Rank chunks by similarity score

Return the top-k relevant chunks

This provides full transparency into the retrieval logic.

6️⃣ LLM Answer Generation (🤖 → 🧠)

The relevant chunks and the user query are sent to Groq LLM (gemma2-9b-it) using LangChain.

Prompt template used:

Use the following context to answer the question concisely.

Context:
{retrieved_chunks}

Question:
{query}

Answer:


The final output is grounded in your private documents.

▶️ How to Run the Project:

1️⃣ Create & activate a virtual environment
uv venv
source .venv/bin/activate        # Linux/Mac
.\.venv\Scripts\activate         # Windows

2️⃣ Install dependencies
uv add -r requirements.txt

3️⃣ Launch Jupyter
jupyter notebook
or
jupyter lab

4️⃣ Add your PDFs
Place your files in:
data/pdfs/

5️⃣ Run RAG_pipeline.ipynb

The notebook will:
Extract text <br>
Create chunks <br>
Generate embeddings <br>
Populate ChromaDB <br>
Accept your queries <br>
Retrieve relevant context <br>
Produce an LLM-powered response <br>

📦 Requirements
Example requirements.txt:

langchain
langchain-core
langchain-community
langchain-text-splitters
langchain-groq
chromadb
sentence-transformers
pymupdf
pypdf
python-dotenv

⭐ Features

📓 All logic in a single easy-to-understand notebook

🔍 Transparent retrieval (you can see how similarity is calculated)

🗂️ Persistent vector store using ChromaDB

⚡ Fast inference using Groq LLM

🧪 End-to-end RAG system for experimentation


