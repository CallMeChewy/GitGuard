![Project Himalaya](./Project_Himalaya_Banner.png)

# GitGuard Development Guide

*Part of Project Himalaya - AI-Human Collaborative Development Framework*

## 🔒 Security Bootstrapping 

### The Chicken-and-Egg Problem

GitGuard is a security tool designed to prevent credential exposure in git repositories. However, during its own development, we face an interesting challenge: **How do we secure GitGuard's development using GitGuard itself?**

### Our Solution

1. **Manual Security Review**: During development, all commits are manually reviewed for security issues
2. **Conservative .gitignore**: We use an extensive .gitignore that covers all possible security patterns
3. **No Secrets in Code**: All examples use placeholder values, never real credentials
4. **Scripts Isolation**: Development scripts are stored in `..Scripts/` to avoid path confusion

### Development Security Checklist

Before any commit to GitGuard:

- [ ] **No real credentials**: All API keys, passwords, tokens are placeholders
- [ ] **No sensitive files**: No actual configuration files with real values
- [ ] **Clean examples**: All examples use dummy data
- [ ] **Path verification**: No absolute paths that could expose system information
- [ ] **Review patterns**: Ensure security patterns don't match our own development files

## 🚀 Development Workflow

### Initial Setup

```bash
# Clone the repository
git clone https://github.com/herbbowers/gitguard.git
cd gitguard

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install in development mode
pip install -e ".[dev]"
```

### Running GitGuard on Itself

Once GitGuard is functional, we can test it on its own repository:

```bash
# Scan GitGuard's own repository
python -m gitguard scan

# Test GitGuard's own .gitignore patterns
python -m gitguard scan --full

# Validate GitGuard follows its own rules
python -m gitguard status
```

### Development Scripts

Development scripts are located in `..Scripts/` (note the `..` prefix to avoid confusion with the `scripts/` directory that might be included in the package).

```bash
# Access development scripts
cd ..Scripts/
ls -la
```

**Why `..Scripts/`?**
- **Path Clarity**: Distinguishes from package scripts
- **Auto-ignored**: Automatically ignored by .gitignore patterns
- **No Confusion**: Won't be mistaken for part of the GitGuard package

## 🧪 Testing Security Features

### Self-Testing

GitGuard includes tests that validate its own security patterns:

```bash
# Test that GitGuard detects common credential patterns
pytest tests/test_validator.py::TestSecurityValidator::test_content_scanning_aws_keys

# Test that GitGuard's .gitignore is comprehensive
pytest tests/test_security_bootstrap.py
```

### Manual Security Validation

Regular security reviews of our own repository:

```bash
# Manual credential scan
grep -r "AKIA[0-9A-Z]\{16\}" . --exclude-dir=.git
grep -r "sk-[a-zA-Z0-9]\{32\}" . --exclude-dir=.git
grep -r "eyJ[A-Za-z0-9_/+-]*\." . --exclude-dir=.git

# Check for common secrets
find . -name "*.env*" -not -path "./.git/*"
find . -name "*secret*" -not -path "./.git/*"
find . -name "*credential*" -not -path "./.git/*"
```

## 📦 Release Security

### Pre-Release Checklist

Before any release:

- [ ] **Full security scan**: Run GitGuard on itself
- [ ] **Dependency audit**: Check all dependencies for vulnerabilities
- [ ] **Example validation**: Ensure all examples use dummy data
- [ ] **Documentation review**: No sensitive information in docs
- [ ] **Build artifact scan**: Scan distribution packages

### Release Process

```bash
# 1. Security validation
python -m gitguard scan --full

# 2. Run all tests
pytest

# 3. Build package
python setup.py sdist bdist_wheel

# 4. Scan build artifacts
python -m gitguard scan dist/

# 5. Upload to PyPI (after validation)
twine upload dist/*
```

## 🏔️ Project Himalaya Integration

### Attribution in Development

Every development file includes proper attribution:

```python
# Author: Claude (Anthropic), as part of Project Himalaya
```

### Development Philosophy

Following Project Himalaya principles:

- **Documentation-Driven**: Write docs before code
- **Modular Architecture**: Keep modules focused and under 500 lines
- **Knowledge Persistence**: Maintain context across development sessions
- **AI-Human Collaboration**: Leverage both human creativity and AI implementation

## 🔧 Development Tools

### Recommended Tools

```bash
# Code formatting
black gitguard/

# Linting
flake8 gitguard/

# Type checking
mypy gitguard/

# Security scanning (once GitGuard is functional)
python -m gitguard scan
```

### IDE Setup

For VS Code, recommended extensions:
- Python
- GitLens
- Better Comments
- Error Lens

## 🚨 Security Incident Response

If a security issue is found in GitGuard itself:

1. **Immediate Assessment**: Determine scope and impact
2. **Fix Development**: Develop fix in private branch
3. **Testing**: Thoroughly test the fix
4. **Coordinated Disclosure**: Follow responsible disclosure practices
5. **Release**: Push fix and notify users
6. **Post-Mortem**: Document lessons learned

## 📚 Resources

- **Project Himalaya Documentation**: `../Docs/ProjectHimalaya/`
- **Security Patterns Reference**: `gitguard/validator.py`
- **Test Examples**: `tests/`
- **Development Scripts**: `..Scripts/`

---

*"The best security tool is one that secures itself as rigorously as it secures others."*

— GitGuard Development Philosophy