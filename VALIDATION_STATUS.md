# Configuration Validation Status

This repository uses automated validation to ensure configuration integrity. 

![Validation Status](https://github.com/DevSecNinja/home-assistant-config/actions/workflows/validate-config.yaml/badge.svg)

## What's Validated

- **YAML Syntax**: All configuration files are checked for valid YAML syntax
- **Home Assistant Configuration**: Official `hassfest` validation ensures integration compatibility  
- **ESPHome Configurations**: Device-specific validation for all ESPHome configs
- **Configuration Integrity**: Full Home Assistant setup validation

## Validation Runs

- ✅ On every push to `main` branch
- ✅ On all pull requests  
- ✅ Manual trigger available

## Local Development

For local validation before committing:

```bash
# Install and run pre-commit hooks
pip install pre-commit
pre-commit install
pre-commit run --all-files

# Manual validation
yamllint .
```

For detailed information, see [docs/VALIDATION.md](docs/VALIDATION.md).

---

*This validation system helps catch configuration errors early while respecting existing formatting and conventions.*