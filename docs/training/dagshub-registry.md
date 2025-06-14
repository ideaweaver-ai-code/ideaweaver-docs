# DagsHub Model Registry Integration

## Overview

IdeaWeaver integrates with DagsHub for experiment tracking and model management. This guide shows you how to use DagsHub with IdeaWeaver for model versioning and deployment.

## Setup

### Train and Register a Model

```bash
source ideaweaver-env/bin/activate
ideaweaver train \
  --model sshleifer/tiny-distilbert-base-cased \
  --dataset ./datasets/training_data.csv \
  --mlflow-uri https://dagshub.com/<your-username>/<your-repo>.mlflow \
  --dagshub-token <your-dagshub-token> \
  --dagshub-repo-owner <your-username> \
  --dagshub-repo-name <your-repo>
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

### DagsHub UI Example

Once your model is registered, you can view it in the DagsHub Model Registry UI:

![DagsHub Model Registry Screenshot](images/dagshub_repo.png)

## Features

- Experiment tracking
- Model versioning
- Artifact storage
- Performance metrics
- Model deployment
- Collaboration tools

## Configuration

### Required Parameters

- `--mlflow-uri`: DagsHub MLflow URI
- `--dagshub-token`: Your DagsHub access token
- `--dagshub-repo-owner`: Your DagsHub username
- `--dagshub-repo-name`: Repository name

### Getting Your DagsHub Token

1. Go to [DagsHub Tokens Settings](https://dagshub.com/user/settings/tokens)
2. Create a new token
3. Copy the token value
4. Use it in your training command

## Best Practices

1. **Repository Organization**
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
   - Verify token is correct
   - Check token permissions
   - Ensure proper access

2. **Connection Issues**
   - Check internet connection
   - Verify repository exists
   - Validate URI format

### Debug Mode

Enable verbose output for debugging:

```bash
ideaweaver train \
  --model sshleifer/tiny-distilbert-base-cased \
  --dataset ./datasets/training_data.csv \
  --mlflow-uri https://dagshub.com/<your-username>/<your-repo>.mlflow \
  --verbose
```

## Resources

- [DagsHub Documentation](https://dagshub.com/docs)
- [MLflow Integration Guide](https://dagshub.com/docs/integration-guide/mlflow/)
- [Model Registry Guide](https://dagshub.com/docs/feature_guide/model-registry/) 