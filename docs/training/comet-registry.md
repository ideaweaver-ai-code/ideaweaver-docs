# Comet Model Registry Integration

## Overview

IdeaWeaver integrates with Comet for experiment tracking and model management. This guide shows you how to use Comet with IdeaWeaver for model versioning and deployment.

## Setup

### Train and Register a Model

```bash
source ideaweaver-env/bin/activate
ideaweaver train \
  --model sshleifer/tiny-distilbert-base-cased \
  --dataset ./datasets/training_data.csv \
  --comet-api-key <your-comet-api-key> \
  --comet-project-name <your-project> \
  --comet-workspace <your-workspace>
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
```

### Comet UI Example

Once your model is registered, you can view it in the Comet UI:

![Comet UI Screenshot](images/comet_ui.png)

## Features

- Experiment tracking
- Model versioning
- Artifact storage
- Performance metrics
- Model deployment
- Collaboration tools

## Configuration

### Required Parameters

- `--comet-api-key`: Your Comet API key
- `--comet-project-name`: Project name
- `--comet-workspace`: Workspace name

### Getting Your Comet API Key

1. Go to [Comet Account Settings](https://www.comet.com/settings/api-keys)
2. Create a new API key
3. Copy the key value
4. Use it in your training command

## Best Practices

1. **Project Organization**
   - Use meaningful experiment names
   - Tag experiments appropriately
   - Document model versions

2. **Model Management**
   - Version your models
   - Add model descriptions
   - Track model lineage

3. **Collaboration**
   - Share experiments with team
   - Document findings
   - Track changes

## Troubleshooting

### Common Issues

1. **Authentication Errors**
   - Verify API key is correct
   - Check key permissions
   - Ensure proper access

2. **Connection Issues**
   - Check internet connection
   - Verify project exists
   - Validate workspace name

### Debug Mode

Enable verbose output for debugging:

```bash
ideaweaver train \
  --model sshleifer/tiny-distilbert-base-cased \
  --dataset ./datasets/training_data.csv \
  --comet-api-key <your-comet-api-key> \
  --verbose
```

## Resources

- [Comet Documentation](https://www.comet.com/docs/)
- [Comet Python SDK](https://www.comet.com/docs/python-sdk/)
- [Model Registry Guide](https://www.comet.com/docs/model-registry/) 