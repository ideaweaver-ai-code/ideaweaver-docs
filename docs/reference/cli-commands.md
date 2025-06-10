# CLI Commands Reference

Complete reference for all IdeaWeaver CLI commands and their options.

## Overview

```bash
Usage: ideaweaver [OPTIONS] COMMAND [ARGS]...

  IdeaWeaver Model Training CLI - A comprehensive tool for AI model training,
  evaluation, and deployment.

  Features include LoRA/QLoRA fine-tuning, RAG systems, MCP integration, and
  enterprise-grade model management. For detailed documentation and examples,
  visit: https://github.com/ideaweaver-ai-code/ideaweaver

Options:
  --help  Show this message and exit.

Commands:
  agent       Intelligent agent workflows for creative and analytical tasks.
  download    Download a model from Hugging Face Hub
  evaluate    Evaluate a model using lm-evaluation-harness with...
  finetune    Supervised fine-tuning commands with LoRA, QLoRA, and full...
  list-tasks  List all available evaluation tasks from lm-evaluation-harness
  mcp         Model Context Protocol (MCP) integration commands
  rag         RAG (Retrieval-Augmented Generation) commands
  train       Train a model with AutoTrain Advanced.
  validate    Validate a configuration file
```

## Model Management

### `download`

Download models from Hugging Face Hub.

```bash
ideaweaver download [OPTIONS] MODEL_ID
```

**Options:**

- `--revision TEXT`: Model revision to download (default: main)
- `--cache-dir PATH`: Custom cache directory for models
- `--token TEXT`: Hugging Face API token
- `--help`: Show help and exit

**Examples:**
```bash
# Download a model
ideaweaver download microsoft/DialoGPT-medium

# Download specific revision
ideaweaver download microsoft/DialoGPT-medium --revision v1.0

# Download with custom cache
ideaweaver download microsoft/DialoGPT-medium --cache-dir ./models
```

### `quantize`

Optimize models through quantization for faster inference.

```bash
ideaweaver quantize [OPTIONS]
```

**Options:**
- `--model PATH`: Path to model directory or Hugging Face model ID
- `--method TEXT`: Quantization method (int8, int4, fp16)
- `--output PATH`: Output directory for quantized model
- `--config PATH`: Quantization configuration file
- `--help`: Show help and exit

**Examples:**
```bash
# Basic int8 quantization
ideaweaver quantize --model microsoft/DialoGPT-medium --method int8

# Custom output directory
ideaweaver quantize --model ./my-model --method int4 --output ./quantized
```

## Training & Fine-tuning

### `train`

Train models with flexible configuration options.

```bash
ideaweaver train [OPTIONS]
```

**Options:**
- `--config PATH`: Training configuration YAML file
- `--model TEXT`: Base model name or path
- `--dataset TEXT`: Dataset name or path
- `--output-dir PATH`: Output directory for trained model
- `--epochs INTEGER`: Number of training epochs
- `--batch-size INTEGER`: Training batch size
- `--learning-rate FLOAT`: Learning rate
- `--help`: Show help and exit

**Examples:**
```bash
# Train with configuration file
ideaweaver train --config config/training.yaml

# Quick training with CLI options
ideaweaver train --model bert-base-uncased --dataset ./data.csv --epochs 3
```

### `finetune`

Supervised fine-tuning with LoRA, QLoRA, and full parameter methods.

#### `finetune lora`

LoRA (Low-Rank Adaptation) fine-tuning.

```bash
ideaweaver finetune lora [OPTIONS]
```

**Options:**
- `--model TEXT`: Base model for fine-tuning
- `--dataset TEXT`: Training dataset
- `--output-dir PATH`: Output directory
- `--rank INTEGER`: LoRA rank (default: 16)
- `--alpha INTEGER`: LoRA alpha parameter (default: 32)
- `--dropout FLOAT`: LoRA dropout rate (default: 0.1)
- `--epochs INTEGER`: Number of epochs (default: 3)
- `--help`: Show help and exit

