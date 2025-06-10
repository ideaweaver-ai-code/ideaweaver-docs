# Support

Need help with IdeaWeaver? Here are the best ways to get assistance.

## Quick Help

### Common Issues

**Command not found**: Make sure your virtual environment is activated
```bash
source ideaweaver-env/bin/activate
```

**Import errors**: Reinstall requirements if packages are missing
```bash
pip install -r requirements.txt --force-reinstall
```

**GPU not detected**: Check CUDA installation
```bash
python -c "import torch; print(torch.cuda.is_available())"
```

### Documentation

- [Installation Guide](../getting-started/installation.md)
- [Quick Start](../getting-started/quick-start.md)
- [CLI Reference](../reference/cli-commands.md)

## Getting Help

### GitHub Issues

For bug reports and feature requests:
- Search existing issues first
- Use the provided templates
- Include relevant system information
- Provide steps to reproduce

### Community Support

- **GitHub Discussions**: General questions and community help

## FAQ

### Installation Issues

**Q: Python 3.12 not found**

A: Use the automated setup script which handles Python installation

**Q: Setup script fails**

A: Check the troubleshooting section in the installation guide

### Usage Questions

**Q: How do I fine-tune my own model?**

A: See the [Quick Start guide](../getting-started/quick-start.md) for LoRA fine-tuning examples

**Q: Can I use local models?**

A: Yes! IdeaWeaver supports local models and Hugging Face models

## Stay Updated

- ⭐ Star the repository on GitHub
- 📢 Follow us on Twitter @ideaweaver_ai