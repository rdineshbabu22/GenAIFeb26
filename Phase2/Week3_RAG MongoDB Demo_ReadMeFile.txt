# RAG MongoDB Demo

A comprehensive Retrieval-Augmented Generation (RAG) system for healthcare test cases and user stories, powered by MongoDB Atlas Vector Search. This demo showcases advanced search capabilities combining semantic vector search, keyword-based BM25 search, and AI-powered reranking for managing healthcare-related test cases and user stories.

## Features

- **Multi-Modal Search**: Vector (semantic), BM25 (keyword), and Hybrid search strategies
- **AI-Powered Processing**: Query preprocessing with abbreviation expansion and synonym mapping
- **Intelligent Reranking**: LLM-based result reranking and summarization using Groq
- **Real-Time Processing**: Batch embedding generation with progress tracking
- **Web Interface**: React-based UI for all operations (data conversion, search, settings)
- **Healthcare Domain**: Specialized for hospital/ward management test cases and user stories
- **Flexible Configuration**: Environment-based settings for different AI providers

## Architecture

### Client-Server Architecture

- **Frontend**: React application with Material-UI components
- **Backend**: Node.js Express server with REST APIs
- **Database**: MongoDB Atlas with Vector Search indexes
- **AI Services**: Mistral for embeddings, Groq for reranking/summarization

### Data Flow Pipeline

1. **Data Ingestion**: Excel files → JSON conversion → Embedding generation
2. **Query Processing**: Normalization → Abbreviation expansion → Synonym expansion
3. **Search Execution**: Parallel vector/BM25/hybrid searches with metadata filtering
4. **Result Refinement**: Deduplication → LLM reranking → Summarization

## Technology Stack

### Backend
- Node.js with ES modules
- Express.js server
- MongoDB Atlas Vector Search
- Mistral AI (embeddings)
- Groq (reranking/summarization)

### Frontend
- React 19 with React Router
- Material-UI (MUI) components
- Axios for API calls

### Key Libraries
- XLSX for Excel processing
- Multer for file uploads
- Concurrently for dev workflow

## Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd rag-mongo-demo-v8
   ```

2. **Install dependencies**
   ```bash
   npm install
   cd client && npm install && cd ..
   ```

3. **Configure environment**
   ```bash
   cp .env.example .env
   # Edit .env with your API keys and MongoDB connection
   ```

## Configuration

### Required Environment Variables

```env
# MongoDB Configuration
MONGODB_URI=mongodb+srv://...
DB_NAME=db_stories_tests
COLLECTION_NAME=test_cases
VECTOR_INDEX_NAME=vector_index
BM25_INDEX_NAME=bm25_index

# AI Services
MISTRAL_API_KEY=your_mistral_key
GROQ_API_KEY=your_groq_key

# Optional
OPENAI_API_KEY=your_openai_key
HUGGINGFACE_API_KEY=your_hf_key
```

### MongoDB Setup

1. Create MongoDB Atlas cluster with Vector Search enabled
2. Create vector index on `embedding` field (1384 dimensions, cosine similarity)
3. Create BM25 search index with field weights:
   - title: 8
   - module: 5
   - description: 2
   - expectedResults: 1.5
   - steps: 1

## Usage

### Development

```bash
# Start both client and server
npm run dev
```

- Client: http://localhost:3000
- Server: http://localhost:3001

### Production

```bash
# Build and start
npm run build
npm run server
```

### Data Loading Workflow

1. **Convert Data**: Use "Convert to JSON" tab to upload Excel files
2. **Generate Embeddings**: Use "Embeddings Store" to create vector embeddings
3. **Search**: Use various search interfaces (BM25, Vector, Hybrid, Reranking)

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/upload-excel` | Upload Excel files |
| POST | `/api/create-embeddings-batch` | Generate embeddings |
| POST | `/api/search` | Vector search |
| POST | `/api/search/bm25` | BM25 search |
| POST | `/api/search/hybrid` | Hybrid search |
| POST | `/api/search/rerank` | Reranked search |
| GET | `/api/jobs/:id` | Job status |

## Project Structure

```
rag-mongo-demo-v8/
├── client/                 # React frontend
│   ├── src/components/     # React components
│   └── public/            # Static assets
├── server/                # Express backend
│   └── index.js          # Main server file
├── src/                   # Shared/server scripts
│   ├── scripts/          # CLI tools and utilities
│   │   ├── data-conversion/  # Excel → JSON
│   │   ├── embeddings/      # Embedding generation
│   │   ├── query-preprocessing/  # Query processing
│   │   └── search/         # Search algorithms
│   └── config/           # Index configurations
├── releases/             # Version releases
└── uploads/             # File upload directory
```

## Key Components

### Search Strategies
- **BM25**: Keyword-based with field weighting
- **Vector**: Semantic similarity using embeddings
- **Hybrid**: Weighted combination of BM25 + Vector
- **Reranking**: LLM-based relevance scoring

### Query Preprocessing
- Text normalization and cleaning
- Healthcare abbreviation expansion (UHID, AHC, EMR, etc.)
- Synonym expansion for query variations

### AI Integration
- **Mistral**: 1384-dimension embeddings
- **Groq**: Llama models for reranking and summarization
- Support for OpenAI and Hugging Face alternatives

## Contributing

This is a demonstration project. For contributions:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

[Add appropriate license information]

## Dependencies

### External Services
- MongoDB Atlas (Vector Search enabled)
- Mistral AI API
- Groq API
- Optional: OpenAI, Hugging Face

### System Requirements
- Node.js 18+
- 2GB RAM minimum
- Internet connection for AI APIs</content>
<parameter name="filePath">c:\Users\rdine\Downloads\rag-mongo-demo-v8\rag-mongo-demo-v8\README.md