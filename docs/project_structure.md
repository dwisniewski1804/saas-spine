# Project Structure

```txt
saas-spine/
├── runtime/
├── modules/
├── adapters/
├── apps/
├── clap/
├── docs/
├── docker-compose.yml
├── Makefile
└── README.md
```

## runtime/

Framework-agnostic core runtime of SaaS-Spine.

Responsible for:

- loading application manifests
- discovering and loading modules
- enforcing architectural rules
- managing module lifecycle
- providing CLI tooling

Contains no domain logic and no framework dependencies.

## modules/

Domain modules representing bounded contexts or subdomains.

Each module is:

- self-contained
- framework-independent
- documented with a Context Canvas
- exposing only explicit contracts

Modules contain domain logic and define clear architectural boundaries.

## adapters/

Integration layers between SaaS-Spine and external frameworks or runtimes.

Adapters:

- map Spine concepts to framework mechanisms
- handle container, routing, and lifecycle bridging
- contain no domain logic

Examples: Laravel adapter, PSR-15 adapter, RoadRunner adapter.

## apps/

Executable applications built on top of SaaS-Spine.

Each application:

- selects modules via a manifest
- chooses adapters
- defines infrastructure and runtime configuration
- is runnable via Docker

Apps are concrete products or reference implementations.

## clap/

Architectural process artifacts.

Contains:

- vision documents
- architectural decision records (ADRs)
- logs and context evolution notes

Used as first-class input for humans and AI agents.

## docs/

Conceptual and architectural documentation.

Includes:

- design principles
- architectural explanations
- onboarding and guidelines

Documents explain intent and structure, not implementation details.

## docker-compose.yml

Default Docker Compose configuration.

Provides a one-command way to run demo or reference applications
together with required infrastructure (e.g. databases).

## Makefile

Developer convenience commands.

Defines shortcuts for common workflows such as:

- starting the project
- running checks
- managing containers

## README.md

Repository entry point.
