# Contributing to Aadhaar Insight AI

Thank you for your interest in contributing to Aadhaar Insight AI! This document provides guidelines and instructions for contributing.

## Code of Conduct

Please be respectful and constructive in all interactions with other contributors.

## Getting Started

1. Fork the repository
2. Clone your fork locally
3. Create a new branch for your feature: `git checkout -b feature/your-feature-name`
4. Make your changes
5. Test your changes thoroughly
6. Commit with clear messages: `git commit -m "Add description of changes"`
7. Push to your fork: `git push origin feature/your-feature-name`
8. Create a Pull Request

## Development Setup

```bash
# Clone the repository
git clone <your-fork-url>
cd final_codes

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run the application
streamlit run dashboard.py
```

## Reporting Issues

When reporting bugs, please include:
- Python version
- Operating system
- Steps to reproduce
- Expected behavior
- Actual behavior
- Error messages/logs
- Data sample (anonymized if necessary)

## Feature Requests

When proposing features:
- Explain the use case
- Describe the expected behavior
- Provide mockups or examples if applicable
- Consider performance implications

## Code Style

- Follow PEP 8 guidelines
- Use meaningful variable names
- Add comments for complex logic
- Keep functions focused and modular
- Use type hints where appropriate

## Pull Request Process

1. Update README.md with any new features or changes
2. Ensure all tests pass
3. Update requirements.txt if adding dependencies
4. Keep commits atomic and well-documented
5. Reference any related issues in the PR description
6. Wait for review before merging

## Documentation

- Document new functions with docstrings
- Update README.md for user-facing changes
- Add comments for complex calculations
- Include examples for new features

## Areas for Contribution

- Bug fixes
- Performance improvements
- Documentation enhancements
- New visualization features
- Additional statistical metrics
- Data validation improvements
- UI/UX enhancements

## Questions?

Feel free to open an issue to ask questions or discuss potential contributions.
