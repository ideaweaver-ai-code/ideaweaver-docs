# AWS CloudFormation MCP Integration

## Overview

IdeaWeaver provides seamless integration with AWS CloudFormation through the Model Context Protocol (MCP), allowing you to manage AWS resources programmatically.

## Setup

1. Set up AWS authentication:
```bash
ideaweaver mcp setup-auth awslabs.cfn-mcp-server
```

2. Enable AWS CloudFormation server:
```bash
ideaweaver mcp enable awslabs.cfn-mcp-server
```

## Common Operations

### List Resources

#### List S3 Buckets
```bash
ideaweaver mcp call-tool awslabs.cfn-mcp-server list_resources \
  --args '{"resource_type": "AWS::S3::Bucket"}'
```

#### List EC2 Instances
```bash
ideaweaver mcp call-tool awslabs.cfn-mcp-server list_resources \
  --args '{"resource_type": "AWS::EC2::Instance"}'
```

### Create Resources

#### Create an S3 Bucket
```bash
ideaweaver mcp call-tool awslabs.cfn-mcp-server create_resource \
  --args '{"resource_type": "AWS::S3::Bucket", "desired_state": {"BucketName": "my-test-bucket-12345"}}'
```

## Configuration

### Required Environment Variables

```bash
# AWS Credentials
export AWS_ACCESS_KEY_ID=AKIAXXXXXXXXXXXX
export AWS_SECRET_ACCESS_KEY=xxxxxxxxxxxx
export AWS_DEFAULT_REGION=us-east-1
```

## Troubleshooting

### Common Issues

1. **Authentication Failures**
   - Verify AWS credentials are correct
   - Check environment variables are set
   - Ensure IAM user has necessary permissions

2. **Resource Creation Failures**
   - Check resource naming conflicts
   - Verify resource limits in your AWS account
   - Ensure IAM permissions include resource creation rights

### Debug Mode

Enable verbose output for debugging:

```bash
ideaweaver mcp call-tool awslabs.cfn-mcp-server list_resources \
  --args '{"resource_type": "AWS::S3::Bucket"}' --verbose
```

## Best Practices

1. **Security**
   - Use IAM roles with least privilege
   - Rotate AWS credentials regularly
   - Never commit AWS credentials to version control

2. **Resource Management**
   - Use meaningful resource names
   - Implement proper tagging strategy
   - Monitor resource usage and costs

3. **Error Handling**
   - Implement proper error checking
   - Use verbose mode for debugging
   - Monitor AWS CloudWatch logs 