**Examples:**
```bash
# Basic LoRA fine-tuning
ideaweaver finetune lora --model microsoft/DialoGPT-medium --dataset ./data

# Custom LoRA parameters
ideaweaver finetune lora --model bert-base --dataset ./data --rank 32 --alpha 64
```

#### `finetune qlora`

QLoRA (Quantized LoRA) for memory-efficient fine-tuning.

```bash
ideaweaver finetune qlora [OPTIONS]
```

**Options:**
- Similar to LoRA with additional quantization options
- `--bits INTEGER`: Quantization bits (4, 8)
- `--double-quant BOOLEAN`: Use double quantization

#### `finetune full`

Full parameter fine-tuning.

```bash
ideaweaver finetune full [OPTIONS]
```

**Options:**
- Standard training options without rank/alpha parameters

## Evaluation & Benchmarking

### `evaluate`

Evaluate models using lm-evaluation-harness and custom benchmarks.

```bash
ideaweaver evaluate [OPTIONS]
```

**Options:**
- `--model PATH`: Model to evaluate
- `--tasks TEXT`: Comma-separated list of evaluation tasks
- `--batch-size INTEGER`: Evaluation batch size
- `--num-fewshot INTEGER`: Number of few-shot examples
- `--output PATH`: Output file for results
- `--device TEXT`: Device to use (cuda, cpu, auto)
- `--help`: Show help and exit

**Examples:**
```bash
# Evaluate on multiple tasks
ideaweaver evaluate --model ./my-model --tasks hellaswag,arc_easy,winogrande

# Custom few-shot evaluation
ideaweaver evaluate --model ./my-model --tasks hellaswag --num-fewshot 5
```

### `list-tasks`

List all available evaluation tasks.

```bash
ideaweaver list-tasks [OPTIONS]
```

**Options:**
- `--category TEXT`: Filter tasks by category
- `--search TEXT`: Search tasks by name or description
- `--help`: Show help and exit

### `compare`

Compare multiple models on the same benchmarks.

```bash
ideaweaver compare [OPTIONS]
```

**Options:**
- `--models TEXT`: Comma-separated list of models to compare
- `--tasks TEXT`: Evaluation tasks for comparison
- `--output PATH`: Output file for comparison results
- `--plot`: Generate comparison plots
- `--help`: Show help and exit

**Examples:**
```bash
# Compare three models
ideaweaver compare --models model1,model2,model3 --tasks hellaswag,arc_easy

# Generate comparison with plots
ideaweaver compare --models model1,model2 --tasks all --plot --output comparison.html
```

## RAG (Retrieval-Augmented Generation)

### `rag init`

Initialize a new RAG system.

```bash
ideaweaver rag init [OPTIONS]
```

**Options:**
- `--vector-store TEXT`: Vector store type (chroma, qdrant, faiss)
- `--embedding-model TEXT`: Embedding model name
- `--llm TEXT`: Language model for generation
- `--config PATH`: RAG configuration file
- `--help`: Show help and exit

### `rag add-documents`

Add documents to the RAG knowledge base.

```bash
ideaweaver rag add-documents [OPTIONS]
```

**Options:**
- `--path PATH`: Path to documents or directory
- `--recursive`: Process directories recursively
- `--chunk-size INTEGER`: Document chunk size
- `--chunk-overlap INTEGER`: Overlap between chunks
- `--help`: Show help and exit

### `rag query`

Query the RAG system.

```bash
ideaweaver rag query [OPTIONS] QUERY
```

**Options:**
- `--config PATH`: RAG configuration file
- `--top-k INTEGER`: Number of retrieved documents
- `--temperature FLOAT`: Generation temperature
- `--save-context`: Save query context for training
- `--help`: Show help and exit

**Examples:**
```bash
# Basic RAG query
ideaweaver rag query "What is machine learning?"

# Custom retrieval parameters
ideaweaver rag query "Explain neural networks" --top-k 10 --temperature 0.7
```

## MCP (Model Context Protocol)

### `mcp list-servers`

List all available MCP servers.

```bash
ideaweaver mcp list-servers [OPTIONS]
```

### `mcp configure`

Configure MCP server connections.

```bash
ideaweaver mcp configure [OPTIONS] SERVER_NAME
```

