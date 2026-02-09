# Module Types

This document defines the **architectural types of modules** used in SaaS-Spine.

Module types describe the **role and responsibility** of a module in the system.
They do not affect directory structure — all modules share the same physical layout.

---

## 1. Core Domain Modules

Modules that implement the **core business value** of the SaaS.

### Characteristics
- contain the most important business rules
- represent key bounded contexts
- define the competitive advantage of the product
- highly stable and protected from change

### Dependency Rules
- may be depended on by other modules (via contracts)
- must not depend on infrastructure or frameworks

### Examples
- billing  
- subscriptions  
- orders  
- recruitment  

---

## 2. Supporting Modules

Modules that support the core domain but are **not themselves core business drivers**.

### Characteristics
- implement secondary or supporting processes
- easier to replace or refactor than core modules
- often orchestrate workflows around core domains

### Dependency Rules
- may depend on Core Domain modules (contracts only)
- must not contain core business logic

### Examples
- notifications  
- reporting  
- search  
- audit-log  

---

## 3. Generic Modules

Reusable modules with **low domain specificity**.

### Characteristics
- applicable across multiple SaaS products
- minimal business rules
- strong candidates for reuse or extraction

### Dependency Rules
- must not depend on Core Domain modules
- expose clean and minimal contracts

### Examples
- identity  
- access-control  
- file-storage  
- email  

---

## 4. Integration Modules

Modules responsible for **integrating external systems**.

### Characteristics
- isolate external APIs and vendors
- protect internal domains from upstream changes
- often implement Anti-Corruption Layers (ACL)

### Dependency Rules
- may depend on domain contracts
- must not expose external models directly

### Examples
- payments-stripe  
- crm-hubspot  
- auth-oauth  
- webhooks  

---

## 5. Infrastructure Modules

Technical modules implementing **infrastructure concerns**.

### Characteristics
- contain technical adapters and implementations
- no business or domain logic
- often configured per application

### Dependency Rules
- implement ports defined in other modules
- must not be depended on by Core Domain modules

### Examples
- persistence-postgres  
- queue-rabbitmq  
- cache-redis  
- logger  

---

## 6. Cross-Cutting Modules

Modules implementing **cross-cutting concerns** shared across the system.

### Characteristics
- apply common policies or mechanisms
- operate across multiple contexts
- do not own business logic

### Dependency Rules
- should avoid direct dependencies on Core Domain modules
- favor configuration and interception over logic

### Examples
- observability  
- metrics  
- security-policy  
- rate-limiting  

---

## 7. Experimental Modules

Temporary or experimental modules used for **research and exploration**.

### Characteristics
- unstable and subject to change
- used for proofs of concept or experiments
- not part of the stable system architecture

### Dependency Rules
- should not be depended on by stable modules
- must be clearly marked as experimental

### Examples
- ai-prototype  
- recommendation-poc  
- beta-feature-x  

---

## Notes

- Module type is an **architectural classification**, not a technical constraint.
- Each module type uses the same directory structure.
- Module type should be documented in:
  - `context-canvas.md`
  - module `README.md`
- Dependency rules may be enforced by `spine check`.

---

## Summary

SaaS-Spine module types exist to:
- clarify architectural intent
- enforce clean dependency direction
- support long-term evolution of the system

Module type defines **why a module exists**, not **how it is implemented**.
