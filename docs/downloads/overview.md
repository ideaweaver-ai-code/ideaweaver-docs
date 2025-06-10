# Model Downloads

IdeaWeaver provides a simple and efficient way to download models from the Hugging Face Hub. The download functionality allows you to:

- Download models directly from Hugging Face Hub
- Specify model variants and versions
- Automatically handle model dependencies
- Verify downloaded model integrity

## Basic Usage

The simplest way to download a model is using the `download` command:

```bash
ideaweaver download <model_name>
```

For example, to download the DialoGPT-medium model:

```bash
ideaweaver download microsoft/DialoGPT-medium
```

## Output Example

When downloading a model, you'll see output similar to this:

```
🔍 Downloading model: microsoft/DialoGPT-medium
📦 Model files:
   - config.json
   - pytorch_model.bin
   - tokenizer.json
   - tokenizer_config.json
   - special_tokens_map.json
✅ Model downloaded successfully to: ./models/microsoft/DialoGPT-medium
```

## Model Directory Structure

After downloading, the model will be stored in a directory structure like this:

```
./models/
└── microsoft/
    └── DialoGPT-medium/
        ├── config.json
        ├── pytorch_model.bin
        ├── tokenizer.json
        ├── tokenizer_config.json
        └── special_tokens_map.json
```

## Next Steps

- Learn about [download commands](commands.md) for advanced options
- Check out the [fine-tuning guide](../fine-tuning/overview.md) to start training with your downloaded model
- Explore [RAG capabilities](../rag/overview.md) to use your model in a retrieval-augmented generation system 