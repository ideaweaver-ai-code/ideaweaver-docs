# Model Context Protocol (MCP) Integration

## Overview

IdeaWeaver includes built-in support for **Model Context Protocol (MCP)**, enabling seamless integration with popular services like GitHub, Slack, AWS, and more. This integration allows AI models to access external data and tools through a standardized protocol.

![MCP Integration](images/mcp_integration.png)

## Quick Start

### 1. Check Dependencies
```bash
ideaweaver mcp check-deps
```

### 2. List Available Servers
```bash
ideaweaver mcp list-servers
```

### 3. Enable GitHub Server
```bash
# First, set up authentication
ideaweaver mcp setup-auth github

# Then enable the server
ideaweaver mcp enable github
```

## Available MCP Servers

| Server              | Description                                   | Authentication Required |
|---------------------|-----------------------------------------------|------------------------|
| GitHub              | Access repositories, issues, PRs, and more    | ✅ GitHub Token         |
| AWS CloudFormation  | AWS resource management and operations        | ✅ AWS Credentials      |
| Terraform           | Provider and module documentation             | ❌ No Auth Required     |

## GitHub Integration Examples

### Repository Search
```bash
ideaweaver mcp call-tool github search_repositories \
  --args '{"query": "machine learning", "perPage": 3}'
```

### File Contents Reading
```bash
ideaweaver mcp call-tool github get_file_contents \
  --args '{"owner": "100daysofdevops", "repo": "100daysofdevops", "path": "README.md"}'
```

### Issues Listing
```bash
ideaweaver mcp call-tool github list_issues \
  --args '{"owner": "100daysofdevops", "repo": "100daysofdevops"}'
```

### Pull Requests Listing
```bash
ideaweaver mcp call-tool github list_pull_requests \
  --args '{"owner": "100daysofdevops", "repo": "100daysofdevops"}'
```

## AWS CloudFormation Integration

1. Set up AWS authentication:
```bash
ideaweaver mcp setup-auth awslabs.cfn-mcp-server
```

2. Enable AWS CloudFormation server:
```bash
ideaweaver mcp enable awslabs.cfn-mcp-server
```

3. List S3 buckets:
```bash
ideaweaver mcp call-tool awslabs.cfn-mcp-server list_resources --args '{"resource_type": "AWS::S3::Bucket"}'
```

### List EC2 Instances
```bash
ideaweaver mcp call-tool awslabs.cfn-mcp-server list_resources \
  --args '{"resource_type": "AWS::EC2::Instance"}'
```

### Create an S3 Bucket
```bash
ideaweaver mcp call-tool awslabs.cfn-mcp-server create_resource \
  --args '{"resource_type": "AWS::S3::Bucket", "desired_state": {"BucketName": "my-test-bucket-12345"}}'
```

## Terraform Integration Examples

### Search for Terraform Modules
```bash
# Enable Terraform server
ideaweaver mcp enable terraform
```

2. Search for Terraform modules:
```bash
ideaweaver mcp call-tool terraform searchModules --args '{"moduleQuery": "aws-vpc"}'
```

Example output:
```
📦 **Terraform Module Search Results**

Available Terraform Modules (top matches) for aws-vpc

Each result includes:
  - moduleID: The module ID (format: namespace/name/provider-name/module-version)
  - Name: The name of the module
  - Description: A short description of the module
  - Downloads: The total number of times the module has been downloaded
  - Verified: Verification status of the module
  - Published: The date and time when the module was published

---

  - moduleID: Harshrai3112/aws-vpc/aws/1.0.0
  - Name: aws-vpc
  - Description:
  - Downloads: 5016
  - Verified: false
  - Published: 2021-06-04 08:59:52.979927 +0000 UTC
---

  - moduleID: Adaptavist/aws-vpc/module/1.1.3
  - Name: aws-vpc
  - Description:
  - Downloads: 860
  - Verified: false
  - Published: 2021-12-20 13:24:39.363039 +0000 UTC
---

  - moduleID: mars/aws-vpc/heroku/1.0.1
  - Name: aws-vpc
  - Description: AWS VPC ready for 🍐 Heroku Private Spaces
  - Downloads: 809
  - Verified: false
  - Published: 2018-10-09 18:15:04.500275 +0000 UTC
```

3. Get module details:
```bash
ideaweaver mcp call-tool terraform getModuleDetails \
  --args '{"moduleName": "terraform-aws-modules/vpc/aws"}'
```

## Server Management

### Check Status
```bash
ideaweaver mcp status
```

### Get Server Information
```bash
ideaweaver mcp server-info github
```

### Disable Server
```bash
ideaweaver mcp disable github
```

### Re-enable Server
```bash
ideaweaver mcp enable github
```

## Configuration

### User Configuration Location
- macOS/Linux: `~/.ideaweaver/mcp/config.json`
- Windows: `%USERPROFILE%\.ideaweaver\mcp\config.json`

### Environment Variables

Common environment variables used by MCP servers:

```bash
# GitHub
export GITHUB_PERSONAL_ACCESS_TOKEN=ghp_xxxxxxxxxxxx

# Slack
export SLACK_BOT_TOKEN=xoxb-xxxxxxxxxxxx
export SLACK_APP_TOKEN=xapp-xxxxxxxxxxxx

# AWS
export AWS_ACCESS_KEY_ID=AKIAXXXXXXXXXXXX
export AWS_SECRET_ACCESS_KEY=xxxxxxxxxxxx
export AWS_DEFAULT_REGION=us-east-1

# Google Drive
export GOOGLE_DRIVE_CREDENTIALS_FILE=/path/to/credentials.json
```

## Troubleshooting

### Common Issues

1. **"MCP not available" error**
   ```bash
   pip install mcp
   ```

2. **"Command 'npx' not found"**
   - Install Node.js from https://nodejs.org/
   - Restart your terminal

3. **Authentication failures**
   - Verify your tokens/credentials are correct
   - Check environment variables are set
   - Use `ideaweaver mcp setup-auth <server>` for interactive setup

4. **Connection timeouts**
   - Check your internet connection
   - Verify firewall settings
   - Some servers may take time to download on first use

### Debug Mode

Enable verbose output for debugging:

```bash
ideaweaver mcp list-servers --verbose
ideaweaver mcp test-connection github --verbose
ideaweaver mcp call-tool github search_repositories \
  --args '{"query": "test"}' --verbose
```

## Next Steps

1. **Start Simple**: Begin with servers that don't require authentication (time, memory, fetch)
2. **Add Authentication**: Set up tokens for GitHub, Slack, or AWS
3. **Integrate with RAG**: Use MCP servers as data sources in your RAG pipelines
4. **Build Workflows**: Combine multiple servers for complex AI workflows
5. **Develop Custom Servers**: Create MCP servers for your proprietary data sources 