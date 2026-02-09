# CLAP Manifest
_Context Log Agent Protocol_

CLAP is an internal engineering protocol for building software **with heavy AI assistance** while keeping the work **auditable, reproducible, and safe to evolve**.

CLAP is **not** part of the product runtime.
It exists to structure *how we work* during development: context management, decision logging, artifact ownership, and a strict separation between thinking and execution.

---

## Why CLAP exists

AI accelerates development, but it also increases risk:

- context loss (wrong assumptions, forgotten constraints)
- non-reproducible outcomes (“it worked once in chat”)
- unclear ownership of AI-generated artifacts
- architecture drifting without recorded decisions
- prompt/model changes silently changing outputs over time

CLAP addresses this by turning AI collaboration into a **disciplined workflow** with durable artifacts.

---

## Scope

CLAP governs:

- how we capture and update **context**
- how we generate and store **artifacts** (docs, diagrams, code skeletons, ADRs)
- how we make and record **decisions**
- how we track **tasks** and execution status
- how AI-assisted work is reviewed and merged

CLAP does **not** govern:

- production runtime behavior
- user-facing features
- infrastructure operations (unless explicitly recorded as ADRs / runbooks)

---

## Core principles

1. **Explicit context management**
   - no “implicit chat memory” as source of truth
   - context must be written down as artifacts

2. **Durable decisions**
   - architectural/product decisions require ADRs
   - trade-offs must be visible later

3. **Separation: thinking vs execution**
   - “reasoning” is not an artifact
   - artifacts must be actionable, testable, and reviewable

4. **Clear ownership**
   - every artifact has an owner (human), a status, and a last-updated date

5. **Auditability**
   - a newcomer should be able to reconstruct *why* the system looks like it does
   - prompts/models may change; artifacts remain

---

## CLAP artifacts

CLAP stores development knowledge as versioned files (Markdown-first).

Minimum set:

- **Context**
  - project constraints, goals, non-goals, domain boundaries
- **Logs**
  - short, dated session logs: what changed, why, what’s next
- **ADRs**
  - architecture decisions with options and trade-offs
- **PRDs**
  - product requirements and scope definitions
- **TRDs**
  - technical requirements and implementation constraints
- **Tasks**
  - executable work units (small enough to complete & review)
- **Diagrams**
  - C4, sequence flows, event storming snapshots, ERD/logical model (as needed)
- **Templates**
  - reusable skeletons for ADRs, tasks, sessions, diagrams

Recommended meta for each artifact (front-matter or header block):

- `Owner`
- `Status` (draft / active / deprecated)
- `Last updated`
- `Related` (links to ADRs/tasks/issues/PRs)

---

## Lifecycle

CLAP work typically follows this loop, split into two phases:

### (CLP) Decision/Planning

1. **Context refresh**
   - confirm scope, constraints, current architecture state
2. **Decision capture**
   - if we’re choosing a direction → write/update an ADR
3. **Task breakdown**
   - split into small, reviewable tasks
4. **Artifact generation**
   - create docs/diagrams/skeletons needed to implement safely

### (ATP) Plan execution and reporting

1. **Implementation**
   - code changes reference tasks/ADRs
2. **Review**
   - validate outcomes vs context and ADR intent
3. **Log the session**
   - short summary + next steps

---

## Naming conventions (suggested)

Keep names predictable and sortable:

- `adr/ADR-XXXX-title.md`
- `logs/YYYY-MM-DD-session.md`
- `tasks/T-XXXX-title.md` (or `tasks/d0/T1-...` if using multi-day structure)
- `diagrams/{c4|flows|eventstorming}/...`
- `templates/...`

Use lowercase with hyphens for file names where possible.

---

## Review checklist (AI-assisted work)

Before merging changes produced with AI support, ensure:

- [ ] Context is updated (if assumptions changed)
- [ ] ADR exists/updated (if architecture changed)
- [ ] Tasks reference the implementation (PR links, commits, or issue ids)
- [ ] Artifacts are reproducible (commands, inputs, steps documented)
- [ ] No sensitive data is committed (PII, keys, transcripts, credentials)
- [ ] Generated code is human-reviewed (not “AI said it’s fine”)

---

## Relationship to the product

CLAP artifacts **live next to the code** to keep architecture and decisions close to implementation.

The product can evolve independently, but CLAP ensures:

- architectural intent stays readable
- AI collaboration remains structured
- onboarding and maintenance cost stays low

---

## Status of this manifest

This file is a living document.

If the team changes how it uses CLAP, update this manifest first,
then updat
