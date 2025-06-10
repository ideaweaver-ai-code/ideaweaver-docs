![Fine-tuning Methods Diagram](fine-tuning.png)

# Fine-tuning Overview

IdeaWeaver provides comprehensive support for model fine-tuning with multiple approaches:

## Available Methods

**Full Fine-tuning**

   - Complete model parameter updates
   - Maximum customization potential
   - Higher resource requirements

**LoRA (Low-Rank Adaptation)**

   - Parameter-efficient fine-tuning
   - Reduced memory footprint
   - Faster training times

**QLoRA (Quantized LoRA)**

   - Memory-efficient fine-tuning
   - 4-bit quantization support
   - Ideal for large models

## Key Features

- **Gradient Checkpointing**: Memory optimization for large models
- **Gradient Accumulation**: Effective batch size control
- **Mixed Precision Training**: FP16/BF16 support
- **Multi-GPU Support**: Distributed training capabilities
- **Experiment Tracking**: Integration with MLflow & W&B

## Prerequisites

- Python 3.12+
- CUDA-compatible GPU (for full fine-tuning)
- Sufficient disk space for model checkpoints
- Dataset in supported format (JSON, CSV, etc.)

## Getting Started

See the [Commands](commands.md) page for detailed usage instructions and [Examples](examples.md) for practical use cases. 