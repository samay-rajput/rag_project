# PDF RAG System with Ollama

A Retrieval-Augmented Generation (RAG) system that enables you to chat with PDF documents using local LLMs via Ollama. This project supports both regular PDFs and scanned PDFs through OCR processing.

## 🌟 Features

- **Hybrid PDF Processing**: Automatically switches between direct text extraction and OCR based on content quality
- **Local LLM Integration**: Uses Ollama for embedding and text generation (no API keys required)
- **Multi-language OCR Support**: Supports multiple languages including English, Hindi, Urdu, Bengali, Marathi, and Chinese
- **Vector Database**: Uses ChromaDB for efficient similarity search
- **Multi-Query Retrieval**: Generates multiple query variations to improve retrieval accuracy
- **Interactive Chat Interface**: Simple function to chat with your PDF documents

## 🛠 Technologies Used

- **LangChain**: For document processing, text splitting, and RAG pipeline
- **Ollama**: Local LLM inference and embeddings
- **ChromaDB**: Vector database for storing document embeddings
- **PyMuPDF**: Direct PDF text extraction
- **Tesseract OCR**: OCR processing for scanned PDFs
- **PDF2Image**: PDF to image conversion for OCR
- **Python Libraries**: Various supporting libraries for text processing and visualization

## 📋 Prerequisites

Before running this project, ensure you have:

1. **Python 3.8+** installed
2. **Ollama** installed on your system
3. **Tesseract OCR** installed (for scanned PDF support)
4. **Poppler** utilities (for PDF to image conversion)

### Installation Instructions

#### 1. Install Ollama
```bash
# On Linux/Mac
curl -fsSL https://ollama.com/install.sh | sh

# On Windows, download from: https://ollama.com/download
```

#### 2. Install Tesseract OCR
```bash
# Ubuntu/Debian
sudo apt-get update
sudo apt-get install -y tesseract-ocr poppler-utils

# For multiple language support
sudo apt-get install -y tesseract-ocr-hin tesseract-ocr-urd tesseract-ocr-ben tesseract-ocr-eng tesseract-ocr-mar tesseract-ocr-chi-sim

# Windows: Download from https://github.com/UB-Mannheim/tesseract/wiki
# Mac: brew install tesseract poppler
```

## 🚀 Quick Start

1. **Clone the repository**
```bash
git clone <your-repo-url>
cd rag_project
```

2. **Install Python dependencies**
```bash
pip install langchain_community langchain_ollama langchain_text_splitters langchain_core
pip install unstructured langchain langchain-community
pip install "unstructured[all-docs]" ipywidgets tqdm
pip install pymupdf pytesseract pdf2image Pillow chromadb
```

3. **Pull required Ollama models**
```bash
ollama pull nomic-embed-text
ollama pull llama3.2
```

4. **Open the Jupyter notebook**
```bash
jupyter notebook rag_notebook_ollama.ipynb
```

5. **Configure your PDF path**
   - Update the `pdf_file_path` variable in the notebook with your PDF file path
   - Set the appropriate `language_code` for OCR (e.g., 'eng', 'hin', 'urd')

6. **Run the cells sequentially** to:
   - Extract text from your PDF
   - Create vector embeddings
   - Set up the RAG pipeline
   - Start chatting with your document

## 📖 How It Works

### 1. Document Processing
The system uses a hybrid approach for PDF text extraction:
- **Direct Extraction**: First attempts to extract text directly from the PDF
- **OCR Fallback**: If insufficient text is found (< 100 words), switches to OCR processing
- **Language Support**: OCR supports multiple languages through Tesseract

### 2. Text Chunking
- Documents are split into manageable chunks (1000 characters with 200 character overlap)
- Ensures optimal retrieval performance and context preservation

### 3. Vector Database Creation
- Text chunks are converted to embeddings using Ollama's `nomic-embed-text` model
- Stored in ChromaDB for efficient similarity search

### 4. RAG Pipeline
- **Multi-Query Retrieval**: Generates multiple query variations to improve retrieval
- **Context Injection**: Retrieved chunks are injected into the LLM prompt
- **Response Generation**: Uses Ollama's `llama3.2` model for final answer generation

## 💡 Usage Examples

```python
# Basic usage after running the setup cells
chat_with_pdf("Summarize the document.")
chat_with_pdf("What are the main topics discussed?")
chat_with_pdf("Explain the methodology used in this paper.")
```

## 🔧 Configuration Options

### PDF Processing
- `pdf_file_path`: Path to your PDF file
- `language_code`: Language for OCR ('eng', 'hin', 'urd', etc.)
- `min_word_threshold`: Minimum word count for direct extraction (default: 100)

### Text Chunking
- `chunk_size`: Size of text chunks (default: 1000)
- `chunk_overlap`: Overlap between chunks (default: 200)

### Models
- `embedding_model`: Ollama embedding model (default: "nomic-embed-text")
- `llm_model`: Ollama chat model (default: "llama3.2")

## 📁 Project Structure

```
rag_project/
├── rag_notebook_ollama.ipynb    # Main Jupyter notebook
├── README.md                    # This file
└── [your_pdf_files]            # Place your PDF files here
```

## 🔍 Key Functions

### `extract_text_from_pdf(pdf_path, language, min_word_threshold)`
Hybrid PDF text extraction function that automatically chooses between direct extraction and OCR.

### `extract_text_with_ocr(pdf_path, language)`
OCR-based text extraction for scanned PDFs using Tesseract.

### `chat_with_pdf(question)`
Main chat interface function that processes questions and returns answers based on the PDF content.

## 🚨 Troubleshooting

### Common Issues

1. **Tesseract not found**
   - Ensure Tesseract is installed and in your system PATH
   - On Windows, you might need to specify the Tesseract path manually

2. **Ollama models not available**
   - Run `ollama pull nomic-embed-text` and `ollama pull llama3.2`
   - Check available models with `ollama list`

3. **Memory issues with large PDFs**
   - Reduce chunk size or increase overlap
   - Process PDFs in smaller sections

4. **Poor OCR quality**
   - Ensure PDF images are high resolution
   - Try different language codes
   - Consider preprocessing images for better OCR results

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [LangChain](https://langchain.com/) for the RAG framework
- [Ollama](https://ollama.com/) for local LLM inference
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) for OCR capabilities
- [ChromaDB](https://www.trychroma.com/) for vector storage

## 📞 Support

If you encounter any issues or have questions, please:
1. Check the troubleshooting section
2. Search existing issues in the repository
3. Create a new issue with detailed information about your problem

---

**Note**: This project runs entirely locally and doesn't require any external API keys or internet connection for inference (after initial model downloads).