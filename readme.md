# Multi-Tool Agentic AI Assistant

A powerful Streamlit-based conversational AI agent that leverages multiple data sources and tools to provide intelligent responses using LangChain and Groq LLM.

---

## Features

- **Multi-Source Information Retrieval** - Access information from Wikipedia, ArXiv, web URLs, PDFs, and text files
- **RAG (Retrieval Augmented Generation)** - Intelligent document search using FAISS vector stores
- **Interactive Chat Interface** - Clean, professional UI with chat history
- **Agentic Workflow** - Autonomous agent that selects appropriate tools based on user queries
- **Real-time Processing** - Fast responses powered by Groq's Llama 3.1 model

---

## Available Tools

1. **Wikipedia Search** - Query Wikipedia for general knowledge
2. **ArXiv Research** - Access academic papers and research documents
3. **Web Content Retrieval** - Extract information from specific URLs
4. **PDF Document Search** - Search through uploaded PDF documents
5. **Personal Information Retrieval** - Query custom text files

---

## Prerequisites

- Python 3.8 or higher
- Groq API Key (Get it from https://console.groq.com/)
- Internet connection for web-based tools

---

## Installation

### Step 1: Clone the repository

```bash
git clone <repository-url>
cd Multi_Source_Rag_App
```

### Step 2: Create a virtual environment

```bash
python -m venv venv
source venv/bin/activate
```

On Windows:
```bash
venv\Scripts\activate
```

### Step 3: Install required packages

```bash
pip install -r requirements.txt
```

### Step 4: Create a .env file (optional)

```bash
echo "groq_api_key=your_api_key_here" > .env
```

---

## Dependencies

Create a `requirements.txt` file with the following content:

```
streamlit
langchain
langchain-community
langchain-groq
langchain-huggingface
python-dotenv
faiss-cpu
arxiv
wikipedia
duckduckgo-search
pypdf
sentence-transformers
```

---

## Project Structure

```
Multi_Source_Rag_App/
│
├── app.py                          # Main Streamlit application
├── requirements.txt                # Python dependencies
├── .env                           # Environment variables (API keys)
├── README.md                      # This file
│
├── Agent Quality Whitepaper.pdf   # Sample PDF document
└── about_me.txt                   # Sample text file
```

---

## Configuration

### Update File Paths

Before running the application, update the following file paths in `app.py`:

**PDF file path (around line 58):**
```python
loader = PyPDFLoader("path/to/your/pdf/file.pdf")
```

**Text file path (around line 65):**
```python
loader1 = TextLoader("path/to/your/text/file.txt")
```

**Web URL (around line 50) - Optional:**
```python
loader = WebBaseLoader('your_url_here')
```

### Customize Tool Descriptions

Modify tool descriptions in the code to match your specific documents:

```python
pdf_retriever_tool = create_retriever_tool(
    retriever, 
    "pdf_retriever_tool", 
    "Your custom description here"
)
```

---

## Usage

### Step 1: Start the application

```bash
streamlit run app.py
```

### Step 2: Enter your Groq API Key

Enter your API key in the sidebar when the application opens.

### Step 3: Start chatting

Type your questions in the chat input box.

### Example Queries

- "What is quantum computing?" (Wikipedia)
- "Find papers about neural networks" (ArXiv)
- "Tell me about Abhiram Kumar Soni" (Text file)
- "Summarize the agent quality whitepaper" (PDF)
- "What happened at IIT Kanpur?" (Web URL)

---

## Advanced Configuration

### Modify LLM Settings

Change the model or parameters in `app.py`:

```python
llm = ChatGroq(
    api_key=groq_key, 
    model="llama-3.1-8b-instant",  # Try: mixtral-8x7b-32768
    temperature=0.7,
    max_tokens=1024
)
```

### Adjust Vector Store Parameters

Customize chunk sizes for better retrieval:

```python
RecursiveCharacterTextSplitter(
    chunk_size=1000,      # Adjust based on your content
    chunk_overlap=200     # Increase for better context
)
```

### Change Embedding Model

Replace HuggingFace embeddings:

```python
HuggingFaceEmbeddings(
    model_name="sentence-transformers/all-MiniLM-L6-v2"
)
```

---

## Troubleshooting

### Common Issues

**ModuleNotFoundError**

```bash
pip install --upgrade -r requirements.txt
```

**API Key Error**

- Ensure your Groq API key is valid
- Check if the key is properly set in the sidebar or .env file

**File Not Found**

- Verify all file paths are correct and use absolute paths
- Ensure PDF and text files exist at specified locations

**FAISS Index Error**

```bash
pip install faiss-cpu --upgrade
```

---

## Customization

### Change UI Theme

Modify the CSS in the `st.markdown()` section of `app.py`:

```python
st.markdown("""
    <style>
    .stApp { 
        background-color: #your_color; 
        color: #your_text_color; 
    }
    </style>
""", unsafe_allow_html=True)
```

### Add New Tools

1. Import the tool at the top of `app.py`
2. Initialize it in the `get_agent_executor()` function
3. Add it to the `tools` list

---

## Security Notes

- Never commit your `.env` file or API keys to version control
- Add `.env` to your `.gitignore` file
- Use environment variables for sensitive information

---

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## Contact

For questions or feedback, please open an issue on GitHub.

---

## Acknowledgments

- LangChain for the agent framework
- Groq for fast LLM inference
- Streamlit for the web interface
- HuggingFace for embeddings

---

**Note:** Remember to update file paths and add your actual documents before running the application!