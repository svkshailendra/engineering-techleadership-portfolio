# ADR-004: Tech Stack Evaluation – Blazor WASM vs. React

## Status
Accepted – April 2025

---

## Context
For the Categoriser tool, we needed a frontend framework that:
- Integrates seamlessly with .NET backend services (Azure Functions, ML.NET).
- Provides strong developer productivity and maintainability.
- Supports modern SPA (Single Page Application) patterns.
- Can be deployed easily to Azure Static Web Apps.

Two primary options were considered:
1. **React**
   - Industry standard, large ecosystem.
   - Rich library support and community.
   - Requires JavaScript/TypeScript expertise.
2. **Blazor WebAssembly**
   - Native .NET integration.
   - Enables full‑stack C# (frontend + backend).
   - Strong alignment with Azure hosting and tooling.

---

## Decision
We chose **Blazor WebAssembly** as the frontend framework.  
This allows a unified C# stack across frontend and backend, reducing context switching and improving maintainability.  
React was ruled out due to additional skill requirements and weaker integration with .NET/Azure services.

---

## Consequences
### Positive
- Single language (C#) across frontend and backend.
- Seamless integration with Azure Functions and Application Insights.
- Easier onboarding for .NET developers.
- Strong alignment with existing portfolio projects.

### Negative
- Smaller ecosystem compared to React.
- Fewer third‑party UI libraries.
- Performance overhead for large WASM payloads.

---

## Alternatives Considered
- **React**: Rich ecosystem, but adds complexity with dual language stack.
- **Angular**: Strong enterprise support, but steep learning curve and less synergy with .NET.
- **Vue.js**: Lightweight, but limited enterprise adoption compared to React/Angular.

---

## References
- Microsoft Docs: [Blazor WebAssembly Overview](https://learn.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-8.0)  

