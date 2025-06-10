# GitHub MCP Integration

## Overview

The GitHub MCP integration allows you to interact with GitHub repositories, issues, pull requests, and more through IdeaWeaver's Model Context Protocol.

## Setup

**Get a GitHub Personal Access Token**

   - Go to: https://github.com/settings/tokens
   - Create a token with repo, issues, and PR permissions

**Configure Authentication**

   ```bash
   # Set up authentication
   ideaweaver mcp setup-auth github
   
   # Or set environment variable
   export GITHUB_PERSONAL_ACCESS_TOKEN=your_token_here
   ```

3. **Enable the Server**
   ```bash
   ideaweaver mcp enable github
   ```

4. **Test the Connection**
   ```bash
   ideaweaver mcp test-connection github
   ```

## Available Operations

### Repository Search
```bash
ideaweaver mcp call-tool github search_repositories \
  --args '{"query": "100daysofdevops", "perPage": 3}'
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

### Repository Creation
```bash
ideaweaver mcp call-tool github create_repository \
  --args '{"name": "mcp-integration-test", "description": "Test repository", "private": false}'
```

### Issue Creation
```bash
ideaweaver mcp call-tool github create_issue \
  --args '{"owner": "100daysofdevops", "repo": "100daysofdevops", "title": "Test Issue", "body": "Test issue description"}'
```

### Comment Creation
```bash
ideaweaver mcp call-tool github add_issue_comment \
  --args '{"owner": "100daysofdevops", "repo": "100daysofdevops", "issue_number": 16, "body": "Test comment"}'
```

## Configuration

The GitHub MCP server configuration is stored in `~/.ideaweaver/mcp/config.json`:

```json
{
  "enabled_servers": [
    "awslabs.cfn-mcp-server",
    "github"
  ],
  "custom_servers": {},
  "default_settings": {
    "auto_connect": true,
    "timeout": 30
  },
  "server_configs": {
    "github": {
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "XXXXXXXXX"
      }
    }
  }
}
```

## Troubleshooting

### Common Issues

**Authentication Failures**

   - Verify your GitHub token has the correct permissions
   - Check if the token is properly set in environment variables
   - Try regenerating the token if issues persist

**Rate Limiting**

   - GitHub API has rate limits for authenticated and unauthenticated requests
   - Consider using a higher rate limit token for production use

**Connection Issues**

   - Check your internet connection
   - Verify GitHub API status at https://www.githubstatus.com/
   - Try using debug mode for more information:
     ```bash
     ideaweaver mcp call-tool github search_repositories \
       --args '{"query": "test"}' --verbose
     ```

## Best Practices

**Token Security**

   - Never commit tokens to version control
   - Use environment variables or secure credential storage
   - Rotate tokens regularly

**Rate Limiting**

   - Monitor your API usage
   - Implement appropriate caching for frequently accessed data
   - Use pagination for large result sets

**Error Handling**

   - Implement proper error handling in your workflows
   - Use the verbose flag for debugging
   - Check GitHub API status before critical operations 