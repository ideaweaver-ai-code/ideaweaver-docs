# Evaluation

Welcome to the Evaluation section! Here you'll find:
- How to run model evaluation with IdeaWeaver
- Examples for both TensorBoard and Weights & Biases (wandb)
- Screenshots and sample outputs
- Detailed command-line options and examples

---

![Evaluation Flow](images/evaluation.png)

## Command Line Options

```bash
ideaweaver evaluate --help

Usage: -c evaluate [OPTIONS] MODEL_PATH

  Evaluate a language model on various benchmarks.

Options:
  -t, --tasks TEXT                Comma-separated list of tasks to evaluate on
  -s, --benchmark-suite [standard|reasoning|knowledge|comprehensive|custom]
                                  Predefined benchmark suite to use
  -wp, --wandb-project TEXT       Weights & Biases project name
  -we, --wandb-entity TEXT        Weights & Biases entity name
  -d, --device TEXT               Device to run evaluation on (auto, cuda, cpu)
  -b, --batch-size INTEGER        Batch size for evaluation
  -f, --num-fewshot INTEGER       Number of few-shot examples
  -l, --limit INTEGER             Limit number of samples for testing
  -o, --output-path TEXT          Path to save evaluation results
  --generate-report               Generate markdown evaluation report
  --report-to [wandb|tensorboard|both|none]
                                  Experiment tracking platform
  --tensorboard-project TEXT      TensorBoard project name
  --tensorboard-experiment TEXT   Custom TensorBoard experiment name
  -v, --verbose                   Verbose output
  --help                          Show this message and exit.
```

## Basic Evaluation Example

Here's a basic example of running evaluation:

```bash
ideaweaver evaluate ./downloaded_model \
  --tasks hellaswag,arc_easy,winogrande \
  --batch-size 2 \
  --limit 2 \
  --output-path results.json \
  --report-to none \
  --verbose
```

### Understanding the Tasks
* HellaSwag – commonsense story completion
* ARC-Easy – grade-school science multiple choice
* Winogrande – pronoun resolution / commonsense coreference

### Key Parameters Explained
* `--limit 2`: Only scores the first two examples of each task (for pipeline testing)
* `--batch_size 2`: Feeds two prompts to the model at a time (useful for larger models on limited GPUs)
* `--device auto`: Automatically selects CUDA if available, otherwise uses CPU
* `--log_samples`: Generates per-example JSON in addition to aggregate metrics

## Sample Output Analysis

### Example Output with Limit=10
```
📋 Evaluation output:
hf (pretrained=./downloaded_model), gen_kwargs: (None), limit: 10.0, num_fewshot: None, batch_size: 2
|  Tasks   |Version|Filter|n-shot| Metric |   |Value|   |Stderr|
|----------|------:|------|-----:|--------|---|----:|---|-----:|
|arc_easy  |      1|none  |     0|acc     |↑  |  0.4|±  |0.1633|
|          |       |none  |     0|acc_norm|↑  |  0.3|±  |0.1528|
|hellaswag |      1|none  |     0|acc     |↑  |  0.3|±  |0.1528|
|          |       |none  |     0|acc_norm|↑  |  0.3|±  |0.1528|
|winogrande|      1|none  |     0|acc     |↑  |  0.7|±  |0.1528|
```

### Understanding the Metrics
* Raw scores (10 questions per benchmark):
  * ARC-Easy: 4/10 correct → 0.4
  * HellaSwag: 3/10 correct → 0.3
  * Winogrande: 7/10 correct → 0.7

* Metric Types:
  * `acc`: Raw accuracy
  * `acc_norm`: Normalized accuracy (after cleanup like stripping articles)
  * `StdErr`: Indicates confidence in the score (±0.15 means ±15% potential variation)

## TensorBoard Example

```bash
ideaweaver evaluate ./my-qwen2-model \
  --tasks hellaswag,arc_easy \
  --batch-size 2 \
  --output-path ./evaluation_results.json \
  --generate-report \
  --report-to tensorboard \
  --tensorboard-project my-eval-project \
  --limit 2 \
  --verbose
```

### Starting TensorBoard Server
```bash
pip install tensorboard  # Already included in installation
nohup tensorboard --logdir logs/ &
# Access at http://localhost:6006/
```

#### TensorBoard UI Example

![Example: TensorBoard visualization of evaluation metrics](images/tensorboard.png)

## Weights & Biases (wandb) Example

### Basic wandb Setup
```bash
ideaweaver evaluate ./downloaded_model \
  --tasks hellaswag,arc_easy \
  --batch-size 2 \
  --output-path ./wandb_results \
  --generate-report \
  --report-to wandb \
  --wandb-project my-wandb-eval-project \
  --wandb-entity laprashant-startup \
  --limit 100 \
  --verbose
```

### Using Both Platforms
```bash
ideaweaver evaluate ./downloaded_model \
  --tasks hellaswag,arc_easy \
  --batch-size 2 \
  --output-path ./wandb_results \
  --generate-report \
  --report-to both \
  --wandb-project my-wandb-eval-project \
  --wandb-entity laprashant-startup \
  --tensorboard-project my-tensorboard-eval-project \
  --limit 100 \
  --verbose
```

#### wandb UI Example

![Example: wandb visualization of evaluation metrics](images/wandb.png)

### wandb Setup Notes
* Run `wandb login` once to set up authentication
* Add `--report-to wandb` to enable wandb logging
* Optionally specify `--wandb-project` and `--wandb-entity`
* Note: Evaluation logs only summary metrics at the end, not per-batch metrics 