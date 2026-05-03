# ADR-001: Monitoring Strategy – Azure Application Insights + AppDynamics

## Context
Our Catalog Application supports telecom billing and Salesforce integration at enterprise scale.  
As usage grew, we faced challenges with:
- High ticket volume due to undetected performance issues.  
- Limited visibility into root causes across APIs, database calls, and Azure Kubernetes workloads.  
- False positives from noisy alerts, slowing incident response.  

We needed a monitoring solution that provided **deep observability**, reduced noise, and improved incident resolution times.

---

## Options Considered
1. **Azure Application Insights + Azure Monitor only**  
   - Native integration with Azure services.  
   - Strong telemetry for custom metrics and logs.  
   - Lower cost, but limited deep transaction tracing.

2. **AppDynamics only**  
   - Enterprise-grade APM with transaction tracing and performance baselines.  
   - Strong anomaly detection.  
   - Higher licensing cost, less seamless Azure integration.

3. **Hybrid Approach: Application Insights + AppDynamics**  
   - Application Insights for custom telemetry and Azure-native monitoring.  
   - AppDynamics for deep transaction tracing, anomaly detection, and performance baselines.  
   - Combined strengths, but requires integration effort.

---

## Decision
We chose **Hybrid Approach (Application Insights + AppDynamics)**.  
This allowed us to leverage Azure-native telemetry for cloud services while using AppDynamics for deep observability and anomaly detection.

---

## Consequences
- **Positive**  
  - Reduced ticket volume by ~15% through proactive monitoring.  
  - Improved MTTR from ~90 → ~25 minutes by combining AppDynamics tracing with Azure alerts.  
  - Reduced false positives by ~40% via AppDynamics baseline tuning.  
  - Increased stakeholder confidence with consistent incident response and validated fixes.

- **Negative**  
  - Higher operational cost due to dual tooling.  
  - Required additional integration and training for teams.  

---

## 🛠️ Implementation & Governance

To ensure this strategy remained a standard practice rather than an afterthought, I integrated observability into our Agile Lifecycle 

- **Automated Accountability**: Modified our Jira workflow to include a mandatory "Observability & Monitoring" sub-task for every feature User Story.

- **Definition of Done (DoD)**: A feature is not considered "Shipped" until
  - Custom Telemetry is implemented in App Insights for business-critical events.
  - Health Rule Baselines are configured in AppDynamics to catch performance regressions.
- **Result**: This eliminated "Monitoring Debt" and ensured that 100% of new features were observable on Day 1.

## Status
Accepted – Implemented across application's Web APIs, SQL Server calls, and Azure Kubernetes workloads.
