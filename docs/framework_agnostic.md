
The inverse is **never allowed**.

Specifically:
- `runtime/` must not depend on Laravel, Symfony, or any framework
- `modules/` must not reference framework classes
- Only `adapters/` are allowed to depend on frameworks

This rule is non-negotiable.

---

## Core vs Adapters

### SaaS-Spine Core

The core consists of:
- Runtime lifecycle (bootstrapping, module loading)
- Module contracts
- Manifest loading
- Validation rules (e.g. required Context Canvas)
- CLI tooling

The core communicates exclusively via:
- Explicit contracts
- Plain PHP
- PSR standards (where applicable)

No framework assumptions are allowed here.

---

### Adapters

Adapters are thin integration layers that map SaaS-Spine concepts onto a specific framework.

Examples:
- Laravel adapter
- Symfony adapter
- PSR-15 HTTP adapter
- RoadRunner adapter

An adapter is responsible for:
- Wiring containers
- Mapping lifecycle hooks
- Bridging routing / events / services
- Translating framework concepts into Spine contracts

Adapters contain **no domain logic**.

---

## Why Provide a Laravel Adapter?

Laravel is widely adopted and provides:
- Fast onboarding
- Excellent DX
- A familiar environment for many developers

Providing a Laravel adapter serves two purposes:
1. A **reference implementation** of the adapter pattern
2. A **ready-to-run demo application** for quick evaluation

However:

> Laravel is an example, not a dependency.

The presence of a Laravel adapter does not define SaaS-Spine’s architecture.

---

## Module Design and Framework Independence

Each module in SaaS-Spine:
- Represents a bounded context or subdomain
- Owns its domain logic
- Publishes only explicit contracts
- Contains required architectural documentation

Mandatory artifacts per module:
- `context-canvas.md`
- `boundaries.md`
- `contracts/`
- `src/`

Modules must not:
- Import framework classes
- Use framework-specific helpers or facades
- Rely on implicit global state

This guarantees that modules remain portable and testable in isolation.

---

## Runtime Without a Framework

SaaS-Spine runtime does not assume:
- A specific HTTP server
- A specific container implementation
- A specific event system

Instead, it defines:
- A minimal module lifecycle
- A manifest-driven composition model
- Explicit integration points

This allows the same runtime to be used with:
- Laravel
- Symfony
- Slim
- Custom PSR-15 servers
- CLI-only applications

---

## Benefits of a Framework-Agnostic Spine

- Long-term architectural stability
- Freedom of framework choice
- Easier refactoring and evolution
- Better alignment with Domain-Driven Design
- Cleaner boundaries for AI agents and automation
- Reduced vendor lock-in

Most importantly:

> The architecture survives framework trends.

---

## Non-Goals

SaaS-Spine explicitly does NOT aim to:
- Replace application frameworks
- Compete with Laravel or Symfony
- Provide UI, auth, billing, or infrastructure out of the box

Those concerns belong to applications and adapters.

---

## Summary

SaaS-Spine treats frameworks as **delivery mechanisms**, not as architecture.

By enforcing strict dependency direction and contract-based integration,
it enables teams to build SaaS products that are:
- modular
- evolvable
- portable
- and resilient to framework churn

Frameworks come and go.
Architecture should not.
