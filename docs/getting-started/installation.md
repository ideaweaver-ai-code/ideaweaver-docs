# Installation Guide

## Quick Setup

IdeaWeaver provides an automated setup script that handles Python 3.12 installation and virtual environment creation:

```bash
# Installation
git clone https://github.com/ideaweaver-ai-code/ideaweaver.git
cd ideaweaver
chmod +x setup_environments.sh
./setup_environments.sh
```

The setup will:

- ✅ Detect or install Python 3.12 automatically
- ✅ Create `ideaweaver-env` virtual environment  
- ✅ Install all dependencies from consolidated `requirements.txt`
- ✅ Set up the IdeaWeaver CLI in development mode

### Activate Environment

```bash
source ideaweaver-env/bin/activate
```

### Verify Installation

```bash
ideaweaver --help
```

**Expected Output:**
```
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

## Manual Installation

If you prefer manual installation or the automated script doesn't work for your system:

### Prerequisites

- **Python 3.12** (Required - not 3.11 or 3.13)
- **Git** for cloning the repository
- **pip** for package management

### Step-by-Step Installation

1. **Clone the Repository**
```bash
git clone https://github.com/ideaweaver-ai-code/ideaweaver.git
cd ideaweaver
```

2. **Create Virtual Environment**
```bash
python3.12 -m venv ideaweaver-env
source ideaweaver-env/bin/activate  
```

3. **Install Dependencies**
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

4. **Install IdeaWeaver CLI**
```bash
cd backend
pip install -e .
cd ..
```

## Environment Variables

Set up your API keys for full functionality:

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

## Troubleshooting

### Python Version Issues

The setup script requires **Python 3.12 exactly**. If you encounter version-related errors:

```bash
# Check your Python version
python3.12 --version  # Should show 3.12.x

# On macOS with Homebrew
brew install python@3.12

# On Ubuntu/Debian
sudo apt-get install python3.12 python3.12-venv python3.12-pip

# On CentOS/RHEL
sudo dnf install python3.12
```

### Common Installation Issues

**Issue: `auto-gptq` installation fails**
- This is normal on macOS (requires CUDA)
- The core functionality works without it

**Issue: `ideaweaver` command not found**
- Make sure you activated the virtual environment
- Verify the backend installation completed successfully

**Issue: Import errors for specific packages**
- Check if all requirements installed: `pip list`
- Reinstall requirements: `pip install -r requirements.txt --force-reinstall`

## Next Steps

After successful installation:

1. Follow the [Quick Start Guide](quick-start.md)
2. Configure your first RAG system
3. Train your first model
4. Set up MCP integrations

## System Requirements

### Minimum Requirements
- **CPU**: 4+ cores recommended
- **RAM**: 8GB minimum, 16GB+ recommended
- **Storage**: 10GB free space minimum
- **OS**: macOS 10.15+, Ubuntu 18.04+

### Recommended for Training
- **GPU**: NVIDIA GPU with 8GB+ VRAM
- **RAM**: 32GB+ for large model training  
- **Storage**: 50GB+ for model storage 