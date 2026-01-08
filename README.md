# PDF RAG System with Ollama

A production-ready Retrieval-Augmented Generation system for document question-answering using local LLMs. Implements hybrid PDF processing with automatic fallback from direct text extraction to OCR for scanned documents.

## Overview

This system enables semantic search and question-answering over PDF documents using a local-first approach. It combines LangChain's RAG framework with Ollama's local inference capabilities, supporting both machine-readable and scanned PDFs through intelligent processing pipeline selection.

## Architecture

- **Document Processing**: Hybrid extraction pipeline (PyMuPDF → OCR fallback)
- **Embeddings**: Ollama `nomic-embed-text` model for vector representations
- **Vector Store**: ChromaDB for similarity search and retrieval
- **Text Generation**: Ollama `llama3.2` for response synthesis
- **Retrieval**: Multi-query approach for improved context coverage

## Technical Stack

```
LangChain (RAG Framework)
├── Document Loaders: PyMuPDFLoader, OCR Pipeline
├── Text Splitters: RecursiveCharacterTextSplitter
├── Embeddings: OllamaEmbeddings
├── Vector Store: ChromaDB
├── Retrievers: MultiQueryRetriever
└── LLM: ChatOllama

OCR Pipeline
├── PDF2Image: High-DPI conversion
├── Tesseract: Multi-language OCR
└── Language Support: eng, hin, urd, ben, mar, chi-sim
```

## Setup

### Dependencies
```bash
# Core dependencies
pip install langchain_community langchain_ollama langchain_text_splitters langchain_core
pip install unstructured langchain chromadb pymupdf pytesseract pdf2image

# System dependencies (Ubuntu/Debian)
sudo apt-get install tesseract-ocr poppler-utils
```

### Ollama Models
```bash
ollama pull nomic-embed-text  # Embedding model
ollama pull llama3.2          # Language model
```

## Implementation

The notebook implements a complete RAG pipeline:

1. **Hybrid PDF Processing** - Automatic selection between direct extraction and OCR based on content quality metrics
2. **Chunking Strategy** - Recursive character splitting (1000 chars, 200 overlap)
3. **Vector Database** - ChromaDB with Ollama embeddings
4. **Multi-Query Retrieval** - Query expansion for improved recall
5. **Response Generation** - Context-aware synthesis using local LLM

## Key Functions

- `extract_text_from_pdf()` - Intelligent PDF processing with OCR fallback
- `extract_text_with_ocr()` - Multi-language OCR processing
- `chat_with_pdf()` - Main query interface

## Configuration

Core parameters:
- `chunk_size`: 1000 (characters)
- `chunk_overlap`: 200 (characters)  
- `min_word_threshold`: 100 (OCR trigger)
- `embedding_model`: "nomic-embed-text"
- `llm_model`: "llama3.2"
