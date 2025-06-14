# AWS Bedrock Model Registry Integration

## Overview

IdeaWeaver integrates with AWS Bedrock for model hosting and deployment. This guide shows you how to use AWS Bedrock with IdeaWeaver for model management and inference.

## Setup

### Train and Deploy a Model

```bash
source ideaweaver-env/bin/activate
ideaweaver train \
  --model sshleifer/tiny-distilbert-base-cased \
  --dataset ./datasets/training_data.csv \
  --deploy-to-bedrock \
  --aws-region us-east-1 \
  --aws-access-key-id <your-access-key> \
  --aws-secret-access-key <your-secret-key>
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
🚀 Deploying model to AWS Bedrock...
✅ Model deployed successfully to AWS Bedrock
```

### AWS Bedrock Console Example

Once your model is deployed, you can view it in the AWS Bedrock Console:

![AWS Bedrock Console Screenshot](images/bedrock_console.png)

## Features

- Model hosting
- Serverless deployment
- Auto-scaling
- Cost optimization
- Security features
- Monitoring tools

## Configuration

### Required Parameters

- `--deploy-to-bedrock`: Flag to enable AWS Bedrock deployment
- `--aws-region`: AWS region for deployment
- `--aws-access-key-id`: AWS access key
- `--aws-secret-access-key`: AWS secret key

### AWS Credentials Setup

1. Go to [AWS IAM Console](https://console.aws.amazon.com/iam/)
2. Create a new IAM user
3. Attach necessary permissions
4. Generate access keys
5. Use keys in your training command

## Best Practices

1. **Security**
   - Use IAM roles
   - Enable encryption
   - Monitor access

2. **Cost Management**
   - Set up budgets
   - Monitor usage
   - Optimize resources

3. **Deployment**
   - Use appropriate instance types
   - Configure auto-scaling
   - Set up monitoring

## Troubleshooting

### Common Issues

1. **Authentication Errors**
   - Verify AWS credentials
   - Check IAM permissions
   - Ensure proper access

2. **Deployment Issues**
   - Check region availability
   - Verify resource limits
   - Monitor CloudWatch logs

### Debug Mode

Enable verbose output for debugging:

```bash
ideaweaver train \
  --model sshleifer/tiny-distilbert-base-cased \
  --dataset ./datasets/training_data.csv \
  --deploy-to-bedrock \
  --aws-region us-east-1 \
  --verbose
```

## Resources

- [AWS Bedrock Documentation](https://docs.aws.amazon.com/bedrock/)
- [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [CloudWatch Monitoring](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html) 