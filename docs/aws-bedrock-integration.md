# AWS Bedrock Integration Guide

## Overview

This guide provides detailed instructions for integrating and deploying models to AWS Bedrock using IdeaWeaver. AWS Bedrock is a fully managed service that makes it easy to build and scale generative AI applications with foundation models.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Model Requirements](#model-requirements)
- [Deployment Process](#deployment-process)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)

## Prerequisites

### AWS Account Setup
1. AWS Account with Bedrock access enabled
2. IAM Role with necessary permissions
3. S3 Bucket in us-east-1 region

### Required Permissions

#### IAM Role Policy
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "bedrock:*"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::aws-bedrock-ideaweaver-bucket-use1",
                "arn:aws:s3:::aws-bedrock-ideaweaver-bucket-use1/*"
            ]
        }
    ]
}
```

#### S3 Bucket Policy
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowBedrockAccess",
            "Effect": "Allow",
            "Principal": {
                "Service": "bedrock.amazonaws.com"
            },
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::aws-bedrock-ideaweaver-bucket-use1",
                "arn:aws:s3:::aws-bedrock-ideaweaver-bucket-use1/*"
            ]
        }
    ]
}
```

## Setup

1. **Create S3 Bucket**
   ```bash
   aws s3api create-bucket \
     --bucket aws-bedrock-ideaweaver-bucket-use1 \
     --region us-east-1
   ```

2. **Configure Bucket Settings**
   ```bash
   # Disable ACLs
   aws s3api put-bucket-ownership-controls \
     --bucket aws-bedrock-ideaweaver-bucket-use1 \
     --ownership-controls Rules=[{ObjectOwnership=BucketOwnerEnforced}]
   ```

3. **Create IAM Role**
   ```bash
   aws iam create-role \
     --role-name bedrock-admin-role \
     --assume-role-policy-document file://trust-policy.json
   ```

## Model Requirements

### Supported Architectures
- llama
- mistral
- t5
- mixtral
- gpt_bigcode
- mllama
- qwen2_vl
- qwen2
- qwen2_5_vl

### Model Structure
```
my-qwen2-model/
├── config.json
├── pytorch_model.bin
├── tokenizer.json
└── tokenizer_config.json
```

## Deployment Process

### 1. Prepare Model
```bash
# Download supported model
git lfs install
git clone https://huggingface.co/Qwen/Qwen2-0.5B my-qwen2-model
```

### 2. Upload to S3
```bash
# Upload model files
aws s3 sync ./my-qwen2-model s3://aws-bedrock-ideaweaver-bucket-use1/bedrock-models/my-qwen2-model/
```

### 3. Deploy to Bedrock
```bash
# Deploy using IdeaWeaver
ideaweaver deploy bedrock \
  --model-path ./my-qwen2-model \
  --model-name my-qwen2-model \
  --s3-bucket aws-bedrock-ideaweaver-bucket-use1 \
  --region us-east-1
```

## Troubleshooting

### Common Issues

1. **Region Mismatch**
   - Error: "Amazon Bedrock does not have access to the S3 location"
   - Solution: Ensure S3 bucket is in us-east-1

2. **Permission Issues**
   - Error: "Access Denied"
   - Solution: Verify IAM role and bucket policies

3. **Model Architecture**
   - Error: "Amazon bedrock does not support the architecture"
   - Solution: Use only supported architectures

4. **Import Job Quotas**
   - Error: "Your account does not have the quota limits"
   - Solution: Request quota increase

### Debugging Steps

1. **Verify S3 Access**
   ```bash
   aws s3 ls s3://aws-bedrock-ideaweaver-bucket-use1/bedrock-models/my-qwen2-model/
   ```

2. **Check IAM Role**
   ```bash
   aws iam get-role --role-name bedrock-admin-role
   ```

3. **Validate Model**
   ```bash
   ideaweaver bedrock validate-model ./my-qwen2-model
   ```

## Best Practices

1. **Model Selection**
   - Start with smaller models (e.g., Qwen2-0.5B)
   - Verify architecture compatibility
   - Test locally before deployment

2. **S3 Organization**
   - Use consistent naming conventions
   - Organize models in subdirectories
   - Enable versioning for important models

3. **Security**
   - Use IAM roles with minimal permissions
   - Disable ACLs on S3 buckets
   - Regularly audit access policies

4. **Monitoring**
   - Track import job status
   - Monitor model performance
   - Set up CloudWatch alarms

## Additional Resources

- [AWS Bedrock Documentation](https://docs.aws.amazon.com/bedrock/)
- [IdeaWeaver CLI Reference](https://your-username.github.io/model-registry/cli-reference)
- [Model Import Best Practices](https://docs.aws.amazon.com/bedrock/latest/userguide/model-import.html) 