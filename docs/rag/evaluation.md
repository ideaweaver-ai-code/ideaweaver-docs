# RAG Evaluation

IdeaWeaver provides comprehensive evaluation capabilities for RAG systems using the RAGAS framework. This allows you to assess the quality and performance of your knowledge bases.

## Evaluation Metrics

The RAGAS framework evaluates several key aspects of your RAG system:

- **Faithfulness**: Measures if the generated answer is factually consistent with the retrieved context
- **Answer Relevancy**: Assesses if the answer is relevant to the question
- **Context Relevancy**: Evaluates if the retrieved context is relevant to the question
- **Context Recall**: Measures how well the system retrieves all relevant information
- **Context Precision**: Assesses the precision of the retrieved information

## Basic Evaluation

```bash
ideaweaver rag evaluate --kb my-kb
```

This will:

1. Generate test questions
2. Run the evaluation
3. Display metrics
4. Generate a report

## Advanced Evaluation

### Custom Test Questions

```bash
ideaweaver rag evaluate --kb my-kb --questions-file custom_questions.json
```

### Specific Metrics

```bash
ideaweaver rag evaluate --kb my-kb --metrics faithfulness,answer_relevancy
```

### Compare Knowledge Bases

```bash
ideaweaver rag compare-kb --kb1 kb1 --kb2 kb2
```

## Generating Test Questions

```bash
ideaweaver rag generate-test-questions --kb my-kb
```

Options:

- `--num-questions`: Number of questions to generate
- `--output-file`: Save questions to a file
- `--question-types`: Types of questions to generate

## Example Output

```
🤖 Auto-generating 5 test questions
🧪 Starting RAGAS evaluation for KB: my-kb
📊 Metrics: faithfulness, answer_relevancy

📋 Evaluation Results:
----------------------------------------
Faithfulness: 0.85
Answer Relevancy: 0.92
Context Relevancy: 0.88
Context Recall: 0.90
Context Precision: 0.87

✅ Evaluation completed successfully!
📄 Report saved to: evaluation_report_my-kb.md
```

## Best Practices

1. **Regular Evaluation**: Evaluate your RAG system regularly as you add new documents
2. **Multiple Metrics**: Use multiple metrics to get a complete picture
3. **Custom Questions**: Create domain-specific test questions
4. **Compare Baselines**: Compare against baseline or previous versions
5. **Monitor Changes**: Track how metrics change over time

## Troubleshooting

Common issues and solutions:

**Low Faithfulness**

   - Check document quality
   - Review chunking strategy
   - Adjust retrieval parameters

**Low Relevancy**

   - Improve question understanding
   - Optimize embedding model
   - Review document preprocessing

**Low Recall**

   - Increase chunk overlap
   - Adjust chunk size
   - Review retrieval strategy

## Next Steps

- [RAG Commands](commands.md) - Complete command reference
- [RAG Overview](overview.md) - System architecture and features
- [Enterprise RAG Guide](../guides/enterprise-rag.md) - Production deployments 