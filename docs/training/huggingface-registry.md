# Hugging Face Model Registry Integration

## Overview

IdeaWeaver integrates with Hugging Face for model hosting and versioning. This guide shows you how to use Hugging Face with IdeaWeaver for model management and deployment.

## Setup

### Train and Push a Model

```bash
source ideaweaver-env/bin/activate
ideaweaver train \
  --model sshleifer/tiny-distilbert-base-cased \
  --dataset ./datasets/training_data.csv \
  --push-to-hub \
  --hub-model-id <your-username>/<model-name> \
  --hub-token <your-huggingface-token>
```

#### Example Output
```
🤗 Using model: sshleifer/tiny-distilbert-base-cased
🚀 Starting model training...

============================================================
🎉 TRAINING SUMMARY
============================================================
📂 Model Path:           ./my-model
🤖 Base Model:           sshleifer/tiny-distilbert-base-cased
📊 Dataset:              ./autotrain_projects/my-model

📊 KEY PERFORMANCE METRICS
----------------------------------------
📉 Final Train Loss:     1.0986
🎯 Overall Accuracy:     20.0%

============================================================
✨ Training completed successfully! Model is ready for use.
============================================================

✅ Training completed successfully!
📁 Model saved to: ./my-model
🚀 Pushing model to Hugging Face Hub...
✅ Model pushed successfully to <your-username>/<model-name>
```

### Hugging Face Hub Example

Once your model is pushed, you can view it on the Hugging Face Hub:

![Hugging Face Hub Screenshot](images/huggingface_hub.png)

## Features

- Model hosting
- Version control
- Model cards
- Inference API
- Community sharing
- Model evaluation

## Configuration

### Required Parameters

- `--push-to-hub`: Flag to enable pushing to Hugging Face Hub
- `--hub-model-id`: Model ID in format username/model-name
- `--hub-token`: Your Hugging Face API token

### Getting Your Hugging Face Token

1. Go to [Hugging Face Settings](https://huggingface.co/settings/tokens)
2. Create a new token
3. Copy the token value
4. Use it in your training command

## Best Practices

1. **Model Organization**
   - Use meaningful model names
   - Add detailed model cards
   - Document model versions

2. **Model Management**
   - Version your models
   - Add model descriptions
   - Track model lineage

3. **Community**
   - Share models appropriately
   - Document usage
   - Provide examples

## Troubleshooting

### Common Issues

1. **Authentication Errors**
   - Verify token is correct
   - Check token permissions
   - Ensure proper access

2. **Connection Issues**
   - Check internet connection
   - Verify model ID format
   - Validate repository exists

### Debug Mode

Enable verbose output for debugging:

```bash
ideaweaver train \
  --model sshleifer/tiny-distilbert-base-cased \
  --dataset ./datasets/training_data.csv \
  --push-to-hub \
  --hub-model-id <your-username>/<model-name> \
  --verbose
```

## Resources

- [Hugging Face Hub Documentation](https://huggingface.co/docs/hub/index)
- [Model Cards Guide](https://huggingface.co/docs/hub/model-cards)
- [Inference API Guide](https://huggingface.co/docs/inference-endpoints/index) 