# GitGuard Test Suite

<img src="../Project_Himalaya_Icon_Round_256.png" alt="Project Himalaya" width="32" height="32" style="vertical-align: middle;"> *Part of Project Himalaya*

This directory contains the test suite for GitGuard.

## Running Tests

### Prerequisites
```bash
pip install -e ".[dev]"
```

### Run All Tests
```bash
pytest
```

### Run with Coverage
```bash
pytest --cov=gitguard
```

### Run Specific Tests
```bash
pytest tests/test_validator.py
pytest tests/test_cli.py -v
```

## Test Structure

- **`test_validator.py`**: Security validation engine tests
- **`test_cli.py`**: Command line interface tests (coming soon)
- **`test_config.py`**: Configuration management tests (coming soon)
- **`test_integration.py`**: End-to-end integration tests (coming soon)

## Contributing Tests

When adding new features:
1. **Write tests first** (TDD approach)
2. **Cover edge cases** and error conditions
3. **Mock external dependencies** (git, filesystem)
4. **Follow naming conventions**: `test_<functionality>`

See [Contributing Guide](../CONTRIBUTING.md) for detailed testing guidelines.

## Test Coverage Goals

- **Core Functionality**: 95%+ coverage
- **CLI Commands**: 90%+ coverage
- **Configuration**: 85%+ coverage
- **Error Handling**: 100% coverage