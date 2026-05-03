# ADR-003: Team Structure Options – Centralized vs. Cross-Functional

## Status
Proposed – May 2025

---

## Context
As engineering organizations scale, structuring teams becomes critical for delivery speed, ownership, and collaboration.  
Two common models were considered for the Categoriser project and supporting repos:

1. **Centralized Functional Teams**
   - Engineers grouped by discipline (frontend, backend, QA, DevOps).
   - Work flows across teams in sequence.
   - Easier to build deep expertise in each function.

2. **Cross-Functional Squads**
   - Teams include all skills needed to deliver end-to-end features.
   - Each squad owns a vertical slice of functionality.
   - Encourages autonomy and faster iteration.

---

## Decision
We propose **cross-functional squads** for portfolio projects.  
Each squad includes frontend (Blazor), backend (Azure Functions), data (Cosmos DB/ML.NET), and QA.  
This aligns with modern product delivery practices and reduces handoff delays.

---

## Consequences
### Positive
- Faster delivery with fewer dependencies.
- Clear ownership of features and outcomes.
- Stronger collaboration across disciplines.
- Easier alignment with product goals.

### Negative
- Requires broader skill sets within squads.
- Risk of duplicated effort across teams.
- Harder to maintain deep specialization.

---

## Alternatives Considered
- **Centralized Functional Teams**: Easier to manage expertise, but slower delivery due to handoffs.
- **Hybrid Model**: Centralized QA/DevOps with cross-functional feature squads. Could balance specialization with autonomy.

---

