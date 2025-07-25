# RAG with Multiple Data Sources Using LangChain

A comprehensive **Retrieval-Augmented Generation (RAG)** system that intelligently queries multiple knowledge sources using LangChain agents. This project demonstrates how to build a sophisticated AI assistant that can seamlessly switch between different data sources based on user queries.

## 🎯 Overview

This project implements a fully functional LangChain Agent that performs RAG across multiple knowledge sources:

- **Wikipedia Tool** - Real-time encyclopedia access
- **Arxiv Paper Search Tool** - Academic paper retrieval
- **LangSmith Documentation** - Web-based vector store integration

The system uses LangChain's agent capabilities with OpenAI's LLM to intelligently route queries to the most appropriate data source.

## 📂 Project Structure

```
RAG-WITH-MULTIPLE-DATA-SOURCES/
├── .env                    # API keys (OpenAI)
├── .gitignore             # Ignore venv, .env, __pycache__
├── agents.ipynb           # Main notebook for running agent
├── README.md              # Project documentation
├── requirements.txt       # Dependencies
└── venv/                  # Virtual environment (ignored)
```

## ✨ Key Features

### Intelligent Agent Architecture
- **Tool-based Agent**: Utilizes LangChain's `create_openai_tools_agent` for dynamic tool selection
- **Context-aware Routing**: Automatically chooses the best data source based on query context
- **Multi-modal Integration**: Seamlessly combines structured and unstructured data sources

### Advanced RAG Implementation
- **FAISS Vector Store**: High-performance similarity search for documentation
- **Document Processing**: Automated chunking with `RecursiveCharacterTextSplitter`
- **Semantic Embeddings**: OpenAI embeddings for accurate document retrieval

### External API Integration
- **Wikipedia API**: Instant access to encyclopedia entries
- **Arxiv API**: Academic paper metadata and abstracts
- **Web Content Loading**: Dynamic documentation scraping and indexing

## 🛠 Technical Stack

| Component | Technology |
|-----------|------------|
| **LLM Framework** | LangChain |
| **Language Model** | OpenAI GPT-3.5 Turbo |
| **Vector Database** | FAISS |
| **Embeddings** | OpenAI Embeddings |
| **External APIs** | Wikipedia, Arxiv |
| **Document Processing** | WebBaseLoader, RecursiveCharacterTextSplitter |

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- OpenAI API key
- Git

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/rag-multi-agent-langchain.git
   cd rag-multi-agent-langchain
   ```

2. **Create and activate virtual environment**
   ```bash
   # Linux/Mac
   python -m venv venv
   source venv/bin/activate
   
   # Windows
   python -m venv venv
   venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   
   Create a `.env` file in the root directory:
   ```env
   OPENAI_API_KEY=your_openai_api_key_here
   ```

### Usage

1. **Launch Jupyter Notebook**
   ```bash
   jupyter notebook agents.ipynb
   ```

2. **Run the agent**
   
   Execute the cells step-by-step, then try these example queries:
   
   ```python
   # Query LangSmith documentation
   response = agent_executor.invoke({
       "input": "Tell me about Langsmith's key features"
   })
   
   # Search for academic papers
   response = agent_executor.invoke({
       "input": "What's the paper 1605.08386 about?"
   })
   
   # General knowledge queries
   response = agent_executor.invoke({
       "input": "Explain quantum computing"
   })
   ```

## 🔧 Architecture Details

### Agent Workflow
1. **Query Analysis**: The agent analyzes the user's input to determine intent
2. **Tool Selection**: Based on context, it chooses between Wikipedia, Arxiv, or vector store
3. **Information Retrieval**: Executes the appropriate retrieval strategy
4. **Response Generation**: Synthesizes information into a coherent response

### Vector Store Creation
```python
# Document loading and processing
loader = WebBaseLoader(urls)
documents = loader.load()

# Text splitting for optimal chunking
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200
)
splits = text_splitter.split_documents(documents)

# Vector store creation
vectorstore = FAISS.from_documents(splits, OpenAIEmbeddings())
```

## 📊 Performance Considerations

- **Caching**: Implements intelligent caching for repeated queries
- **Chunking Strategy**: Optimized chunk sizes for better retrieval accuracy
- **Parallel Processing**: Concurrent API calls where possible
- **Memory Management**: Efficient vector store operations

## 🔒 Security & Best Practices

- **API Key Management**: Secure storage in environment variables
- **Rate Limiting**: Respectful API usage with built-in limits
- **Error Handling**: Robust error handling for external API failures
- **Data Privacy**: No sensitive data stored in version control

## 🚧 Future Enhancements

- [ ] **PDF Document Support** - Direct PDF parsing and indexing
- [ ] **Conversation Memory** - Multi-turn conversation context
- [ ] **Custom Data Sources** - Integration with proprietary databases
- [ ] **Web Interface** - Streamlit/Gradio deployment
- [ ] **Performance Monitoring** - Query analytics and optimization
- [ ] **Multi-language Support** - Internationalization capabilities

## 🤝 Contributing

We welcome contributions! Here's how you can help:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Commit your changes** (`git commit -m 'Add amazing feature'`)
4. **Push to the branch** (`git push origin feature/amazing-feature`)
5. **Open a Pull Request**

### Development Setup
```bash
# Install development dependencies
pip install -r requirements-dev.txt

# Run tests
pytest tests/

# Format code
black .
flake8 .
```

## 📈 Use Cases

- **Research Assistant**: Academic paper discovery and summarization
- **Documentation Helper**: Technical documentation queries
- **Knowledge Base**: General information retrieval
- **Educational Tool**: Multi-source learning assistance

## 🐛 Troubleshooting

### Common Issues

**OpenAI API Key Error**
```bash
# Ensure your .env file is properly configured
export OPENAI_API_KEY=your_key_here
```

**Dependencies Issues**
```bash
# Reinstall dependencies
pip install --upgrade -r requirements.txt
```

**Vector Store Performance**
```bash
# Clear cache and rebuild
rm -rf .faiss_cache/
```

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **LangChain Team** for the excellent framework
- **OpenAI** for powerful language models
- **FAISS** for efficient vector operations
- **Wikipedia & Arxiv** for open knowledge access

## 📧 Contact

**Chitraksh Suri**
- LinkedIn: [Connect with me](https://linkedin.com/in/chitrakshsuri)
- GitHub: [@chitrakshsuri](https://github.com/chitrakshsuri)
- Email: chitraksh.suri@example.com

---

*Built with ❤️ using LangChain and OpenAI*