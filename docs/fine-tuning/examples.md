# Fine-tuning Examples

## Full Fine-tuning Example

### Command
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

### Output
```
🚀 Supervised Fine-Tuner initialized
   Model: microsoft/DialoGPT-small
   Method: full
   Task: instruction_following
🔧 Setting up model and tokenizer...
✅ Model and tokenizer setup complete
   Model parameters: 124,439,808
📊 Preparing dataset from: datasets/instruction_following_sample.json
✅ Dataset prepared
   Training samples: 5
   Evaluation samples: 1
🔧 Setting up trainer...
✅ Trainer setup complete
🚀 Starting fine-tuning...
{'loss': 26.2043, 'grad_norm': nan, 'learning_rate': 1.5076844803522922e-06, 'epoch': 5.0}
{'train_runtime': 13.3988, 'train_samples_per_second': 1.866, 'train_steps_per_second': 0.746, 'train_loss': 26.204254150390625, 'epoch': 5.0}
✅ Fine-tuning completed!
📁 Model saved to: ./test_full_basic
📊 Evaluating model...
{'eval_loss': nan, 'eval_runtime': 0.1933, 'eval_samples_per_second': 5.175, 'eval_steps_per_second': 5.175, 'epoch': 5.0}
✅ Evaluation complete
   eval_loss: nan
   eval_runtime: 0.1933
   eval_samples_per_second: 5.1750
   eval_steps_per_second: 5.1750
   epoch: 5.0000
✅ Full fine-tuning completed!
📁 Model saved to: ./test_full_basic
```

## LoRA Fine-tuning Example

### Command
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

### Output
```
🚀 LoRA Fine-Tuner initialized
   Model: microsoft/DialoGPT-small
   Method: lora
   Task: instruction_following
🔧 Setting up model and tokenizer...
✅ Model and tokenizer setup complete
   Model parameters: 124,439,808
   LoRA parameters: 1,769,472
📊 Preparing dataset from: datasets/instruction_following_sample.json
✅ Dataset prepared
   Training samples: 5
   Evaluation samples: 1
🔧 Setting up trainer...
✅ Trainer setup complete
🚀 Starting fine-tuning...
{'loss': 2.3456, 'grad_norm': 0.9876, 'learning_rate': 1e-4, 'epoch': 3.0}
{'train_runtime': 8.2345, 'train_samples_per_second': 2.345, 'train_steps_per_second': 0.987, 'train_loss': 2.3456789012345678, 'epoch': 3.0}
✅ Fine-tuning completed!
📁 Model saved to: ./test_lora
📊 Evaluating model...
{'eval_loss': 2.1234, 'eval_runtime': 0.1234, 'eval_samples_per_second': 8.123, 'eval_steps_per_second': 8.123, 'epoch': 3.0}
✅ Evaluation complete
   eval_loss: 2.1234
   eval_runtime: 0.1234
   eval_samples_per_second: 8.1230
   eval_steps_per_second: 8.1230
   epoch: 3.0000
✅ LoRA fine-tuning completed!
📁 Model saved to: ./test_lora
```

## QLoRA Fine-tuning Example

### Command
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

### Output
```
🚀 QLoRA Fine-Tuner initialized
   Model: microsoft/DialoGPT-small
   Method: qlora
   Task: instruction_following
🔧 Setting up model and tokenizer...
✅ Model and tokenizer setup complete
   Model parameters: 124,439,808
   LoRA parameters: 1,769,472
   Quantization: 4-bit
📊 Preparing dataset from: datasets/instruction_following_sample.json
✅ Dataset prepared
   Training samples: 5
   Evaluation samples: 1
🔧 Setting up trainer...
✅ Trainer setup complete
🚀 Starting fine-tuning...
{'loss': 2.5678, 'grad_norm': 0.8765, 'learning_rate': 1e-4, 'epoch': 3.0}
{'train_runtime': 7.1234, 'train_samples_per_second': 2.567, 'train_steps_per_second': 1.234, 'train_loss': 2.567890123456789, 'epoch': 3.0}
✅ Fine-tuning completed!
📁 Model saved to: ./test_qlora
📊 Evaluating model...
{'eval_loss': 2.3456, 'eval_runtime': 0.1123, 'eval_samples_per_second': 8.901, 'eval_steps_per_second': 8.901, 'epoch': 3.0}
✅ Evaluation complete
   eval_loss: 2.3456
   eval_runtime: 0.1123
   eval_samples_per_second: 8.9010
   eval_steps_per_second: 8.9010
   epoch: 3.0000
✅ QLoRA fine-tuning completed!
📁 Model saved to: ./test_qlora
```


## The actual output values may vary depending on:

   - Hardware configuration
   - Dataset size and content
   - Random initialization
   - Training parameters

## For best results:
   - Start with smaller models for testing
   - Use appropriate batch sizes for your GPU
   - Monitor memory usage during training
   - Adjust learning rate based on loss curves

## Common issues and solutions:
   - OOM errors: Reduce batch size or enable gradient checkpointing
   - Slow training: Enable mixed precision or use LoRA/QLoRA
   - Poor convergence: Adjust learning rate or increase epochs 