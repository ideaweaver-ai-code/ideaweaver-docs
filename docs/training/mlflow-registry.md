# MLflow Model Registry Integration

## Overview

IdeaWeaver provides seamless integration with MLflow for experiment tracking and model registration. This guide shows you how to use MLflow with IdeaWeaver for model management.

## Setup

### 1. Start the MLflow server

```bash
source ideaweaver-env/bin/activate
mlflow server --host 127.0.0.1 --port 5000 --backend-store-uri sqlite:///mlflow.db
```

### 2. Train and register a model

```bash
ideaweaver train \
  --model bert-base-uncased \
  --dataset ./datasets/training_data.csv \
  --track-experiments \
  --mlflow-uri http://127.0.0.1:5000 \
  --mlflow-experiment "MyExperiment" \
  --register-model
```

#### Example Output
```
🤗 Using model: bert-base-uncased
📊 Experiment tracking enabled
🏷️  Model registration enabled
🚀 Starting model training...
2025/06/05 11:08:39 INFO mlflow.tracking.fluent: Experiment with name 'MyExperiment' does not exist. Creating a new experiment.
...
```

#### MLflow UI Example

![MLflow UI Example](images/mlflow_ui_example.png)

You can view your run and registered model in the MLflow UI at [http://127.0.0.1:5000](http://127.0.0.1:5000).

## Features

- Experiment tracking
- Model versioning
- Model registration
- Performance metrics logging
- Artifact storage
- Model deployment

## Best Practices

1. **Experiment Organization**
   - Use meaningful experiment names
   - Tag experiments appropriately
   - Document experiment parameters

2. **Model Registration**
   - Version your models
   - Add model descriptions
   - Track model lineage

3. **Performance Tracking**
   - Log all relevant metrics
   - Track resource usage
   - Monitor model performance

## Troubleshooting

### Common Issues

1. **Connection Errors**
   - Verify MLflow server is running
   - Check network connectivity
   - Validate URI format

2. **Authentication Issues**
   - Check credentials
   - Verify permissions
   - Ensure proper access

### Debug Mode

Enable verbose output for debugging:

```bash
ideaweaver train \
  --model bert-base-uncased \
  --dataset ./datasets/training_data.csv \
  --track-experiments \
  --mlflow-uri http://127.0.0.1:5000 \
  --verbose
```

## Resources

- [MLflow Documentation](https://mlflow.org/docs/latest/index.html)
- [Model Registry Guide](https://mlflow.org/docs/latest/model-registry.html)
- [Tracking Server Setup](https://mlflow.org/docs/latest/tracking.html#tracking-server) 