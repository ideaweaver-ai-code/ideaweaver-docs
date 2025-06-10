
## Training Approaches

IdeaWeaver supports two flexible training approaches:

### 1. Config-Based Training

Using a YAML configuration file for complex setups:

```bash
ideaweaver train --config configs/config.yml --verbose
```

## Configuration Used (YAML-based training)

```yaml
📋 Final configuration:
   project_name: text-classifier
   task: text_classification
   backend: local
   base_model: google/bert_uncased_L-2_H-128_A-2
   dataset: ./datasets/training_data.csv
   params: 
     epochs: 3
     batch_size: 8
     learning_rate: 2e-05
     max_seq_length: 128
     eval_strategy: no
     save_total_limit: 1
   data:
     train_split: train
   hub:
     push_to_hub: false
   method: sft
   tracking:
     enabled: false
```

### 2. Command Line Training

Pass all parameters directly via command line for quick experiments:

```bash
ideaweaver train \
  --model google/bert_uncased_L-2_H-128_A-2 \
  --dataset ./datasets/training_data.csv \
  --task text_classification \
  --project-name cli-final-test \
  --epochs 1 \
  --batch-size 4 \
  --learning-rate 2e-05 \
  --verbose
```

## Command Line Training Output

Here's the successful output from the command line training approach:

```bash
🤗 Using model: google/bert_uncased_L-2_H-128_A-2
🎯 Task: text_classification
📋 Final configuration:
   backend: local
   params: {'epochs': 1, 'batch_size': 4, 'learning_rate': 2e-05, 'max_seq_length': 128}
   data: {'train_split': 'train'}
   hub: {'push_to_hub': False}
   base_model: google/bert_uncased_L-2_H-128_A-2
   task: text_classification
   dataset: ./datasets/training_data.csv
   project_name: cli-final-test
   tracking: {'enabled': False}
🚀 Starting model training...
📝 Training config written to: /tmp/training_config.yml
📋 Training configuration:
backend: local
base_model: google/bert_uncased_L-2_H-128_A-2
data:
  column_mapping:
    target: target
    text: text
  path: ./autotrain_projects/cli-final-test
  train_split: train
  valid_split: null
log: tensorboard
params:
  batch_size: 4
  epochs: 1
  lr: 2.0e-05
  max_seq_length: 128
project_name: cli-final-test
task: text_classification

🔧 Running command: autotrain --config /tmp/training_config.yml
...
[Training progress with successful completion]
...

📊 Loading metrics from trainer state: ./cli-final-test/checkpoint-1/trainer_state.json
✅ Successfully loaded metrics from trainer state

============================================================
🎉 TRAINING SUMMARY
============================================================
📂 Model Path:           ./cli-final-test
🤖 Base Model:           google/bert_uncased_L-2_H-128_A-2
📊 Dataset:              ./autotrain_projects/cli-final-test

📊 KEY PERFORMANCE METRICS
----------------------------------------
📉 Final Train Loss:     1.0869
🎯 Overall Accuracy:     40.0%

============================================================
✨ Training completed successfully! Model is ready for use.
============================================================

✅ Training completed successfully!
📁 Model saved to: ./cli-final-test
```



## Key Metrics Achieved

| Metric | Value | Notes |
|--------|-------|-------|
| **Final Training Loss** | 1.0869 | Successfully extracted from trainer_state.json |
| **Overall Accuracy** | 40.0% | Evaluation accuracy on validation set |
| **Training Epochs** | 1.0 | Early stopping or completed epoch |
| **Model Size** | 17MB | Compact BERT model (2 layers, 128 hidden units) |
| **Dataset Size** | 24 samples | 19 training + 5 validation samples |

## Technical Details

### Model Architecture
- **Base Model**: `google/bert_uncased_L-2_H-128_A-2`
- **Task**: Text Classification (Sentiment Analysis)
- **Classes**: 3 (positive, negative, neutral)
- **Parameters**: Small BERT with 2 layers and 128 hidden units

### Training Configuration
- **Learning Rate**: 2e-05
- **Batch Size**: 8
- **Max Sequence Length**: 128
- **Optimizer**: AdamW
- **Scheduler**: Linear
- **Early Stopping**: Enabled (patience: 5, threshold: 0.01)

### Data Processing
- **Training Split**: 19 samples
- **Validation Split**: 5 samples  
- **Text Column**: `autotrain_text`
- **Target Column**: `autotrain_label`

## Files Generated

### Model Files
- `./text-classifier/model.safetensors` (17MB)
- `./text-classifier/config.json`
- `./text-classifier/tokenizer.json`
- `./text-classifier/tokenizer_config.json`

### Training Artifacts
- `./text-classifier/checkpoint-3/trainer_state.json` - Contains detailed training metrics
- `./datasets/text-classifier/` - Copy of processed training data
- TensorBoard logs for visualization

## Verification Commands

