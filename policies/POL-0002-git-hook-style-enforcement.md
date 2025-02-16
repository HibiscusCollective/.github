# Git Hook Style Enforcement - POL-0002

**Authors**: Pierre Fouilloux (@pfouilloux)

![Accepted](https://img.shields.io/badge/status-accepted-green)
![Date](https://img.shields.io/badge/Date-16_Feb_2025-lightblue)
![Policy Type](https://img.shields.io/badge/category-technical-orange)
![Approval Model](https://img.shields.io/badge/approved_by-project_lead-red)

## Context and Problem Statement

Maintaining consistent code style across multiple repositories and contributors is challenging. Manual enforcement leads to inconsistent results and slows code reviews.

## Effective date

2025-03-01

## Purpose & Scope

### Objective

Ensure consistent code quality and style across all repositories through automated pre-commit validation

### Scope

- All new repositories
- Existing repositories during major updates
- All contribution types (code, documentation, configuration)

## Implementation framework

### Shared Configuration Repository

1. Create [HibiscusCollective/githooks](https://github.com/HibiscusCollective/githooks) repo containing:
   - Pre-commit hook templates
   - Linting configurations
   - Installation scripts

### Required Tooling

[Lefthook](git@github.com:evilmartians/lefthook) as per [ADR-0001](https://github.com/HibiscusCollective/adrs/blob/main/ADR-0001-git-hook-manager-selection.md)

```yaml
# Example .lefthook.yml
assert_lefthook_installed: true
remotes:
  - git_url: https://github.com/HibiscusCollective/githooks
    configs:
      # [Required] Configure the global workflow groups and steps
      - config/workflow.yml 
      # [Optional] Select code generation to apply
      - config/pre-commit/gen/rust.yml
      # [Optional] Select the linters to apply
      - config/pre-commit/lint/rust.yml
      - config/pre-commit/lint/typescript.yml
      # [Optional] More customization options...
```

### Enforcement Process

1. Repository maintainers must:
   - Install shared hooks during setup
   - Run validation in CI pipeline
2. Contributors receive immediate feedback via pre-commit checks
3. PRs must pass pre-commit checks

## Compliance Monitoring

- Weekly automated scan for lefthook configs org wide
- PR validation in CI/CD

## Reference Documents

- [**ADR-0001** Git hook manager selection](https://github.com/HibiscusCollective/adrs/blob/main/ADR-0001-git-hook-manager-selection.md)
