# Validation Commands

The `validate` command in IdeaWeaver helps you verify your configuration files before running operations. This ensures that your setup is correct and helps prevent errors during execution.

## Basic Usage

```bash
ideaweaver validate --config <config_file>
```

### Arguments

- `config`: Path to the configuration file to validate (required)

## Examples

### Basic Validation

```bash
ideaweaver validate --config configs/config.yml
```

Example output:
```
🔍 Validating configuration file: config.yml
✅ Configuration is valid
📋 Validation summary:
   - All required fields are present
   - Schema validation passed
   - Dependencies are properly configured
```


Example output:
```
✅ Configuration is valid!
✅ Model google/bert_uncased_L-2_H-128_A-2 is accessible
```

## Error Handling

The validation command provides detailed error messages when issues are found:

```bash
ideaweaver validate --config config/training_config.yaml
```

Example output:
```
❌ Invalid configuration: Missing required field: project_name
```

## Best Practices

1. **Validate Early**: Run validation before starting any operation
2. **Use Verbose Mode**: When debugging configuration issues
3. **Version Control**: Keep validated configurations in version control
4. **Documentation**: Document any special configuration requirements 