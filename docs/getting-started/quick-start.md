# Quick Start Guide

Get up and running with IdeaWeaver in minutes! This guide walks you through the essential features.

## Prerequisites

Make sure you have completed the [Installation Guide](installation.md) and can run:

```bash
source ideaweaver-env/bin/activate
ideaweaver --help
```

## Available Commands

IdeaWeaver provides comprehensive CLI commands for AI model operations:

```bash
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

## Download Your First Model

Start by downloading a model from Hugging Face:

```bash
# Download a small model for quick testing
ideaweaver download microsoft/DialoGPT-medium

# Use the `--save-path` option to specify the directory where the downloaded model will be stored.
ideaweaver download microsoft/DialoGPT-medium --save-path ./models/my-model
```

## Basic Model Training

### 1. Prepare Your Dataset

Create a simple training configuration:

```yaml
# config/training_config.yaml
model:
  name: "microsoft/DialoGPT-medium"
  task: "text-generation"

dataset:
  name: "your-dataset-name"
  split: "train"

training:
  output_dir: "./results"
  num_train_epochs: 3
  per_device_train_batch_size: 4
  learning_rate: 5e-5
  save_steps: 500
  logging_steps: 100
```

### 2. Start Training

```bash
# Basic training
ideaweaver train --config config/training_config.yaml
```

## RAG (Retrieval-Augmented Generation)

### 1. Set Up Your First RAG System

```bash
# 1. Create a knowledge base
ideaweaver rag create-kb --name mykb --embedding-model sentence-transformers/all-MiniLM-L6-v2

# 2. Ingest documents into the knowledge base
ideaweaver rag ingest --kb mykb --source ./documents/

# 3. Query the knowledge base
ideaweaver rag query --kb mykb --question "What is machine learning?"
```

## 🔌 MCP (Model Context Protocol) Integration

### 1. List Available MCP Servers

```bash
# See all available MCP integrations
ideaweaver mcp list-servers
```

### 2. Set Up GitHub Integration

```bash
# 1. Set up GitHub authentication (will prompt for your token)
ideaweaver mcp setup-auth github

# 2. Enable the GitHub MCP server
ideaweaver mcp enable github

# 3. List available MCP servers (to verify)
ideaweaver mcp list-servers

# 4. Call a tool on the GitHub MCP server (example: list issues)
ideaweaver mcp call-tool github list_issues --args '{"owner": "your-username/org name", "repo": "your-repo"}'
```

## Model Evaluation

### 1. Evaluate with Standard Benchmarks

```bash
# Run evaluation on specific tasks
ideaweaver evaluate ./downloaded_model --tasks hellaswag,arc_easy,winogrande --output-path results.json
```

## Agents

### Agents for Multi-Agent Workflows

```bash
# Generate storybooks
ideaweaver agent generate_storybook --theme "brave little mouse" --target-age "3-5"
```

## Model Fine-tuning
```bash
ideaweaver finetune full \
  --model microsoft/DialoGPT-small \
  --dataset datasets/instruction_following_sample.json \
  --output-dir ./test_full_basic \
  --epochs 5 \
  --batch-size 2 \
  --gradient-accumulation-steps 2 \
  --learning-rate 5e-5 \
  --max-seq-length 256 \
  --gradient-checkpointing \
  --verbose
```

## Configuration Validation

Always validate your configurations before running:

```bash
# Validate training configuration
ideaweaver validate config/training_config.yaml
```

## Pro Tips

1. **Environment Variables**: Set API keys in your shell profile for persistence
2. **Configuration Files**: Use YAML configs for complex setups - easier to reproduce
3. **Logging**: Add `--verbose` flag to most commands for detailed output
4. **GPU Usage**: Commands automatically detect and use available GPUs
5. **Caching**: Models and datasets are cached locally to speed up repeated runs

## 🚨 Common Issues

**Command not found**: Make sure your virtual environment is activated
```bash
source ideaweaver-env/bin/activate
```

**Import errors**: Reinstall requirements if packages are missing
```bash
pip install -r requirements.txt --force-reinstall
```

**GPU not detected**: Check CUDA installation
```bash
python -c "import torch; print(torch.cuda.is_available())"
```

## Next Steps

Now that you've got the basics down:

1. 📖 Explore detailed [Tutorials](../tutorials/)
2. 🔧 Check the [CLI Reference](../reference/cli-commands.md)
3. 🤝 Join our [Community](../community/contributing.md)
4. 🚀 Deploy to [Production](../guides/cloud-deployment.md)

Ready to build something amazing? Let's go! 🚀 