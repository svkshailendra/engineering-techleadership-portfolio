# Incident Response Playbook

This playbook reflects how I led production engineering practices for Azure-based systems, combining native telemetry with AppDynamics for deep observability.

---

## 🎯 Goals
- Reduce Mean Time to Recovery (MTTR) by combining proactive monitoring with actionable alerts.
- Provide clear visibility across backend, ML pipelines, and production workloads.
- Ensure structured communication and continuous learning after incidents.

---

## 🔍 Detection
- **Azure Application Insights** → Custom telemetry for expense categorization pipelines.  
- **Azure Monitor** → Alert routing with tuned thresholds to reduce false positives.  
- **AppDynamics** → Transaction tracing and performance baselines to detect anomalies in real time (e.g., slow queries, memory leaks).

---

## 🛠️ Response Roles
- **Incident Commander (rotating bi-weekly)** → Coordinates response, ensures updates every 20 minutes.  
- **Responder(s)** → Engineers with domain expertise (backend vs ML pipelines).  
- **Comms Lead** → Posts updates to Teams + customer status page.  
- **Scribe** → Captures timeline and actions for postmortem.

---

## 🚨 Mitigation
- Automated rollback scripts for Azure Functions reduced recovery time.  
- Feature flags used to disable non‑critical ML workflows during SEV‑1 incidents.  
- AppDynamics dashboards leveraged to pinpoint bottlenecks (e.g., Cosmos DB query latency) and validate fixes before rollout.

---

## 📊 Outcomes
- MTTR improved from 90 → 25 minutes by combining AppDynamics deep tracing with Azure alerts.  
- Ticket volume dropped 30% after proactive monitoring rollout over a period of 6 months.  
- Reduced false positives by 40% through AppDynamics baseline tuning.  
- Stakeholder trust improved with consistent comms cadence during outages.
