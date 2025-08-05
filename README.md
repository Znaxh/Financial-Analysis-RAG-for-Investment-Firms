# Financial Analysis RAG for Investment Firms

A comprehensive Retrieval-Augmented Generation (RAG) system designed specifically for investment firms to analyze financial documents, market data, and provide intelligent insights for investment decisions.

## 🚀 Features

### Core Capabilities
- **Document Processing**: Upload and process various financial documents (PDFs, Word docs, Excel files, etc.)
- **Financial Data Integration**: Real-time market data from multiple sources (Yahoo Finance, Alpha Vantage, etc.)
- **Intelligent Chat Interface**: RAG-powered conversational AI for financial analysis
- **Vector Search**: Semantic search across financial documents and data
- **Multi-source Context**: Combines document content with live financial data

### Financial Data Sources
- Stock prices and historical data
- Company fundamentals and financials
- Analyst recommendations
- Earnings data and reports
- Market indices and economic indicators

### Document Types Supported
- PDF reports and research documents
- Excel spreadsheets and financial models
- Word documents and presentations
- CSV data files
- HTML web content

## 🏗️ Architecture

```
├── src/
│   ├── api/                 # FastAPI routes and schemas
│   ├── core/               # Core components (database, vector store)
│   ├── data/               # Data processing and fetching
│   └── services/           # Business logic and RAG service
├── tests/                  # Test suite
├── scripts/               # Utility scripts
├── data/                  # Data storage
├── models/                # ML models (if any)
└── notebook/              # Jupyter notebooks for analysis
```

## 🛠️ Technology Stack

- **Backend**: FastAPI, Python 3.11+
- **Database**: PostgreSQL, SQLAlchemy ORM
- **Vector Database**: ChromaDB
- **Embeddings**: Sentence Transformers
- **LLM**: OpenAI GPT-3.5/4
- **Financial APIs**: Yahoo Finance, Alpha Vantage
- **Containerization**: Docker, Docker Compose
- **Testing**: Pytest, Coverage

## 📋 Prerequisites

- Python 3.11 or higher
- Docker and Docker Compose (for containerized deployment)
- OpenAI API key
- Optional: Alpha Vantage API key, other financial data API keys

## 🚀 Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/Financial-Analysis-RAG-for-Investment-Firms.git
cd Financial-Analysis-RAG-for-Investment-Firms
```

### 2. Setup Environment
```bash
# Run the setup script
python scripts/setup.py

# Or manually:
pip install -r requirements.txt
cp .env.example .env
# Edit .env with your API keys
```

### 3. Configure Environment Variables
Edit the `.env` file with your API keys:
```env
OPENAI_API_KEY=your_openai_api_key_here
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_key_here
DATABASE_URL=postgresql://username:password@localhost:5432/financial_rag
```

### 4. Run the Application

#### Option A: Local Development
```bash
python -m src.main
```

#### Option B: Docker Compose
```bash
docker-compose up -d
```

The API will be available at `http://localhost:8000`

## 📖 API Documentation

Once the application is running, visit:
- **Interactive API Docs**: `http://localhost:8000/docs`
- **ReDoc Documentation**: `http://localhost:8000/redoc`

### Key Endpoints

#### Financial Data
- `GET /api/v1/financial-data/stock/{symbol}/price` - Get stock price data
- `GET /api/v1/financial-data/stock/{symbol}/info` - Get company information
- `GET /api/v1/financial-data/stock/{symbol}/financials/{type}` - Get financial statements
- `GET /api/v1/financial-data/search` - Search for stock symbols

#### Document Management
- `POST /api/v1/documents/upload` - Upload documents
- `GET /api/v1/documents/` - List uploaded documents
- `POST /api/v1/documents/search` - Search documents
- `DELETE /api/v1/documents/{id}` - Delete documents

#### Chat Interface
- `POST /api/v1/chat/` - Send chat messages
- `GET /api/v1/chat/sessions/{session_id}/history` - Get chat history
- `DELETE /api/v1/chat/sessions/{session_id}` - Delete chat session

## 💡 Usage Examples

### 1. Upload Financial Documents
```python
import requests

files = {'file': open('quarterly_report.pdf', 'rb')}
response = requests.post('http://localhost:8000/api/v1/documents/upload', files=files)
```

### 2. Get Stock Data
```python
response = requests.get('http://localhost:8000/api/v1/financial-data/stock/AAPL/price?period=1y')
stock_data = response.json()
```

### 3. Chat with RAG System
```python
chat_data = {
    "message": "What are the key financial metrics for Apple?",
    "context_symbols": ["AAPL"],
    "use_documents": True
}
response = requests.post('http://localhost:8000/api/v1/chat/', json=chat_data)
```

## 🧪 Testing

Run the test suite:
```bash
# Run all tests with coverage
python scripts/run_tests.py

# Run only linting
python scripts/run_tests.py --lint-only

# Run specific tests
pytest tests/test_api.py -v
```

## 🔧 Configuration

### Environment Variables
See `.env.example` for all available configuration options.

### Database Configuration
The system supports both SQLite (for development) and PostgreSQL (for production):
```env
# SQLite (default)
DATABASE_URL=sqlite:///./financial_rag.db

# PostgreSQL
DATABASE_URL=postgresql://user:password@localhost:5432/financial_rag
```

### Vector Store Configuration
ChromaDB settings:
```env
CHROMA_PERSIST_DIRECTORY=./data/chroma_db
EMBEDDING_MODEL=sentence-transformers/all-MiniLM-L6-v2
```

## 📊 Monitoring and Logging

- Health checks available at `/health/` and `/health/detailed`
- Structured logging with configurable levels
- Prometheus metrics support (optional)

## 🚀 Deployment

### Docker Deployment
```bash
# Build and run with Docker Compose
docker-compose up -d

# Scale the application
docker-compose up -d --scale app=3
```

### Production Considerations
- Use PostgreSQL for the database
- Configure proper secrets management
- Set up reverse proxy (Nginx included)
- Enable HTTPS/TLS
- Configure monitoring and alerting

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines
- Follow PEP 8 style guidelines
- Write tests for new features
- Update documentation as needed
- Use type hints where appropriate

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- OpenAI for GPT models
- Hugging Face for embedding models
- The open-source community for various libraries and tools

## 📞 Support

For support, please open an issue on GitHub or contact the development team.

---

**Note**: This is a comprehensive financial analysis system. Please ensure you comply with all relevant financial regulations and data privacy requirements when using this system with real financial data.