```bash
# Verify model files
ls -la ./text-classifier/

# Check trainer state metrics
cat ./text-classifier/checkpoint-3/trainer_state.json | jq '.log_history[-1]'

# Test model loading
python -c "from transformers import AutoTokenizer, AutoModelForSequenceClassification; tokenizer = AutoTokenizer.from_pretrained('./text-classifier'); model = AutoModelForSequenceClassification.from_pretrained('./text-classifier'); print('✅ Model loads successfully')"
```

## Success Indicators

✅ **Metrics Display Fixed**: Real training metrics now shown instead of "Not available"  
✅ **Model Training**: Successfully trained sentiment classification model  
✅ **File Generation**: All model files created correctly  
✅ **Data Processing**: Dataset processed and split appropriately  
✅ **Trainer State**: Detailed training history preserved in JSON format  

## Next Steps

1. **Model Evaluation**: Test the trained model on new data
2. **Fine-tuning**: Experiment with hyperparameters for better accuracy
3. **Deployment**: Deploy the model for inference
4. **Integration**: Use with RAG or other IdeaWeaver features



## Example: Training Output with MiniLM (Command-Line)

Below is a sample output from running the training command with the Microsoft MiniLM model:

```bash
ideaweaver train \
  --model microsoft/MiniLM-L6-H384-uncased \
  --dataset ./datasets/training_data.csv \
  --task text_classification \
  --project-name cli-minilm-test \
  --epochs 1 \
  --batch-size 4 \
  --learning-rate 2e-05 \
  --verbose
```

> **Note:**
> If the model (`microsoft/MiniLM-L6-H384-uncased`) is not present locally, it will be automatically downloaded from Hugging Face the first time you run the command.

## Sample Output

```text
🤗 Using model: microsoft/MiniLM-L6-H384-uncased
🎯 Task: text_classification
📋 Final configuration:
   backend: local
   params: {'epochs': 1, 'batch_size': 4, 'learning_rate': 2e-05, 'max_seq_length': 128}
   data: {'train_split': 'train'}
   hub: {'push_to_hub': False}
   base_model: microsoft/MiniLM-L6-H384-uncased
   task: text_classification
   dataset: ./datasets/training_data.csv
   project_name: cli-minilm-test
   tracking: {'enabled': False}
🚀 Starting model training...
📝 Training config written to: /tmp/tmppyzh5clq.yml
📋 Training configuration:
backend: local
base_model: microsoft/MiniLM-L6-H384-uncased
data:
  column_mapping:
    target: target
    text: text
  path: ./autotrain_projects/cli-minilm-test
  train_split: train
  valid_split: null
log: tensorboard
params:
  batch_size: 4
  epochs: 1
  lr: 2.0e-05
  max_seq_length: 128
project_name: cli-minilm-test
task: text_classification

🔧 Running command: autotrain --config /tmp/tmppyzh5clq.yml
INFO     | ... - Using AutoTrain configuration: /tmp/tmppyzh5clq.yml
INFO     | ... - Running task: text_multi_class_classification
INFO     | ... - Using backend: local
INFO     | ... - Starting local training...
INFO     | ... - loading dataset from disk
INFO     | ... - Starting to train...
INFO     | ... - {'loss': 1.1103, 'grad_norm': 2.46, 'learning_rate': 2e-05, 'epoch': 0.33}
INFO     | ... - {'loss': 1.126, 'grad_norm': 3.26, 'learning_rate': 1.75e-05, 'epoch': 0.67}
INFO     | ... - {'loss': 1.0338, 'grad_norm': 5.06, 'learning_rate': 1.5e-05, 'epoch': 1.0}
INFO     | ... - {'eval_loss': 1.0817, 'eval_f1_macro': 0.19, 'eval_f1_micro': 0.4, 'eval_accuracy': 0.4, 'epoch': 1.0}
INFO     | ... - {'loss': 1.0702, ...}
INFO     | ... - {'loss': 1.1341, ...}
INFO     | ... - {'loss': 1.1244, ...}
INFO     | ... - {'eval_loss': 1.0829, 'eval_accuracy': 0.4, 'epoch': 2.0}
INFO     | ... - {'loss': 1.1247, ...}
INFO     | ... - {'loss': 1.0579, ...}
INFO     | ... - {'loss': 1.0865, ...}
INFO     | ... - {'eval_loss': 1.0832, 'eval_accuracy': 0.4, 'epoch': 3.0}
INFO     | ... - {'train_runtime': 2.29, 'train_loss': 1.0964, 'epoch': 3.0}
INFO     | ... - Finished training, saving model...
INFO     | ... - Job ID: 36417

============================================================
🎉 TRAINING SUMMARY
============================================================
📂 Model Path:           ./cli-minilm-test
🤖 Base Model:           microsoft/MiniLM-L6-H384-uncased
📊 Dataset:              ./autotrain_projects/cli-minilm-test

📊 KEY PERFORMANCE METRICS
----------------------------------------
📉 Final Train Loss:     1.0338
🎯 Overall Accuracy:     40.0%

============================================================
✨ Training completed successfully! Model is ready for use.
============================================================

✅ Training completed successfully!
📁 Model saved to: ./cli-minilm-test
``` 