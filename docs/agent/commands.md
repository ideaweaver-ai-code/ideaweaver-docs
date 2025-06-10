# Agent Commands

IdeaWeaver provides a comprehensive set of agent commands for various tasks. Each command is designed to leverage the power of AI agents to accomplish specific goals.

## LLM Requirements and Dependencies

IdeaWeaver's agent system is designed to work with multiple language model providers, with a preference for local models through Ollama for cost-effective operation.

### Ollama Setup (Recommended)

Ollama is the preferred LLM provider for IdeaWeaver agents. It provides:
- Free, local model inference
- No API costs
- Privacy and data security
- Offline operation capability

To set up Ollama:

1. Install Ollama:
   ```bash
   # macOS
   curl -fsSL https://ollama.com/install.sh | sh
   
   # Linux
   curl -fsSL https://ollama.com/install.sh | sh
   ```

2. Start the Ollama service:
   ```bash
   ollama serve
   ```

3. Pull a recommended model:
   ```bash
   ollama pull phi3:mini  # Fast and efficient
   # or
   ollama pull llama2:7b  # More capable but larger
   ```

### OpenAI Fallback

If Ollama is not available, IdeaWeaver will automatically fall back to using OpenAI's API. Please note:

- OpenAI usage incurs costs based on token consumption
- API key is required (set via OPENAI_API_KEY environment variable)
- Internet connection is required
- Usage is subject to OpenAI's rate limits and terms of service

To use OpenAI:

1. Obtain an API key from OpenAI
2. Set the environment variable:
   ```bash
   export OPENAI_API_KEY="your-api-key"
   ```

### Checking LLM Status

You can verify your LLM setup at any time:
```bash
ideaweaver agent check-llm
```

This will show:
- Available Ollama models (if installed)
- OpenAI API status (if configured)
- Current active provider
- Connection status

## Available Commands

To see all available agent commands:

```bash
ideaweaver agent --help
```

Example output:
```
Usage: ideaweaver agent [OPTIONS] COMMAND [ARGS]...

  Intelligent agent workflows for creative and analytical tasks.

  This command group provides access to various AI agents for tasks like:
  - Creative writing and story generation
  - Research and content creation
  - Social media content generation
  - Travel planning and recommendations
  - Stock market analysis

Options:
  --help  Show this message and exit.

Commands:
  check-llm         Check the status and availability of language model...
  generate_storybook  Generate a storybook with specified theme and target age
  linkedin_post     Create engaging LinkedIn posts for professional...
  research_write    Research and write comprehensive content on various...
  stock_analysis    Perform comprehensive stock market analysis
  travel_plan       Create personalized travel itineraries and...
```

## Check LLM Status

Verify your language model setup and availability:

```bash
ideaweaver agent check-llm
```

Example output:
```
🔍 Checking for Ollama availability...
✅ Ollama is available! Using model: phi3:mini
📋 Available models: deepseek-r1:1.5b, phi3:mini
✅ Created CrewAI LLM wrapper successfully

✅ LLM Status:
   Provider: ollama
   Model: phi3:mini
   Status: Connected and ready
```

## Generate Storybook

Generate an engaging and age-appropriate storybook:

```bash
ideaweaver agent generate_storybook --theme "brave little mouse" --target-age "3-5"
```

Options:

- `--theme`: The main theme or topic of the storybook
- `--target-age`: Target age range (e.g., "3-5", "6-8")
- `--num-pages`: Number of pages (default: 5)
- `--style`: Writing style (e.g., "whimsical", "educational")
- `--openai-api-key`: Your OpenAI API key (if not set in environment)

For a complete example of a generated storybook, see [Agent Examples](examples.md#storybook-generation).

## Research and Writing

Conduct research and create comprehensive content:

```bash
ideaweaver agent research_write --topic "AI in healthcare"
```

## LinkedIn Post Creation

Generate professional LinkedIn content:

```bash
ideaweaver agent linkedin_post --topic "AI trends in 2025"
```

## Travel Planning

Create detailed travel itineraries:

```bash
ideaweaver agent travel_plan --destination "Tokyo" --duration "7 days" --budget "$2000-3000"
```

## Stock Analysis

Perform comprehensive stock market analysis:

```bash
ideaweaver agent stock_analysis --symbol AAPL
```

## Command Options

Each command supports various options for customization:

- `--verbose`: Enable detailed output
- `--output`: Specify output file/directory
- `--format`: Choose output format (markdown, json, etc.)
- `--model`: Select specific LLM model
- `--temperature`: Adjust creativity level (0.0-1.0)

For detailed options for each command, use:

```bash
ideaweaver agent <command> --help
```

For example, to see options for the check-llm command:

```bash
ideaweaver agent check-llm --help
```

Example output:
```
Usage: ideaweaver agent check-llm [OPTIONS]

  Check the status and availability of language model providers.
  
  This command verifies:
  - Local model availability (Ollama)
  - API access (OpenAI)
  - Model capabilities
  - Connection status
  
  Useful for troubleshooting and ensuring required models are available
  for agent operations.

Options:
  --help  Show this message and exit.
``` 