# Naming Conventions & Vocabulary

This document defines **canonical naming rules** for the SaaS Spine project.

Its purpose is to:

* establish a shared vocabulary for humans and AI agents,
* keep the architecture understandable after months or years,
* avoid semantic drift, bikeshedding, and framework‑driven naming,
* make generated code, docs, and ADRs consistent by default.

This file is **normative**. If something is named differently, it should be justified explicitly (ADR).

---

## 1. What SaaS Spine *Is* (and Is Not)

### Is

* A **code‑first structural foundation** for building SaaS products
* A **set of bounded contexts** with strong architectural boundaries
* A **long‑living backbone**, meant to survive pivots and rewrites
* A system designed for **human developers assisted by AI agents**

### Is NOT

* A full SaaS product
* A no‑code / low‑code builder
* A CRUD generator
* A UI framework
* A Laravel/Symfony/Rails replacement

Naming must always reflect this distinction.

---

## 2. Framework / Project Naming

### 2.1 Conceptual Meaning

The framework name must communicate:

* structural importance (foundation, backbone, spine, kernel)
* neutrality (not tied to a specific UI or business domain)
* longevity

Examples of acceptable root names:

* `SaaSBackbone`
* `SaaSSpine`
* `SaaSFoundation`
* `SaaSKernel`
* `ProductBackbone`

The final choice is **less important than internal consistency**.

---

### 2.2 Repository & Distribution Naming

Regardless of the final brand name, repositories should follow this pattern:

* `<root>-core` – backend core framework
* `<root>-console` – reference admin UI (optional)
* `<root>-sdk-js` – JavaScript / TypeScript SDK
* `<root>-adapters-*` – external integrations
* `<root>-skeleton-*` – starter templates

Example (using a placeholder root name `spine`):

* `spine-core`
* `spine-console`
* `spine-sdk-js`
* `spine-adapters-stripe`

This allows renaming the framework without breaking the mental model.

---

## 3. Module (Bounded Context) Naming

### 3.1 Core Principle

**Every module represents a bounded context.**

A module name must:

* describe a *business capability*, not a technical detail
* be stable over time
* be understandable without reading code

### 3.2 Canonical Core Modules

The following module names are considered canonical for SaaS Spine:

* **Identity** – authentication, credentials, sessions, MFA
* **Tenancy** – tenants/workspaces and membership
* **AccessControl** – roles, permissions, policies
* **Billing** – plans, subscriptions, payment lifecycle
* **Entitlements** – feature flags, quotas, limits
* **Audit** – audit log and compliance events
* **Notifications** – email / in‑app notifications
* **Jobs** – background processing, queues, schedulers
* **Integrations** – outbound/inbound integrations and webhooks
* **Observability** – logging, metrics, tracing, health checks
* **Admin** – backoffice capabilities (optional)
* **AgentRuntime** – AI tools, execution context, agent audit (optional)

Not all projects need all modules, but **names should not be reinvented**.

---

## 4. Namespaces & Code Structure (Backend)

### 4.1 Root Namespace

The root namespace equals the framework name:

```
SaaSSpine\...
```

(or equivalent if the final name changes)

---

### 4.2 Module Namespace Structure

Each module follows the same internal structure:

```
<Root>\<Module>\
  Domain\
  Application\
  Infrastructure\
```

Example:

```
SaaSSpine\Billing\Domain
SaaSSpine\Billing\Application
SaaSSpine\Billing\Infrastructure
```

This structure is preferred over generic layers like `Controllers`, `Services`, or `Utils`.

---

## 5. Adapter & Integration Naming

External systems must never leak directly into the domain.

### 5.1 Adapter Naming Rules

Adapters must:

* explicitly name the external system
* express their role clearly

Accepted suffixes:

* `Adapter`
* `Gateway`
* `Acl` (Anti‑Corruption Layer)

Examples:

* `StripeBillingAdapter`
* `PostmarkMailerAdapter`
* `SlackIntegrationAdapter`
* `StripeAcl`

Avoid vague names like `StripeService` or `ExternalClient`.

---

## 6. Frontend & SDK Naming

### 6.1 SDK

SDKs must be:

* headless
* framework‑agnostic
* named consistently

Example:

* `@spine/sdk-js`

The SDK exposes **capabilities**, not UI components.

---

### 6.2 Reference UI

The reference UI is named as a **console**, not a product:

* `<root>-console`

It exists to demonstrate integration and provide a usable baseline.

---

## 7. Naming Anti‑Patterns (Explicitly Forbidden)

The following names should never appear:

* `Utils`
* `Helpers`
* `Common`
* `Core2`
* `NewAuth`
* `AuthV2`
* `SharedStuff`

If a name feels generic, it is probably wrong.

---

## 8. AI Agent Guidelines

AI agents working on this project must:

* reuse existing module names
* avoid inventing new vocabulary
* treat module names as **bounded contexts**, not folders
* follow the namespace and adapter conventions exactly

If an agent cannot map a concept to an existing module, it should:

1. propose a new bounded context explicitly
2. justify it in natural language
3. wait for confirmation

---

## 9. Summary

* Names encode architectural intent
* Stability is more important than creativity
* Consistency beats cleverness
* If naming is unclear, architecture is unclear

This document is designed to be used as **training material and guardrails for AI agents** generating code, documentation, and architectural decisions.
