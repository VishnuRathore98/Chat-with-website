
# 🦜 Chat-with-Website

An intelligent web chatbot that allows you to have natural conversations with any website's content using AI-powered semantic search and language models.

## 📋 Overview

**Chat-with-Website** is a Streamlit-based application that enables users to interact with website content through natural language queries. It leverages advanced LLM (Large Language Model) technology combined with vector embeddings to understand and answer questions about any webpage.

### Key Features

- **Web Content Loading**: Automatically fetch and process content from any URL
- **Semantic Search**: Convert text into vector embeddings for intelligent content retrieval
- **AI-Powered Responses**: Uses Deepseek-R1 LLM to generate contextual answers
- **User-Friendly Interface**: Built with Streamlit for an intuitive web UI
- **Context-Aware Answers**: Maintains webpage context when answering questions
- **Efficient Chunking**: Splits large documents into manageable chunks with overlap for better context

## 🛠️ Tech Stack

- **Framework**: [Streamlit](https://streamlit.io/) - Web UI framework
- **LLM**: [Deepseek-R1:1.5b](https://ollama.ai/) - Language model for generating responses
- **Embeddings**: [MXbai-Embed-Large](https://ollama.ai/) - Vector embeddings model
- **Vector Database**: [FAISS](https://github.com/facebookresearch/faiss) - Fast similarity search
- **Document Processing**: [LangChain](https://www.langchain.com/) - LLM orchestration framework
- **Web Scraping**: [BeautifulSoup 4](https://www.crummy.com/software/BeautifulSoup/) - HTML parsing

## 📦 Installation

### Prerequisites

- Python 3.8 or higher
- [Ollama](https://ollama.ai/) installed and running locally
- pip package manager

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/VishnuRathore98/Chat-with-website.git
   cd Chat-with-website
   ```

2. **Create a virtual environment (recommended)**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Ensure Ollama is running**
   ```bash
   # Pull required models
   ollama pull deepseek-r1:1.5b
   ollama pull mxbai-embed-large
   
   # Start Ollama service (if not already running)
   ollama serve
   ```

5. **Run the application**
   ```bash
   streamlit run app.py
   ```

   The app will open in your default browser at `http://localhost:8501`

## 🚀 Usage

1. **Start the application** using the command above
2. **Enter a website URL** in the sidebar input field (e.g., `https://example.com`)
3. **Ask questions** about the website content in the main text input
4. **Receive AI-generated answers** based on the webpage content

### Example Workflow

```
URL Input: https://docs.python.org/3/library/functions.html
Question: What is the purpose of the len() function?
Answer: [AI generates a contextual response based on the documentation]
```

## 🔧 How It Works

### Architecture Flow

```
Website URL
    ↓
Web Loader (WebBaseLoader)
    ↓
Document Processing
    ↓
Text Chunking (RecursiveCharacterTextSplitter)
    ↓
Vector Embeddings (MXbai-Embed-Large)
    ↓
FAISS Vector Store
    ↓
Retrieval Chain
    ↓
LLM (Deepseek-R1:1.5b)
    ↓
Response Parser & Display
```

### Key Components

1. **WebBaseLoader**: Fetches HTML content from the provided URL
2. **RecursiveCharacterTextSplitter**: Divides documents into 1000-character chunks with 200-character overlap
3. **OllamaEmbeddings**: Converts text chunks into vector representations
4. **FAISS**: Stores and retrieves similar vectors for context matching
5. **ChatPromptTemplate**: Structures prompts for the LLM
6. **Ollama LLM**: Generates natural language responses
7. **Output Parser**: Cleans up model responses (removes thinking tags)

## 📄 Dependencies

| Package | Purpose |
|---------|---------|
| `streamlit` | Web UI framework |
| `langchain` | LLM orchestration |
| `langchain_community` | Pre-built integrations |
| `langchain_core` | Core LangChain utilities |
| `langchain_text_splitters` | Document chunking |
| `bs4` (BeautifulSoup4) | HTML/XML parsing |
| `faiss-cpu` | Vector search database |
| `ollama` | Local LLM integration |

## ⚙️ Configuration

The application uses the following default configurations:

- **Embedding Model**: `mxbai-embed-large`
- **Language Model**: `deepseek-r1:1.5b`
- **Chunk Size**: 1000 characters
- **Chunk Overlap**: 200 characters
- **Vector Store**: FAISS

To use different models, modify the model names in `app.py`:

```python
embeddings = OllamaEmbeddings(model="your-model-name")
llm = Ollama(model="your-llm-name")
```

## 🎯 Use Cases

- **Documentation Search**: Query technical documentation dynamically
- **Research Tool**: Extract information from research papers and web content
- **FAQ Assistant**: Answer questions about specific web pages
- **Learning Tool**: Interactive learning from online educational content
- **Content Analysis**: Understand and discuss website topics

## ⚠️ Limitations

- Requires Ollama to be running locally
- Processing time depends on webpage size and model performance
- Limited to publicly accessible URLs
- Performance varies with hardware specifications
- Model responses are limited to the context provided

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| "Connection refused" error | Ensure Ollama is running (`ollama serve`) |
| Model not found | Pull required models: `ollama pull deepseek-r1:1.5b` |
| Slow responses | Use a faster model or increase hardware resources |
| Invalid URL error | Verify the URL is accessible and properly formatted |
| Out of memory | Reduce chunk size or use a lighter model |

## 🔐 Security Considerations

- Only process content from trusted URLs
- The application doesn't store any data by default
- Keep Ollama service restricted to localhost in production
- Be cautious with sensitive website data

## 🚧 Future Enhancements

- [ ] Support for multiple URLs in one session
- [ ] Document upload functionality
- [ ] Conversation history persistence
- [ ] Model selection interface
- [ ] Response caching
- [ ] API integration support
- [ ] Multi-language support


## 💡 Tips & Best Practices

1. **Optimal Performance**: Use URLs with well-structured text content
2. **Query Specificity**: Ask specific questions for better answers
3. **Model Selection**: Experiment with different models for quality vs. speed trade-offs
4. **Resource Management**: Monitor system resources when processing large websites

---
