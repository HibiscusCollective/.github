# **ADR-0001** Git hook manager selection

**Authors**: Pierre Fouilloux

![Accepted](https://img.shields.io/badge/status-accepted-brightgreen)
![2025-02-16](https://img.shields.io/badge/Date-16_Feb_2025-lightblue)
![Approval Model](https://img.shields.io/badge/approved_by-project_lead-red)

## Context and Problem Statement

We need a git hook management solution that:

* Ensures consistent hook execution across developer environments
* Supports polyglot tech stack (Node.js, Python, Go)
* Allows centralized hook configuration
* Provides parallel execution for performance
* Enables easy maintenance/updates

## Decision Drivers

* Cross-platform support (Linux/macOS/Windows)
* Performance for large monorepo operations
* Configuration-as-code approach
* Language/framework agnostic
* Team adoption complexity

## Considered Options

* pre-commit (Python-centric)
* Lefthook (Go-based, polyglot)
* Husky (Node.js focused)

## Decision Outcome

Chosen option: "Lefthook", because:

* 3-5x faster than alternatives through parallel execution
* Single binary installation
* Supports multiple languages via Docker/native
* YAML configuration with inheritance
* Remote config support for centralized management

### Consequences

* Good, because unified hook management across all projects
* Good, because native monorepo support with directory filters
* Neutral, because requires Go runtime for advanced customization
* Neutral, because new tool learning curve

### Confirmation

* All repos contain `.lefthook.yml` by March 2025
* Pre-commit hook execution time <2s
* 100% hook configuration in version control

## Pros and Cons

### pre-commit

* Good, because strong Python ecosystem
* Bad, because limited to Python/node environments
* Bad, because sequential execution

### Lefthook

* Good, because parallel task execution
* Good, because remote config inheritance
* Good, because language-agnostic
* Bad, because less known than alternatives

### Husky

* Good, because simple JS integration
* Bad, because Node.js dependency and large node_modules dependency tree
* Bad, because no built-in parallelization
