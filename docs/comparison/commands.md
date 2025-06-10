# Model Comparison Commands

The `compare` command in IdeaWeaver provides a comprehensive interface for comparing multiple language models using the lm-evaluation-harness framework.

## Basic Usage

```bash
ideaweaver compare [OPTIONS] MODEL_PATHS...
```

### Arguments

- `MODEL_PATHS`: One or more paths to the models to compare (required)

### Options

- `-t, --tasks TEXT`: Comma-separated list of tasks to evaluate on (required)
- `-wp, --wandb-project TEXT`: Weights & Biases project name
- `-we, --wandb-entity TEXT`: Weights & Biases entity name
- `-d, --device TEXT`: Device to run evaluation on (auto, cuda, cpu)
- `-b, --batch-size INTEGER`: Batch size for evaluation
- `-f, --num-fewshot INTEGER`: Number of few-shot examples
- `-l, --limit INTEGER`: Limit number of samples for testing
- `--generate-report`: Generate markdown comparison report
- `-v, --verbose`: Verbose output

## Examples

### Basic Comparison

```bash
ideaweaver compare \
  models/gpt2 \
  models/bert-base-uncased \
  --tasks gsm8k,truthfulqa \
  --batch-size 8
```

Example output:
```
🔍 Comparing models:
   - models/gpt2
   - models/bert-base-uncased

📊 Running tasks:
   - gsm8k
   - truthfulqa

🚀 Starting evaluation...
✅ Evaluation complete

📋 Results:
Model: gpt2
- gsm8k: 0.45
- truthfulqa: 0.62

Model: bert-base-uncased
- gsm8k: 0.38
- truthfulqa: 0.58
```

### With Weights & Biases Integration

```bash
ideaweaver compare \
  models/gpt2 \
  models/bert-base-uncased \
  --tasks gsm8k,truthfulqa \
  --wandb-project model-comparison \
  --wandb-entity your-username \
  --generate-report
```

Example output:
```
🔍 Comparing models:
   - models/gpt2
   - models/bert-base-uncased

📊 Running tasks:
   - gsm8k
   - truthfulqa

🔗 Weights & Biases integration enabled
   Project: model-comparison
   Entity: your-username

🚀 Starting evaluation...
✅ Evaluation complete

📋 Results:
Model: gpt2
- gsm8k: 0.45
- truthfulqa: 0.62

Model: bert-base-uncased
- gsm8k: 0.38
- truthfulqa: 0.58

📝 Generating comparison report...
✅ Report saved to: comparison_report.md
```

### Advanced Usage

```bash
ideaweaver compare \
  models/gpt2 \
  models/bert-base-uncased \
  --tasks gsm8k,truthfulqa \
  --device cuda \
  --batch-size 16 \
  --num-fewshot 3 \
  --limit 100 \
  --verbose
```

Example output:
```
🔍 Comparing models:
   - models/gpt2
   - models/bert-base-uncased

📊 Configuration:
   Tasks: gsm8k, truthfulqa
   Device: cuda
   Batch size: 16
   Few-shot examples: 3
   Sample limit: 100

🚀 Starting evaluation...
📊 Progress:
   - Loading models...
   - Preparing datasets...
   - Running evaluations...
   - Computing metrics...

✅ Evaluation complete

📋 Detailed Results:
Model: gpt2
- gsm8k:
  * Accuracy: 0.45
  * Average time: 1.2s
  * Memory usage: 2.1GB
- truthfulqa:
  * Accuracy: 0.62
  * Average time: 0.8s
  * Memory usage: 1.8GB

Model: bert-base-uncased
- gsm8k:
  * Accuracy: 0.38
  * Average time: 0.9s
  * Memory usage: 1.5GB
- truthfulqa:
  * Accuracy: 0.58
  * Average time: 0.7s
  * Memory usage: 1.3GB
```

## Best Practices

1. **Task Selection**: Choose relevant tasks for your use case
2. **Resource Management**: Adjust batch size based on available memory
3. **Weights & Biases**: Use for tracking and sharing results
4. **Report Generation**: Always generate reports for documentation
5. **Verbose Mode**: Use when debugging or analyzing performance 