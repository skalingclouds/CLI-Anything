# CLI-Anything Development Patterns

> Auto-generated skill from repository analysis

## Overview

CLI-Anything is a Python-based platform for creating CLI harnesses that integrate various tools and services. The codebase follows a modular architecture where each tool (like Zoom, DrawIO, AnyGen) has its own dedicated harness with standardized structure. The project emphasizes multilingual documentation support and cross-platform compatibility.

## Coding Conventions

### File Naming
- Use `snake_case` for all file names
- CLI entry points: `{tool}_cli.py`
- Test files: `test_*.py` or `*_test.py`
- Documentation: `README.md`, `{TOOL}.md`

### Project Structure
```
{tool}/
├── agent-harness/
│   ├── cli_anything/
│   │   └── {tool}/
│   │       ├── __init__.py
│   │       ├── core/
│   │       ├── utils/
│   │       ├── tests/
│   │       └── {tool}_cli.py
│   └── setup.py
├── README.md
└── {TOOL}.md
```

### Setup.py Template
```python
setup(
    name='cli-anything-{tool}',
    url='https://github.com/HKUDS/CLI-Anything',
    packages=find_packages(),
    # ... other metadata
)
```

### Import Organization
- Mixed import style accepted
- Group imports: standard library, third-party, local
- Use relative imports within packages

## Workflows

### Add New Harness
**Trigger:** When someone wants to integrate a new application or service  
**Command:** `/new-harness`

1. Create new tool directory structure:
   ```bash
   mkdir -p {tool}/agent-harness/cli_anything/{tool}/{core,utils,tests}
   ```

2. Create core package files:
   ```python
   # {tool}/agent-harness/cli_anything/{tool}/__init__.py
   """CLI harness for {Tool}"""
   __version__ = "0.1.0"
   ```

3. Implement CLI entry point:
   ```python
   # {tool}/agent-harness/cli_anything/{tool}/{tool}_cli.py
   import argparse
   
   def main():
       parser = argparse.ArgumentParser(description='{Tool} CLI')
       # Add tool-specific arguments
       args = parser.parse_args()
       # Implement tool logic
   
   if __name__ == "__main__":
       main()
   ```

4. Create setup.py with correct metadata:
   ```python
   setup(
       name='cli-anything-{tool}',
       version='0.1.0',
       url='https://github.com/HKUDS/CLI-Anything',
       packages=find_packages(),
   )
   ```

5. Add comprehensive documentation (README.md, {TOOL}.md)

6. Create test structure with core and e2e tests

7. Update main README.md and README_CN.md with new tool section

8. Update .gitignore to include new directories

### Fix Setup.py Metadata
**Trigger:** When setup.py files have incorrect repository URLs or metadata  
**Command:** `/fix-setup-urls`

1. Identify setup.py files with placeholder URLs
2. Replace placeholder patterns:
   ```python
   # Before
   url='https://github.com/yourusername/your-repo'
   
   # After
   url='https://github.com/HKUDS/CLI-Anything'
   ```
3. Verify author and package name consistency
4. Update any other metadata inconsistencies

### Update README Documentation
**Trigger:** When documentation needs to be updated for new features or corrections  
**Command:** `/update-docs`

1. Update README.md with new content:
   ```markdown
   ## {Tool} Integration
   
   ### Installation
   ```bash
   cd {tool}/agent-harness
   pip install -e .
   ```
   
   ### Usage
   ```bash
   python -m cli_anything.{tool}.{tool}_cli
   ```
   ```

2. Create corresponding Chinese translation in README_CN.md

3. Ensure consistent formatting and cross-references between versions

4. Update table of contents if structure changed

### Add Platform Integration
**Trigger:** When adding support for a new development platform or IDE  
**Command:** `/add-platform`

1. Create platform-specific directory:
   ```
   {platform}/
   ├── scripts/
   │   ├── install.sh
   │   └── install.ps1
   ├── SKILL.md
   └── README.md
   ```

2. Implement cross-platform installation scripts:
   ```bash
   #!/bin/bash
   # install.sh
   set -e
   
   # Platform detection
   # Dependency installation
   # CLI-Anything setup
   ```

3. Create platform documentation (SKILL.md)

4. Update main README files with platform-specific instructions

5. Update .gitignore to include new platform directories

### Iterative Script Refinement
**Trigger:** When refining installation or setup scripts based on code review feedback  
**Command:** `/refine-script`

1. **Initial Implementation:** Create basic script functionality

2. **Error Handling:** Add comprehensive error checking:
   ```bash
   if ! command -v python3 &> /dev/null; then
       echo "Error: Python 3 is required"
       exit 1
   fi
   ```

3. **Robustness Improvements:**
   - Add backup mechanisms
   - Implement temporary file handling
   - Add JSON/config validation

4. **Platform-Specific Enhancements:**
   - Handle OS-specific paths
   - Add Windows PowerShell equivalents
   - Test cross-platform compatibility

5. **Final Polish:**
   - Update documentation
   - Add usage examples
   - Clean up debug code

## Testing Patterns

### Test Structure
```python
# test_core.py
import unittest
from cli_anything.{tool}.core import main_function

class Test{Tool}Core(unittest.TestCase):
    def test_basic_functionality(self):
        # Test core features
        pass
    
    def setUp(self):
        # Test setup
        pass
```

### End-to-End Testing
```python
# test_full_e2e.py  
def test_cli_integration():
    # Test complete CLI workflow
    pass
```

## Commit Conventions

Follow conventional commits with prefixes:
- `feat:` - New features
- `fix:` - Bug fixes  
- `docs:` - Documentation updates
- Keep messages under 50 characters when possible

## Commands

| Command | Purpose |
|---------|---------|
| `/new-harness` | Create complete new CLI harness for a tool |
| `/fix-setup-urls` | Fix placeholder URLs in setup.py files |
| `/update-docs` | Update both English and Chinese README files |
| `/add-platform` | Add support for new development platform/IDE |
| `/refine-script` | Iteratively improve setup/installation scripts |