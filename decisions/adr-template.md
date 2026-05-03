# Architecture Decision Record (ADR)

## Title
Use GraphQL for API Layer

## Status
Proposed / Accepted / Deprecated

## Context
We need a flexible API layer to support multiple clients (web, mobile, partner integrations).  
REST APIs are currently in use but require multiple endpoints and versioning complexity.

## Decision
Adopt GraphQL as the primary API layer for new services.  
Existing REST endpoints will remain for legacy clients.

## Consequences
- ✅ Simplifies client queries (fetch only needed data)  
- ✅ Reduces number of endpoints to maintain  
- ❌ Requires new tooling and developer training  
- ❌ Potential performance overhead if queries are not optimized  

## Alternatives Considered
- Continue with REST  
- Use gRPC for internal services only