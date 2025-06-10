# Langfuse Cloud Integration

To enable prompt monitoring and tracing with Langfuse Cloud, set the following environment variables in your shell or `.env` file:

```bash
export LANGFUSE_PUBLIC_KEY="your-public-key"
export LANGFUSE_SECRET_KEY="your-secret-key"
export LANGFUSE_HOST="https://cloud.langfuse.com"
```

You can find your API keys in the Langfuse dashboard under **Project Settings > API Keys**.

## Langfuse Prompt Monitoring via CLI

You can monitor prompts and generations in your LLM workflows using the IdeaWeaver CLI's Langfuse integration. Here's how to test and use prompt monitoring:

### 1. Check Langfuse Connection
```bash
ideaweaver langfuse status
```
- Verifies your environment variables and Langfuse Cloud connectivity.

### 2. Monitor a Command
Wrap any supported IdeaWeaver command to log its prompts and generations:
```bash
ideaweaver langfuse monitor evaluate --model my-model --tasks hellaswag
```
- This logs all prompts and generations from the `evaluate` command to Langfuse.
- You can use any other supported subcommand (e.g., `train`, `rag query`, etc.).

### 3. List Recent Traces
```bash
ideaweaver langfuse list-traces
```
- Shows recent monitored runs (traces) that have been logged to Langfuse.

### 4. Show Details of a Trace
```bash
ideaweaver langfuse show-trace <trace-id>
```
- Replace `<trace-id>` with the ID from `list-traces`.
- Prints details of the trace, including prompts and generations, in your terminal.

### 5. What to Expect in the Langfuse Dashboard
- Each monitored command creates a new trace in Langfuse.
- Click into a trace to see all prompt and generation events, including their input and output.

#### Example End-to-End Test
```bash
ideaweaver langfuse status
ideaweaver langfuse monitor evaluate --model my-model --tasks hellaswag
ideaweaver langfuse list-traces
ideaweaver langfuse show-trace <trace-id>
```

For more details, see the Langfuse section in the documentation or your GitHub Pages site. 