# ADR-001: Choosing Cosmos DB over SQL Server

## Status
Accepted – April 2026

---

## Context
The Categoriser tool requires a scalable, globally available database to store expense records.  
Key requirements:
- Multi‑tenant support (partitioning by userId)
- Low latency reads/writes for Blazor WebAssembly clients
- Flexible schema for evolving categorization logic
- Integration with Azure Functions

Two options were considered:
1. **Azure SQL Database**
   - Strong relational model
   - Mature ecosystem, transactional guarantees
   - Well‑known to most engineers
2. **Azure Cosmos DB**
   - Globally distributed, multi‑region replication
   - Schema‑less, supports JSON documents
   - Native SDK integration with Azure Functions
   - Partitioning and scaling built‑in

---

## Decision
We chose **Cosmos DB** as the primary data store for expense records.  
Partitioning is done by `userId` to ensure scalability and isolation.  
SQL Server was ruled out due to schema rigidity and higher operational overhead for multi‑region scaling.

---

## Consequences
### Positive
- Seamless integration with Azure Functions
- Flexible schema supports evolving ML.NET categorization
- Built‑in partitioning and scaling
- Global distribution supports future expansion

### Negative
- Higher cost compared to SQL Server for small workloads
     -  Mitigation: We implemented Autoscale throughput (RU/s) to align costs with actual usage peaks.
- Requires careful partition key design
     -  Mitigation: Established a Partitioning Strategy document and performed load testing on the userId key to validate performance at 10x projected volume.

---

## Alternatives Considered
- **Azure SQL Database**: Strong relational guarantees, but scaling and schema evolution would be harder.
- **Table Storage**: Cheaper, but lacks rich querying and SDK support.
- **PostgreSQL on Azure**: Flexible, but less native integration with Functions and Blazor.

---

## References
- Microsoft Docs: [Cosmos DB vs SQL Database](https://learn.microsoft.com/en-us/azure/cosmos-db/introduction)  

