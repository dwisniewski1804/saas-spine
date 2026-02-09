# Module Structure

```txt
modules/<module-name>/
├── context-canvas.md
├── boundaries.md
├── contracts/
├── src/
├── tests/
└── README.md
```

## modules/{module-name}/

Root directory of a single SaaS-Spine module.

A module represents a bounded context or subdomain.
It is the smallest independently understandable and loadable unit in the system.

## context-canvas.md

Mandatory Context Canvas for the module.

Describes:

- purpose of the bounded context
- core domain concepts
- business rules and policies
- inbound and outbound interactions
- ubiquitous language

Used as a primary architectural reference for humans and AI agents.

## boundaries.md

Explicit definition of module boundaries.

Explains:

- what the module owns
- what it is responsible for
- what is explicitly out of scope
- allowed and forbidden dependencies

This file exists to prevent accidental coupling.

## contracts/

Public API of the module.

Contains:

- interfaces (ports)
- DTOs
- commands
- events

Other modules and applications may depend only on this directory.
No implementation details should be exposed here.

## src/

Internal implementation of the module.

Contains:

- domain logic
- application services
- internal adapters

Code in this directory must not be imported directly by other modules.

## tests/

Module-level tests.

Includes:

- unit tests for domain logic
- contract tests (if applicable)

Tests should not depend on external frameworks or infrastructure.

## README.md

Module-level overview.
