# Agent Overview

IdeaWeaver's Agent system provides powerful AI-powered workflows for various tasks. These agents are designed to work together to accomplish complex goals through intelligent task planning and execution.

## LLM Requirements

IdeaWeaver agents require a language model provider to function. The system is designed to work with:

**Ollama (Recommended)**

   - Free, local model inference
   - No API costs
   - Privacy and data security
   - Offline operation capability

**OpenAI (Fallback)**

   - Cloud-based API access
   - Paid service based on token usage
   - Requires internet connection
   - Requires API key

For detailed setup instructions, see the [Agent Commands](commands.md) page.

## Key Features

- **Intelligent Task Planning**: Agents can break down complex tasks into manageable steps
- **Multi-Agent Collaboration**: Different agents can work together on related tasks
- **Tool Integration**: Access to various tools and APIs for enhanced capabilities
- **Progress Tracking**: Monitor agent activities and task completion
- **Context Awareness**: Maintains context across multiple interactions
- **Flexible LLM Integration**: Seamless switching between local and cloud models

## Available Agents

1. **Research Agent**: Conducts thorough research on given topics
2. **Writer Agent**: Creates high-quality content based on research
3. **Reviewer Agent**: Ensures content quality and accuracy
4. **Planner Agent**: Creates detailed plans for various tasks
5. **Analyst Agent**: Performs data analysis and generates insights

## Getting Started

To start using agents, first check your LLM setup:

```bash
ideaweaver agent check-llm
```

Then explore the various agent commands available:

```bash
ideaweaver agent --help
```

For detailed information about specific commands and LLM setup, see the [Agent Commands](commands.md) page. 