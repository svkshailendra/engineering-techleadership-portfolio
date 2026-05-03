# DORA Metrics Overview

## 🎯 Purpose
DORA (DevOps Research and Assessment) metrics are industry‑standard measures of software delivery performance.  
They help engineering leaders understand **speed, stability, and quality** in delivery pipelines.

---

## 📑 The Four Key Metrics

### 1. Deployment Frequency
- **Definition**: How often code is deployed to production.
- **Goal**: High frequency indicates fast iteration and responsiveness.
- **Example Targets**:
  - Elite performers: On‑demand (multiple per day)
  - Medium performers: Weekly to monthly

---

### 2. Lead Time for Changes
- **Definition**: Time from code commit to running in production.
- **Goal**: Short lead times show efficient pipelines and reduced bottlenecks.
- **Example Targets**:
  - Elite performers: < 1 day
  - Medium performers: 1 week – 1 month

---

### 3. Change Failure Rate
- **Definition**: Percentage of deployments causing failures (bugs, outages, rollbacks).
- **Goal**: Low failure rates indicate quality and stability.
- **Example Targets**:
  - Elite performers: 0–15%
  - Medium performers: 16–30%

---

### 4. Mean Time to Restore (MTTR)
- **Definition**: Time to recover from a failure in production.
- **Goal**: Fast recovery minimizes business impact.
- **Example Targets**:
  - Elite performers: < 1 hour
  - Medium performers: < 1 day

---

## ✅ Best Practices
- **Automate pipelines**: CI/CD reduces lead time and failure rates.
- **Monitor continuously**: Use Application Insights, Log Analytics, or Grafana dashboards.
- **Track trends, not absolutes**: Improvement over time matters more than hitting a static target.
- **Balance speed and stability**: Optimize for both, not one at the expense of the other.

---

## 🚀 Example Dashboard Concept
| Metric                | Current Value | Target | Trend |
|------------------------|---------------|--------|-------|
| Deployment Frequency   | 3 per week    | Daily  | ↑ Improving |
| Lead Time for Changes  | 2 days        | < 1 day| → Stable |
| Change Failure Rate    | 12%           | < 15%  | ↓ Improving |
| MTTR                   | 3 hours       | < 1 hr | ↑ Improving |

---

## 📌 References
- Google Cloud DORA Research: [https://cloud.google.com/devops](https://cloud.google.com/devops)  
