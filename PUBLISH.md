# Publishing BrowseVersa to PyPI

This guide covers the complete process of publishing the BrowseVersa package to PyPI. BrowseVersa is a Windows-specific browser version detection tool designed for Windows systems, Windows Server environments, and enterprise deployments.

## 📋 Prerequisites

### 1. Python Environment
- Python 3.6+ installed
- pip and setuptools updated
- Virtual environment recommended (optional but recommended)

### 2. Required Packages
```bash
pip install --upgrade pip setuptools wheel
pip install build twine
```

### 3. PyPI Account
- [PyPI account](https://pypi.org/account/register/) created
- [TestPyPI account](https://test.pypi.org/account/register/) created (recommended)
- API tokens generated for both accounts

### 4. Package Configuration
- `pyproject.toml` properly configured
- `README.md` updated and formatted
- `LICENSE` file included
- `MANIFEST.in` configured for file inclusion

## 🔧 Package Configuration

### 1. Project Metadata (`pyproject.toml`)
```toml
[project]
name = "browseversa"
version = "1.0.0"
description = "A comprehensive tool to detect web browser versions on Windows systems"
readme = "README.md"
license = "MIT"
authors = [
    {name = "Pandiyaraj Karuppasamy", email = "pandiyarajk@live.com"}
]
keywords = ["browser", "version", "detection", "windows", "automation"]
classifiers = [
    "Operating System :: Microsoft :: Windows",
    # ... other classifiers
]
```

### 2. Entry Points
```toml
[project.scripts]
browseversa = "browseversa:main"
```

### 3. URLs
```toml
[project.urls]
Homepage = "https://github.com/pandiyarajk/browseversa"
Repository = "https://github.com/pandiyarajk/browseversa"
```

## 🧪 Testing Before Publishing

### 1. Run Tests
```bash
# Install test dependencies
pip install pytest

# Run tests
pytest
```

### 2. Check Code Quality
```bash
# Code formatting
black browseversa.py

# Linting
flake8 browseversa.py

# Type checking
mypy browseversa.py
```

## 🔨 Building the Package

### 1. Clean Previous Builds

```bash
# Remove old build artifacts
Remove-Item -Recurse -Force dist
Remove-Item -Recurse -Force build
Remove-Item -Recurse -Force *.egg-info
```

### 2. Build Distribution Files

```bash
# Build both source and wheel distributions
python -m build
```

### 3. Verify Build Output

```bash
# List generated files
Get-ChildItem dist

# Expected output:
# browseversa-1.0.0-py3-none-any.whl
# browseversa-1.0.0.tar.gz
```

## ✅ Quality Checks

### 1. Check Package Metadata

```bash
# Validate distribution metadata
twine check dist/*
```

**Expected output**:
```
Checking dist\browseversa-1.0.0-py3-none-any.whl: PASSED
Checking dist\browseversa-1.0.0.tar.gz: PASSED
```

### 2. Test Package Installation

```bash
# Test installation from local files
pip install dist/browseversa-1.0.0-py3-none-any.whl

# Test the package
python -c "import browseversa; print(browseversa.__version__)"

# Uninstall test installation
pip uninstall browseversa -y
```

## 🧪 TestPyPI Upload (Recommended)

### 1. Upload to TestPyPI

```bash
# Upload to test environment
twine upload --repository testpypi dist/*
```

### 2. Verify TestPyPI Installation

```bash
# Install from TestPyPI
pip install --index-url https://test.pypi.org/simple/ browseversa

# Test functionality
browseversa --script-version

# Uninstall
pip uninstall browseversa -y
```

### 3. Check TestPyPI Page

- Visit [TestPyPI browseversa](https://test.pypi.org/project/browseversa/)
- Verify package information is correct
- Check that all files uploaded properly

## 🚀 Production PyPI Upload

### 1. Final Verification

```