**Supported Servers:**
- `github`: GitHub integration
- `slack`: Slack workspace integration  
- `aws`: AWS services integration
- `filesystem`: Local filesystem access

### `mcp query`

Query data through MCP servers.

```bash
ideaweaver mcp query [OPTIONS] SERVER_NAME QUERY
```

**Examples:**
```bash
# Query GitHub repositories
ideaweaver mcp query github "List recent issues in my repository"

# Query Slack conversations
ideaweaver mcp query slack "Summarize today's discussions"
```

## Llama.cpp Integration

### `llama convert`

Convert models to GGML format for llama.cpp.

```bash
ideaweaver llama convert [OPTIONS]
```

**Options:**
- `--model PATH`: Model to convert
- `--output PATH`: Output GGML file
- `--type TEXT`: Conversion type (f16, f32, q4_0, q4_1, q5_0, q5_1, q8_0)
- `--help`: Show help and exit

### `llama inference`

Run inference using llama.cpp.

```bash
ideaweaver llama inference [OPTIONS]
```

**Options:**
- `--model PATH`: GGML model file
- `--prompt TEXT`: Input prompt
- `--max-tokens INTEGER`: Maximum generated tokens
- `--temperature FLOAT`: Sampling temperature
- `--help`: Show help and exit

## Workflow Integration

### `crew`

CrewAI operations for multi-agent workflows.

```bash
ideaweaver crew [OPTIONS] COMMAND [ARGS]...
```

**Commands:**
- `generate-storybook`: Generate storybooks using multi-agent approach
- `setup-crew`: Configure CrewAI agents
- `run-workflow`: Execute custom CrewAI workflows

### `zenml`

ZenML pipeline operations.

```bash
ideaweaver zenml [OPTIONS] COMMAND [ARGS]...
```

**Commands:**
- `init-pipeline`: Initialize ZenML pipelines
- `run-pipeline`: Execute ZenML pipelines
- `list-pipelines`: Show available pipelines

## Utilities

### `validate`

Validate configuration files.

```bash
ideaweaver validate [OPTIONS] CONFIG_FILE
```

**Options:**
- `--type TEXT`: Configuration type (training, rag, evaluation)
- `--strict`: Enable strict validation
- `--help`: Show help and exit

**Examples:**
```bash
# Validate training configuration
ideaweaver validate config/training.yaml --type training

# Validate RAG setup
ideaweaver validate config/rag.yaml --type rag
```

## Global Options

These options are available for most commands:

- `--verbose, -v`: Enable verbose output
- `--quiet, -q`: Suppress non-error output
- `--config PATH`: Global configuration file
- `--log-level TEXT`: Set logging level (DEBUG, INFO, WARNING, ERROR)
- `--no-cache`: Disable caching
- `--device TEXT`: Force specific device (cuda, cpu, mps)

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
  
chunking:
  chunk_size: 1000
  chunk_overlap: 200
```

### Evaluation Configuration

```yaml
# config/evaluation.yaml
model: "path/to/model"
tasks:
  - "hellaswag"
  - "arc_easy"
  - "winogrande"
batch_size: 8
num_fewshot: 5
device: "auto"
output_file: "results.json"
```

## Environment Variables

Set these environment variables for full functionality:

```bash
# API Keys
export OPENAI_API_KEY="your-openai-key"
export HUGGINGFACE_HUB_TOKEN="your-hf-token"
export ANTHROPIC_API_KEY="your-anthropic-key"

# Experiment Tracking
export WANDB_API_KEY="your-wandb-key"
export MLFLOW_TRACKING_URI="your-mlflow-uri"

# Cloud Services
export AWS_ACCESS_KEY_ID="your-aws-key"
export AWS_SECRET_ACCESS_KEY="your-aws-secret"

# MCP Integrations
export GITHUB_TOKEN="your-github-token"
export SLACK_BOT_TOKEN="your-slack-token"
```

## Exit Codes

- `0`: Success
- `1`: General error
- `2`: Configuration error
- `3`: Model not found
- `4`: Dataset error
- `5`: Training/evaluation error
- `6`: Network/API error 