# ADR-006: Service Bus Topology

## Status
Accepted

## Context
The Smart Notification Router publishes categorized alert messages to Azure Service Bus. Initially the system uses a simple **queue per category** approach to route messages to a single consuming team. As the product and number of consumers grow, we must decide whether to continue with queues or migrate to a **Topics + Subscriptions** topology.

Key constraints and requirements:
- **Per‑team routing**: multiple teams may need the same category feed or filtered subsets.
- **Simplicity**: low operational overhead for the current single‑team deployment.
- **Scalability**: ability to fan‑out messages to many consumers without duplicating producer logic.
- **Filtering**: consumers may want server‑side filtering (e.g., only high‑confidence items).
- **Reliability**: DLQ handling, message ordering (where required), and replayability.
- **Cost and management**: topics/subscriptions add configuration and monitoring overhead.

## Decision
Continue using **Queues** for the current single‑team deployment, and adopt a documented migration path to **Topics + Subscriptions** when multi‑team fan‑out or per‑team filtering requirements exceed the operational cost threshold.

## Alternatives Considered
1. **Keep Queues (current)**  
   - *Pros*: Simple to implement and reason about; minimal configuration; straightforward DLQ semantics.  
   - *Cons*: Producer must send duplicate messages if multiple teams need the same feed; limited server‑side filtering.

2. **Topics + Subscriptions (recommended for scale)**  
   - *Pros*: Native fan‑out; subscriptions support SQL filters and actions; single producer publish model; easier to add new consumers.  
   - *Cons*: More configuration; subscription management and monitoring overhead; potential for subscription drift and orphaned subscriptions.

3. **Hybrid approach**  
   - Use queues for single‑team or high‑throughput categories and topics for categories that require multi‑team distribution.  
   - *Pros*: Flexibility; incremental migration.  
   - *Cons*: Added architectural complexity; requires clear operational rules.

## Consequences
- **Short term**: Using queues keeps the system simple and reduces operational burden. Producers and current consumers remain unchanged.
- **When to migrate**: Migrate to topics when any of the following occur:
  - Two or more independent teams require the same category feed.
  - Multiple consumers require different server‑side filters on the same message stream.
  - Operational cost of duplicating messages from the producer becomes significant.
- **Operational changes on migration**:
  - Update producer to publish to a Topic instead of multiple Queues.
  - Create Subscriptions per consumer/team with appropriate SQL filters (e.g., `Category = 'Info' AND Confidence >= 80`).
  - Implement subscription lifecycle management (creation, deletion, monitoring).
  - Update monitoring and alerting to include subscription metrics and per‑subscription DLQ rates.
- **Testing and rollout**:
  - Deploy a pilot Topic with a small set of subscriptions.
  - Validate message delivery, filter correctness, and DLQ behavior.
  - Gradually switch consumers to subscriptions and decommission duplicated queues.

## Migration Checklist
1. **Design**: Define topic names, subscription naming conventions, and filter templates.
2. **Producer change**: Add Topic publish support while retaining queue publish for a fallback period.
3. **Create subscriptions**: Provision subscriptions for each consumer with filters and forward‑to rules if needed.
4. **Monitor**: Add telemetry for subscription message counts, delivery latency, and DLQ rates.
5. **Cutover**: Switch consumers to subscriptions; verify parity with previous queue behavior.
6. **Cleanup**: Remove redundant queue publishing and decommission unused queues.

## Notes
- Keep message schema stable and include **Category** and **Confidence** application properties to enable subscription filters.
- Use Azure Resource Manager templates or IaC to manage topics and subscriptions to avoid manual drift.
- Document subscription ownership and retention policies to prevent orphaned subscriptions.
