# Home Assistant Configuration Repository

This is a Home Assistant configuration repository containing YAML configuration files, ESPHome device configurations, automations, scripts, and templates. The configuration is organized using Home Assistant's package system and includes custom integrations managed through HACS.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

### Prerequisites and Setup
- Ensure Python 3.12+ is available: `python3 --version`
- Install Home Assistant Core: `pip3 install homeassistant` -- takes 2-3 minutes. NEVER CANCEL.
- Install colorlog dependency: `pip3 install colorlog==6.8.2`
- Install YAML linting: `pip3 install yamllint` 

### Validation and Testing
- **YAML Linting (REQUIRED)**: `yamllint .` -- takes 5 seconds. NEVER CANCEL. Set timeout to 30+ seconds.
  - **ALWAYS run YAML linting before committing changes** or CI may fail
  - Common issues: missing document start `---`, trailing spaces, line length >80 chars, indentation
- **Configuration Check**: `hass --script check_config -c .` 
  - **WARNING**: Will fail without secrets.yaml file (contains secret values)
  - Creates partial validation - checks syntax and structure
  - Takes 10-15 seconds. NEVER CANCEL. Set timeout to 60+ seconds.

### Key Repository Structure
```
.
├── configuration.yaml          # Main HA configuration (loads packages)
├── automations.yaml           # GUI-created automations (large file)
├── integrations/              # Package-based configuration files
│   ├── default_config.yaml   # Core HA integrations
│   ├── sensor.yaml           # Custom sensors
│   ├── influxdb.yaml         # Database configuration (uses secrets)
│   └── [24 other integration files]
├── templates/
│   └── README.j2             # Jinja template for auto-generating README
├── esphome/                  # ESPHome device configurations (32 files)
│   ├── common/               # Shared ESPHome packages
│   ├── components/           # Custom ESPHome components  
│   └── *.yaml               # Individual device configs
├── automations/              # Custom automation packages
├── blueprints/               # Home Assistant blueprints
└── scripts/                  # Custom scripts
```

## Validation Scenarios

### Always Test These Scenarios After Making Changes:
1. **YAML Syntax Validation**: 
   - Run `yamllint .` and ensure no syntax errors
   - Fix any indentation, trailing spaces, or line length issues
2. **Home Assistant Configuration Validation**:
   - Run `hass --script check_config -c .` 
   - Verify no new syntax errors are introduced (secret-related failures are expected)
3. **Git Integration**:
   - Check git status: `git --no-pager status`
   - Verify only intended files are modified

### Manual Testing Requirements:
- **CRITICAL**: This is a configuration-only repository - no application runtime testing is possible
- **Validation consists entirely of static configuration checking**
- **Never attempt to run Home Assistant server** - it requires hardware integrations, secrets, and network access not available in development environment

## Common Tasks

### Making Configuration Changes:
1. **Always check current branch**: `git --no-pager status`
2. **Edit YAML files** using proper indentation (2 spaces, no tabs)
3. **Validate immediately**: `yamllint <changed-file>`
4. **Run full lint**: `yamllint .` -- 5 seconds. NEVER CANCEL.
5. **Check HA config**: `hass --script check_config -c .` -- 15 seconds. NEVER CANCEL.
6. **Commit changes** with descriptive message

### ESPHome Device Configuration:
- ESPHome configurations use `packages` and `substitutions` for reusability
- Common configurations are in `esphome/common/`
- Device-specific configurations reference common packages
- **DO NOT attempt to compile ESPHome configurations** - requires specific hardware and network access

### Working with Integrations:
- Integration configs are in `integrations/` directory
- Each file represents a Home Assistant integration or package
- Main `configuration.yaml` loads all integrations via `packages: !include_dir_named integrations`
- **Secrets are stored separately** and not available in development environment

## Timing Expectations and Timeouts

| Command | Expected Time | Timeout Setting | Notes |
|---------|---------------|-----------------|-------|
| `yamllint .` | 5 seconds | 30 seconds | NEVER CANCEL - lints all 74+ YAML files |
| `hass --script check_config` | 15 seconds | 60 seconds | NEVER CANCEL - validates HA configuration |
| `pip3 install homeassistant` | 2-3 minutes | 300+ seconds | NEVER CANCEL - installs HA Core |
| `git --no-pager status` | 1 second | 10 seconds | Fast git operations |

## Repository Statistics
- **Total YAML files**: 74
- **Integration files**: 24
- **ESPHome configurations**: 32 (includes common packages, components, individual devices)
- **GitHub Actions workflows**: 1 (todo-to-issue)
- **Generated README**: Auto-generated from templates/README.j2

## Common File Locations

### Frequently Modified Files:
```bash
# View main configuration
cat configuration.yaml

# List all integration packages  
ls -la integrations/

# View automation structure
head -20 automations.yaml

# Check ESPHome devices
ls -la esphome/*.yaml
```

### Key Integration Files:
- `integrations/sensor.yaml` - Custom sensor definitions
- `integrations/influxdb.yaml` - Database integration (uses secrets)
- `integrations/default_config.yaml` - Core HA integrations
- `integrations/packages.yaml` - Package loading configuration

### Template System:
- `templates/README.j2` - Jinja template for README generation
- Template uses Home Assistant sensors to populate statistics
- **DO NOT manually edit README.md** - it's auto-generated

## Troubleshooting

### Common Issues:
1. **Secret-related errors**: Expected when secrets.yaml is not available
2. **YAML indentation**: Use 2 spaces, no tabs, consistent indentation
3. **Line length**: Keep lines under 80 characters
4. **Missing document start**: Add `---` at beginning of YAML files

### Quick Fixes:
```bash
# Fix YAML formatting issues
yamllint <file> --format parsable

# Check specific integration
hass --script check_config -c . | grep -A5 -B5 <integration_name>

# View git changes
git --no-pager diff
```

## CI/CD Integration

### GitHub Actions:
- **Only workflow**: `.github/workflows/todo-to-issue.yaml`
- Runs on push to main branch
- Converts TODO comments to GitHub issues
- **No automated testing or validation** - manual validation required

### Required Validations Before Commit:
1. `yamllint .` must pass without errors
2. `hass --script check_config -c .` should not introduce new errors
3. Git diff should show only intended changes

## Development Guidelines

### File Editing:
- **Use 2-space indentation consistently**
- **No trailing whitespace**
- **Keep lines under 80 characters**
- **Add `---` document start to new YAML files**

### Testing Changes:
- **Always lint before committing**: `yamllint .`
- **Check configuration syntax**: `hass --script check_config -c .`
- **Review git diff**: `git --no-pager diff`

### ESPHome Best Practices:
- Reuse common configurations from `esphome/common/`
- Use `substitutions` for device-specific values
- Reference existing device configs as templates
- **Maintain consistent naming conventions**

**CRITICAL REMINDER**: This repository contains configuration files only. Validation is limited to static analysis. Never attempt to run Home Assistant server or compile ESPHome configurations in development environment.