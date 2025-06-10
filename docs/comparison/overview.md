# Model Comparison

The model comparison feature in IdeaWeaver allows you to evaluate and compare multiple language models using the lm-evaluation-harness framework. This powerful tool helps you make data-driven decisions about model selection and performance.

## Features

- **Multiple Model Comparison**: Compare any number of models side by side
- **Comprehensive Benchmarks**: Access to a wide range of evaluation tasks
- **Weights & Biases Integration**: Track and visualize comparison results
- **Customizable Evaluation**: Control batch size, few-shot examples, and more
- **Detailed Reports**: Generate markdown comparison reports

## Supported Tasks

The comparison tool supports various benchmark tasks from lm-evaluation-harness, including:

- **Language Understanding**: GLUE, SuperGLUE, RACE
- **Reasoning**: GSM8K, MATH, HumanEval
- **Knowledge**: MMLU, TruthfulQA
- **Generation**: LAMBADA, StoryCloze
- **And many more**: Check available tasks using `ideaweaver list-tasks`

## Integration with Weights & Biases

The comparison feature integrates with Weights & Biases for:
- Experiment tracking
- Performance visualization
- Result sharing
- Historical comparisons

## Example Use Cases

1. **Model Selection**: Compare different models for a specific task
2. **Version Comparison**: Evaluate improvements between model versions
3. **Hyperparameter Tuning**: Compare models with different configurations
4. **Architecture Analysis**: Compare different model architectures
5. **Resource Optimization**: Find the best model for your resource constraints

## Best Practices

1. **Task Selection**: Choose relevant tasks for your use case
2. **Resource Management**: Consider batch size and device selection
3. **Documentation**: Keep track of model versions and configurations
4. **Regular Updates**: Re-run comparisons when new models are available
5. **Result Analysis**: Use generated reports for detailed analysis 