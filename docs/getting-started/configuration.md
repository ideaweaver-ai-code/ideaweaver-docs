# Configuration

## Environment Setup

Set up your API keys and configuration for IdeaWeaver:

```bash
# OpenAI API (for GPT models)
export OPENAI_API_KEY='your-openai-api-key'

# Hugging Face Hub (for model downloads)
export HUGGINGFACE_HUB_TOKEN='your-huggingface-token'

# Weights & Biases (for experiment tracking)
export WANDB_API_KEY='your-wandb-api-key'

# Comet ML (for experiment tracking)
export COMET_API_KEY='your-comet-api-key'

# MLflow (for experiment tracking)
export MLFLOW_TRACKING_URI='your-mlflow-uri'

# DagsHub (for experiment tracking)
export DAGSHUB_TOKEN='your-dagshub-token'

# AWS Credentials (for cloud deployment)
export AWS_ACCESS_KEY_ID='your-aws-access-key'
export AWS_SECRET_ACCESS_KEY='your-aws-secret-key'
export AWS_DEFAULT_REGION='us-east-1'

# Qdrant (for vector store)
export QDRANT_URL='your-qdrant-url'
export QDRANT_API_KEY='your-qdrant-key'

# GitHub (for MCP integration)
export GITHUB_TOKEN='your-github-token'
```

## Configuration Files

### Training Configuration

```yaml
# config/training.yaml
model:
  name: "microsoft/DialoGPT-medium"
  task: "text-generation"
  
dataset:
  name: "your-dataset"
  split: "train"
  
training:
  output_dir: "./results"
  num_train_epochs: 3
  per_device_train_batch_size: 4
  learning_rate: 5e-5
  save_steps: 500
  logging_steps: 100
  
lora:
  rank: 16
  alpha: 32
  dropout: 0.1
```

### RAG Configuration

```yaml
# config/rag.yaml
vector_store:
  type: "chroma"
  persist_directory: "./chroma_db"
  
embeddings:
  model: "sentence-transformers/all-MiniLM-L6-v2"
  
llm:
  provider: "openai"
  model: "gpt-3.5-turbo"
  temperature: 0.7
  
retrieval:
  top_k: 5
  similarity_threshold: 0.7
```

## Next Steps

- [Quick Start Guide](quick-start.md)
- [CLI Commands Reference](../reference/cli-commands.md) 