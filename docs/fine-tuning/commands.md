# Fine-tuning Commands

## Basic Usage

```bash
ideaweaver finetune [OPTIONS] COMMAND [ARGS]
```

## Available Methods

- `full`: Full parameter fine-tuning
- `lora`: LoRA fine-tuning
- `qlora`: QLoRA fine-tuning

## Full Fine-tuning Example

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

## Common Options

| Option | Description | Default |
|--------|-------------|---------|
| `--model` | Base model name or path | Required |
| `--dataset` | Path to dataset file | Required |
| `--output-dir` | Directory to save model | Required |
| `--epochs` | Number of training epochs | 3 |
| `--batch-size` | Training batch size | 8 |
| `--learning-rate` | Learning rate | 2e-5 |
| `--max-seq-length` | Maximum sequence length | 512 |
| `--gradient-checkpointing` | Enable gradient checkpointing | False |
| `--gradient-accumulation-steps` | Gradient accumulation steps | 1 |
| `--verbose` | Enable verbose output | False |

## LoRA Fine-tuning Example

```bash
ideaweaver finetune lora \
  --model microsoft/DialoGPT-small \
  --dataset datasets/instruction_following_sample.json \
  --output-dir ./test_lora \
  --epochs 3 \
  --batch-size 4 \
  --learning-rate 1e-4 \
  --lora-rank 8 \
  --lora-alpha 16 \
  --verbose
```

## QLoRA Fine-tuning Example

```bash
ideaweaver finetune qlora \
  --model microsoft/DialoGPT-small \
  --dataset datasets/instruction_following_sample.json \
  --output-dir ./test_qlora \
  --epochs 3 \
  --batch-size 4 \
  --learning-rate 1e-4 \
  --lora-rank 8 \
  --lora-alpha 16 \
  --bits 4 \
  --verbose
```

## Additional Options

### Experiment Tracking

```bash
# With MLflow
ideaweaver finetune full \
  --model microsoft/DialoGPT-small \
  --dataset datasets/instruction_following_sample.json \
  --output-dir ./test_full_basic \
  --track-experiments \
  --mlflow-uri http://127.0.0.1:5000 \
  --mlflow-experiment "MyExperiment"

# With Weights & Biases
ideaweaver finetune full \
  --model microsoft/DialoGPT-small \
  --dataset datasets/instruction_following_sample.json \
  --output-dir ./test_full_basic \
  --track-experiments \
  --wandb-project "MyProject" \
  --wandb-entity "MyEntity"
```

For more examples and use cases, see the [Examples](examples.md) page. 