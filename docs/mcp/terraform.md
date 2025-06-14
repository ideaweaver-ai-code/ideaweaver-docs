# Terraform MCP Integration

## Overview

IdeaWeaver provides integration with Terraform through the Model Context Protocol (MCP), allowing you to search and manage Terraform modules and providers.

## Setup

Enable Terraform server:
```bash
ideaweaver mcp enable terraform
```

## Module Operations

### Search for Terraform Modules
```bash
ideaweaver mcp call-tool terraform searchModules \
  --args '{"moduleQuery": "aws-vpc"}'
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
```

### Get Module Details
```bash
ideaweaver mcp call-tool terraform getModuleDetails \
  --args '{"moduleName": "terraform-aws-modules/vpc/aws"}'
```

## Best Practices

1. **Module Selection**
   - Check module verification status
   - Review download statistics
   - Read module documentation
   - Verify module compatibility

2. **Version Management**
   - Use specific version numbers
   - Test module updates in staging
   - Keep track of module dependencies

3. **Security**
   - Use verified modules when possible
   - Review module source code
   - Check for known vulnerabilities

## Troubleshooting

### Common Issues

1. **Module Not Found**
   - Verify module name is correct
   - Check module namespace
   - Ensure module is public

2. **Version Conflicts**
   - Check provider version compatibility
   - Verify module version exists
   - Review version constraints

### Debug Mode

Enable verbose output for debugging:

```bash
ideaweaver mcp call-tool terraform searchModules \
  --args '{"moduleQuery": "aws-vpc"}' --verbose
```

## Next Steps

1. **Explore Modules**: Search for modules in the Terraform Registry
2. **Review Documentation**: Read module documentation and examples
3. **Test Integration**: Try different module operations
4. **Build Workflows**: Combine with other MCP servers for complex operations 