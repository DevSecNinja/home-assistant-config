# Configuration Validation

This repository uses automated validation to ensure configuration integrity and catch potential issues early.

## Validation Types

### 1. YAML Linting (`yamllint`)
- **Purpose**: Validates YAML syntax and formatting
- **Scope**: All YAML files except ESPHome configs and blueprints
- **Configuration**: `.yamllint`
- **What it checks**: Syntax errors, basic formatting consistency

### 2. Home Assistant Configuration Validation (`hassfest`)
- **Purpose**: Validates Home Assistant configuration structure
- **Scope**: All Home Assistant configuration files
- **What it checks**: Integration compatibility, configuration structure, deprecated features

### 3. ESPHome Configuration Validation
- **Purpose**: Validates ESPHome device configurations
- **Scope**: All `.yaml` files in the `esphome/` directory
- **What it checks**: ESPHome-specific syntax and component compatibility

### 4. Home Assistant Config Check
- **Purpose**: Comprehensive Home Assistant configuration validation
- **Scope**: Complete Home Assistant setup
- **What it checks**: Full configuration integrity, integration setup, template syntax

### 5. Markdown Linting
- **Purpose**: Ensures consistent markdown formatting
- **Scope**: Markdown files (excluding auto-generated `README.md`)
- **Configuration**: `.markdownlint.json`

## When Validation Runs

- **Push to main**: All validation checks
- **Pull requests**: All validation checks
- **Manual trigger**: Available via GitHub Actions UI

## Local Validation (Optional)

### Pre-commit Hooks
```bash
pip install pre-commit
pre-commit install
pre-commit run --all-files
```

### Manual Validation
```bash
# YAML linting
yamllint .

# Home Assistant config check
docker run --rm -v "$PWD":/config homeassistant/home-assistant:stable \
  python -m homeassistant --config /config --script check_config

# ESPHome validation
esphome config esphome/device.yaml
```

## Configuration Files

- `.yamllint` - YAML linting configuration
- `.markdownlint.json` - Markdown linting rules
- `.pre-commit-config.yaml` - Pre-commit hooks configuration
- `.github/workflows/validate-config.yaml` - Main validation workflow

## Troubleshooting

### Common Issues

1. **YAML Syntax Errors**: Check indentation and quotes
2. **Missing Dependencies**: Ensure all custom integrations are properly configured
3. **Template Errors**: Validate Jinja2 templates in automations and sensors
4. **ESPHome Errors**: Check component compatibility and pin assignments

### Getting Help

- Check the GitHub Actions logs for detailed error messages
- Refer to [Home Assistant Documentation](https://www.home-assistant.io/docs/)
- Review [ESPHome Documentation](https://esphome.io/) for device-specific issues