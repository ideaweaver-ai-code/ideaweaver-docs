# Download Commands

## Basic Download

Download a model from Hugging Face Hub:

```bash
ideaweaver download <model_name>
```

### Example
```bash
ideaweaver download microsoft/DialoGPT-medium
```

## Advanced Options

### Specify Output Directory

Download a model to a specific directory:

```bash
ideaweaver download <model_name> --save-path <path>
```

### Example
```bash
ideaweaver download microsoft/DialoGPT-medium --save-path ./my_models
```

## Troubleshooting

### Common Issues

**Download Fails**

   - Check your internet connection
   - Verify the model name is correct
   - Ensure you have sufficient disk space

**File Verification Fails**

   - Check for disk space issues
   - Verify file permissions
