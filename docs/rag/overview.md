# RAG (Retrieval-Augmented Generation)

IdeaWeaver provides comprehensive RAG capabilities for building knowledge-based AI systems. The RAG system supports both traditional and agentic approaches, with multiple vector store options and advanced evaluation features.

## Key Features

- **Multiple Vector Stores**: Support for Chroma, Qdrant (local and cloud)
- **Advanced Embeddings**: Sentence Transformers, OpenAI, and custom models
- **Document Processing**: PDF, DOCX, TXT, Markdown with smart chunking
- **Evaluation**: RAGAS framework for comprehensive assessment
- **Agentic RAG**: Multi-step reasoning with tool integration

## Qdrant Integration

IdeaWeaver provides seamless integration with Qdrant, a high-performance vector database. You can setup:

1. **Qdrant Cloud**: For production deployments with managed service

### Using Qdrant Local

### Using Qdrant Cloud
```bash
# Set Qdrant Cloud credentials as environment variables
export QDRANT_URL="your-cloud-url"
export QDRANT_API_KEY="your-api-key"

ideaweaver rag create-kb --name cloud-kb \
    --vector-store qdrant_cloud \
    --qdrant-url "$QDRANT_URL" \
    --qdrant-api-key "$QDRANT_API_KEY" \
    --description "Cloud Qdrant knowledge base"
```

> **Note**: For security reasons, never commit API keys or sensitive URLs to version control. Use environment variables or secure secret management systems.

### Qdrant Features
- High-performance vector search
- Scalable architecture
- Advanced filtering capabilities
- Payload support for metadata
- Real-time updates

## RAG Architecture

![RAG Architecture](../images/agent.png)



## Getting Started

1. Create a knowledge base:
```bash
ideaweaver rag create-kb --name my-kb --description "My first knowledge base"
```

2. Ingest documents:
```bash
ideaweaver rag ingest --kb my-kb --source ./docs --file-types md,pdf
```

3. Query the knowledge base:
```bash
ideaweaver rag query --kb my-kb -q "What are the main features?"
```

4. Evaluate the RAG system:
```bash
ideaweaver rag evaluate --kb my-kb
```

## Next Steps

- [RAG Commands](commands.md) - Complete command reference
- [RAG Evaluation](evaluation.md) - Evaluation and benchmarking
- [Enterprise RAG Guide](../guides/enterprise-rag.md) - Production deployments 