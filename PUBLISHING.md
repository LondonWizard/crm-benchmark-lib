# Publishing Guide for CRM Benchmark Library

This guide explains how to publish new versions of the `crm-benchmark-lib` package to PyPI.

## Prerequisites

- PyPI account with publishing rights
- GitHub repository access
- Python 3.7+
- Build and twine packages: `pip install build twine`

## Manual Publishing Steps

1. **Update Version**:
   - Update the version in `crm_benchmark_lib/__init__.py`
   - Update the version in `setup.py`
   - Commit these changes

2. **Create Release**:
   - Tag the release: `git tag -a v0.2.1 -m "Release v0.2.1"`
   - Push the tag: `git push origin v0.2.1`

3. **Build Distribution**:
   ```bash
   python -m build
   ```
   This creates both source and wheel distributions in the `dist/` directory.

4. **Upload to TestPyPI** (optional but recommended):
   ```bash
   python -m twine upload --repository testpypi dist/*
   ```

5. **Test the TestPyPI package**:
   ```bash
   pip install --index-url https://test.pypi.org/simple/ crm-benchmark-lib
   ```

6. **Upload to PyPI**:
   ```bash
   python -m twine upload dist/*
   ```

## Automated Publishing with GitHub Actions

The repository includes a GitHub Actions workflow that automatically publishes the package when a new tag starting with "v" is pushed:

1. **Update Version and Tag**:
   ```bash
   # Update versions in files
   git add .
   git commit -m "Bump version to x.y.z"
   git tag -a vx.y.z -m "Release vx.y.z"
   git push origin main --tags
   ```

2. **GitHub Actions Workflow**:
   - The workflow in `.github/workflows/python-package.yml` will:
     - Run tests
     - Build the package
     - Publish to PyPI

3. **Add Secrets**:
   - Add your PyPI credentials as GitHub secrets:
     - `PYPI_USERNAME`: Your PyPI username
     - `PYPI_PASSWORD`: Your PyPI password or token

## Development Workflow

1. **Make Changes**: Implement new features or fix bugs.
2. **Add Tests**: Add tests for new functionality.
3. **Run Tests**: Run `pytest` to ensure everything works.
4. **Update Documentation**: Update README and docstrings.
5. **Bump Version**: Increment version based on [Semantic Versioning](https://semver.org/).
6. **Publish**: Follow the steps above to release a new version. 