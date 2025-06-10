# RAG Commands

## Knowledge Base Management

### Create Knowledge Base
```bash
ideaweaver rag create-kb --name my-kb --description "My knowledge base"
```

Options:

- `--name`: Knowledge base name (required)
- `--description`: Knowledge base description
- `--embedding-model`: Embedding model to use
- `--chunk-size`: Chunk size for text splitting
- `--chunk-overlap`: Overlap between chunks
- `--chunking-strategy`: Text chunking strategy (recursive|token|semantic)
- `--vector-store`: Vector store backend (chroma|qdrant_local|qdrant_cloud)
- `--qdrant-url`: Qdrant Cloud URL (required for qdrant_cloud)
- `--qdrant-api-key`: Qdrant Cloud API key (optional)
- `--qdrant-prefix`: Collection prefix for Qdrant (optional)
- `--qdrant-timeout`: Connection timeout in seconds (optional)

> **Note**: For security reasons, never commit API keys or sensitive URLs to version control. Use environment variables or secure secret management systems.

### List Knowledge Bases
```bash
ideaweaver rag list-kb
```

### Delete Knowledge Base
```bash
ideaweaver rag delete-kb --name my-kb
```

## Document Management

### Ingest Documents
```bash
ideaweaver rag ingest --kb my-kb --source ./docs --file-types md,pdf
```

Options:

- `--kb`: Knowledge base name (required)
- `--source`: Source path (file or directory) (required)
- `--file-types`: Comma-separated list of file types to include
- `--verbose`: Verbose output

### Show Knowledge Base Statistics
```bash
ideaweaver rag stats --kb my-kb
```

## Querying

### Basic Query
```bash
ideaweaver rag query --kb my-kb -q "What are the main features?"
```

### Agentic Query
```bash
# Set OpenAI API key as environment variable
export OPENAI_API_KEY="$OPENAI_API_KEY"

# Run agentic query
ideaweaver rag agentic-query --kb my-kb -q "Explain the advanced features"
```

### Compare RAG Types
```bash
ideaweaver rag compare-rag-types --kb my-kb -q "What are the key features?"
```

## Evaluation

### Evaluate RAG System
```bash
ideaweaver rag evaluate --kb my-kb
```

### Generate Test Questions
```bash
ideaweaver rag generate-test-questions --kb my-kb
```

### Compare Knowledge Bases
```bash
ideaweaver rag compare-kb --kb1 kb1 --kb2 kb2
```

## Visualization

### Show RAG Workflow
```bash
ideaweaver rag show-workflow
```

## Example Workflow

1. Create a new knowledge base with Qdrant Cloud:
```bash
# Set Qdrant Cloud credentials as environment variables
export QDRANT_URL="your-cloud-url"
export QDRANT_API_KEY="your-api-key"

# Create knowledge base
ideaweaver rag create-kb --name cloud-kb \
    --vector-store qdrant_cloud \
    --qdrant-url "$QDRANT_URL" \
    --qdrant-api-key "$QDRANT_API_KEY" \
    --description "Cloud knowledge base"
```

> **Note**: For security reasons, never commit API keys or sensitive URLs to version control. Use environment variables or secure secret management systems.

2. Ingest documents:
```bash
ideaweaver rag ingest --kb cloud-kb --source ./docs --file-types md
```

3. Query the knowledge base:
```bash
ideaweaver rag query --kb cloud-kb -q "What are the main features?"
```

4. Evaluate the system:
```bash
ideaweaver rag evaluate --kb cloud-kb
```

5. Generate test questions:
```bash
ideaweaver rag generate-test-questions --kb cloud-kb
```

6. Compare with another knowledge base:
```bash
ideaweaver rag compare-kb --kb1 cloud-kb --kb2 another-kb
```

## Advanced Usage

### Using Different Vector Stores

Chroma:
```bash
ideaweaver rag create-kb --name chroma-kb --vector-store chroma
```

Qdrant Cloud:
```bash
# Set Qdrant Cloud credentials as environment variables
export QDRANT_URL="your-cloud-url"
export QDRANT_API_KEY="your-api-key"

ideaweaver rag create-kb --name qdrant-cloud-kb \
    --vector-store qdrant_cloud \
    --qdrant-url "$QDRANT_URL" \
    --qdrant-api-key "$QDRANT_API_KEY" \
    --qdrant-timeout 30
```

> **Note**: For security reasons, never commit API keys or sensitive URLs to version control. Use environment variables or secure secret management systems. Example:
> ```bash
> export QDRANT_URL="your-cloud-url"
> export QDRANT_API_KEY="your-api-key"
> export OPENAI_API_KEY="your-openai-key"
> export HUGGINGFACE_HUB_TOKEN="your-hf-token"
> export GITHUB_TOKEN="your-github-token"
> ```

### Custom Chunking Strategy

```bash
ideaweaver rag create-kb --name custom-kb \
    --chunking-strategy semantic \
    --chunk-size 500 \
    --chunk-overlap 50
```

### Using Different Embedding Models

```bash
ideaweaver rag create-kb --name custom-emb-kb \
    --embedding-model sentence-transformers/all-mpnet-base-v2
``` 