# YouTube-Chatbot-using-LangChain
# 🎬 YouTube Chatbot with LangChain

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/yourusername/youtube-chatbot.svg)](https://github.com/yourusername/youtube-chatbot)
[![GitHub forks](https://img.shields.io/github/forks/yourusername/youtube-chatbot.svg)](https://github.com/yourusername/youtube-chatbot/fork)

An intelligent chatbot that extracts transcripts from YouTube videos and answers questions about their content using LangChain and OpenAI's powerful language models.

## ✨ Features

- 🎥 **Automatic Transcript Extraction** - Pulls transcripts directly from YouTube videos
- 🤖 **AI-Powered Q&A** - Ask questions and get instant answers about video content
- 📚 **Source Attribution** - Know exactly which parts of the video your answer came from
- 🔍 **Smart Chunking** - Intelligently splits content for optimal processing
- 🧠 **Vector Embeddings** - Uses OpenAI embeddings for semantic search
- 💾 **FAISS Database** - Fast similarity search across video content
- 🌐 **Web Interface** - Beautiful Streamlit UI for easy interaction
- 💻 **CLI Support** - Command-line interface for advanced users
- 💬 **Chat History** - Maintains conversation context
- ⚙️ **Customizable** - Easy configuration for different use cases

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- OpenAI API key ([Get one here](https://platform.openai.com/api-keys))
- Internet connection

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/youtube-chatbot.git
cd youtube-chatbot
```

2. **Create virtual environment (recommended)**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set up environment variables**
Create a `.env` file in the project root:
```env
OPENAI_API_KEY=sk-your_api_key_here
```

### Usage

#### Web Interface (Recommended) 🌐
```bash
streamlit run youtube_chatbot_complete.py
```
Open your browser to `http://localhost:8501`

#### Command Line 💻
```bash
python youtube_chatbot_complete.py
```

## 📖 How It Works

```
YouTube Video URL
    ↓
📥 Extract Transcript (via youtube-transcript-api)
    ↓
✂️ Split into Chunks (RecursiveCharacterTextSplitter)
    ↓
🧠 Create Embeddings (OpenAI Embeddings API)
    ↓
🗄️ Store in Vector DB (FAISS)
    ↓
💬 User Asks Question
    ↓
🔍 Semantic Search (Retrieve top 3 chunks)
    ↓
🤖 Generate Answer (GPT-3.5-turbo / GPT-4)
    ↓
📝 Return Answer + Sources
```

## 💡 Example Usage

### Web Interface
1. Paste a YouTube URL in the sidebar
2. Click "Load Video"
3. Ask your questions in the chat box
4. Get instant answers with source references

### Questions You Can Ask
- "What is this video about?"
- "Summarize the key points"
- "Explain [concept] mentioned in the video"
- "What are the main takeaways?"
- "Who are the speakers?"

### Supported Videos
✅ TED Talks  
✅ Educational tutorials  
✅ Lectures and conferences  
✅ News segments  
✅ Podcasts with transcripts  
✅ Any video with captions/subtitles

## ⚙️ Configuration

Edit the `CONFIG` dictionary in `youtube_chatbot_complete.py`:

```python
CONFIG = {
    "chunk_size": 1000,           # Size of text chunks
    "chunk_overlap": 200,         # Overlap between chunks
    "temperature": 0.7,           # 0=factual, 1=creative
    "model": "gpt-3.5-turbo",     # or "gpt-4"
    "k_retrieval": 3,             # Number of sources to retrieve
}
```

### Configuration Options

| Option | Default | Description |
|--------|---------|-------------|
| `chunk_size` | 1000 | Characters per chunk (smaller = more precise) |
| `chunk_overlap` | 200 | Character overlap between chunks |
| `temperature` | 0.7 | LLM creativity (0=factual, 1=creative) |
| `model` | gpt-3.5-turbo | OpenAI model to use |
| `k_retrieval` | 3 | Number of chunks to use for context |

## 📊 Architecture

### Core Components

1. **YoutubeLoader** - Extracts transcripts from YouTube videos
2. **RecursiveCharacterTextSplitter** - Intelligently splits text into chunks
3. **OpenAIEmbeddings** - Creates vector embeddings for semantic search
4. **FAISS** - Vector database for fast similarity search
5. **RetrievalQA** - Combines retrieval and generation for Q&A
6. **LangChain** - Orchestrates all components

### Tech Stack

- **Backend**: LangChain, OpenAI API
- **Vector DB**: FAISS
- **Frontend**: Streamlit (Web UI)
- **CLI**: Pure Python
- **Environment**: Python 3.8+

## 💰 Cost Estimation

### OpenAI API Pricing
- GPT-3.5 Turbo: ~$0.0005 per 1K tokens
- Embeddings: ~$0.0001 per 1K tokens

### Per Video Cost
- Short video (5-10 min): $0.01 - $0.05
- Medium video (30-60 min): $0.05 - $0.15
- Long video (2+ hours): $0.20 - $0.50

**💡 Tip**: Use GPT-3.5 Turbo (default) for best cost-performance ratio

## 🐛 Troubleshooting

### Common Issues

**Error: "OPENAI_API_KEY not found"**
- Create `.env` file with your API key
- Verify the key is active on [OpenAI dashboard](https://platform.openai.com)

**Error: "Video has no transcripts"**
- Video must have captions/subtitles enabled on YouTube
- Try a different video

**Error: "No module named langchain"**
```bash
pip install -r requirements.txt
```

**Slow Processing**
- Try shorter videos first
- Reduce `chunk_size` to 500-800
- Use GPT-3.5-turbo instead of GPT-4

### Getting Help

1. Check [Issues](https://github.com/yourusername/youtube-chatbot/issues)
2. Read the [FAQ](docs/FAQ.md)
3. Create a new issue with details

## 📁 Project Structure

```
youtube-chatbot/
├── youtube_chatbot_complete.py     # Main chatbot code
├── requirements.txt                 # Python dependencies
├── .env.example                     # Example environment file
├── .gitignore                       # Git ignore rules
├── README.md                        # This file
├── LICENSE                          # MIT License
├── CONTRIBUTING.md                  # Contributing guidelines
├── docs/
│   ├── INSTALLATION.md             # Detailed installation guide
│   ├── CONFIGURATION.md            # Configuration guide
│   ├── API.md                      # API documentation
│   └── FAQ.md                      # Frequently asked questions
├── examples/
│   ├── example_questions.txt       # Example questions
│   └── sample_videos.txt           # Sample video URLs
└── tests/
    └── test_chatbot.py             # Unit tests
```

## 🔧 Development

### Setting Up Development Environment

```bash
# Clone repo
git clone https://github.com/yourusername/youtube-chatbot.git
cd youtube-chatbot

# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install dependencies with dev tools
pip install -r requirements-dev.txt

# Install pre-commit hooks
pre-commit install
```

### Running Tests

```bash
pytest tests/
```

### Code Style

- Follow PEP 8
- Use type hints
- Document functions with docstrings
- Max line length: 88 characters

## 🤝 Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

## 🙋 Support

- **Documentation**: [docs/](docs/)
- **Issues**: [GitHub Issues](https://github.com/yourusername/youtube-chatbot/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/youtube-chatbot/discussions)

## 🔐 Security

⚠️ **IMPORTANT**: Never commit your `.env` file to version control!

- Add `.env` to `.gitignore` (already included)
- Use environment variables for API keys
- Keep your API keys confidential
- Rotate keys if accidentally exposed

## 🙏 Acknowledgments

- [LangChain](https://python.langchain.com/) - Language model orchestration
- [OpenAI](https://openai.com/) - Powerful language models
- [FAISS](https://faiss.ai/) - Efficient similarity search
- [Streamlit](https://streamlit.io/) - Web app framework
- [youtube-transcript-api](https://github.com/jdeepd/youtube-transcript-api) - Transcript extraction

## 📈 Roadmap

- [ ] Support for multiple languages
- [ ] Video segment timestamps in answers
- [ ] Save conversations to database
- [ ] Export Q&A as PDF
- [ ] Multi-video search across multiple videos
- [ ] Custom LLM support (Anthropic, Cohere, etc.)
- [ ] Web API deployment
- [ ] Browser extension
- [ ] Mobile app

## 💬 Feedback

Have ideas or found bugs? Please [create an issue](https://github.com/yourusername/youtube-chatbot/issues)!

---

**Made with ❤️ by [Your Name]**

⭐ If this project helped you, please give it a star!

[![forthebadge](https://forthebadge.com/images/badges/made-with-python.svg)](https://www.python.org/)
