# ADR-007: In‑Memory Processing and Session Scope

## Status
Accepted

## Context
Smart Notification Router currently processes uploaded batches **in memory only**. Session state is scoped to the browser tab: a session (and its dashboard results) lives only while that tab remains open. This design was chosen to prioritize user privacy, simplicity, and a low operational footprint for the public/free demo.

Key constraints and requirements:
- **Privacy**: avoid storing potentially sensitive email content by default.  
- **Simplicity**: minimal infra and operational overhead for a demo/free tier.  
- **User experience**: session persistence within a tab so users can navigate without losing the current batch.  
- **Recoverability & auditability**: limited because data is not persisted.  
- **Extensibility**: potential future need for replay, analytics, or enterprise audit trails.

## Decision
Keep the **in‑memory, tab‑scoped session model** as the default and canonical behavior for the public/demo deployment. Sessions remain active only while the browser tab is open; closing the tab ends the session and clears the in‑memory batch. Do **not** enable automatic persistence by default.

## Alternatives Considered
1. **Always Persisted**  
   - *Pros*: full audit trail, replayability, easier debugging and analytics.  
   - *Cons*: storage cost, compliance burden, increased attack surface for sensitive data.

2. **Configurable Opt‑in Persistence** (not chosen now)  
   - *Pros*: preserves privacy by default while allowing enterprise deployments to enable persistence.  
   - *Cons*: additional implementation and documentation effort; risk of accidental data retention if misconfigured.

3. **Hybrid (in‑memory default + optional persistence)**  
   - *Pros*: flexible; balances privacy and enterprise needs.  
   - *Cons*: introduces complexity; requires clear UX and governance to avoid accidental storage.

## Rationale
- The primary product goal for the public/demo instance is **privacy and low friction**. In‑memory, tab‑scoped sessions meet that goal while providing a usable UX (results persist while the user works in the same tab).  
- Persisting data by default would change the privacy posture and increase operational responsibilities; that tradeoff is not acceptable for the public demo.  
- If enterprise customers require persistence, we will evaluate an opt‑in, well‑governed persistence feature as a separate, documented capability (see Implementation Notes).

## Consequences
- **User experience**: Dashboard state persists while the tab is open; opening the same app in a new tab creates a new, empty session.  
- **No audit trail**: There is no built‑in ability to replay or inspect past batches after the tab is closed.  
- **Limited analytics**: Historical metrics and model retraining datasets cannot be derived from persisted user batches in the public deployment.  
- **Operational simplicity**: Lower cost and fewer compliance obligations for the public instance.

## Implementation Notes
- **Session management**: Keep session identifiers in memory (or in a short‑lived browser storage mechanism scoped to the tab, e.g., `sessionStorage`) and avoid writing batch contents to any server‑side persistent store.  
- **Explicit enterprise path**: If persistence is later required, implement it behind a clearly documented feature flag or separate deployment profile (enterprise/self‑hosted). Persisted mode must include:
  - **Encryption at rest**, secure key management, and RBAC.  
  - **Retention policies** (configurable TTL) and automated cleanup.  
  - **Data minimization**: persist only necessary fields unless full content is explicitly required and consented.  
  - **Privacy notice** and admin consent UI when enabling persistence.  
- **Telemetry**: Emit minimal telemetry for public instances (e.g., anonymized counts) without persisting raw content. For enterprise deployments, add telemetry only after consent and with appropriate controls.
- **Documentation**: Update README and architecture docs to clearly state the default in‑memory behavior and the lifecycle of a session (tab open → session active; tab close → session ends).

## Migration / Future Work
- If customer demand or product requirements justify persistence, implement an opt‑in persisted mode as a separate feature with a migration plan and compliance checklist.  
- Provide admin tools for replay and controlled export in enterprise mode only.  
- Add a short smoke test that verifies session isolation across tabs and that closing a tab clears in‑memory state.

## Notes
- For the public demo, treat the in‑memory, tab‑scoped model as a privacy feature and a deliberate product decision rather than a temporary limitation.
