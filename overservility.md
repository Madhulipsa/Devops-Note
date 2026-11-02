 Observability
 
## What is Observability?
 
Observability is the process of monitoring **logs, metrics and traces** of your application so that it tells you:
 
- **What** is going on inside the application
- **Why** it is happening
- **Why** it happened
> Monitoring tells you that **something is wrong**. Observability tells you **what is wrong and why**.
 
---
 
## The 3 Pillars
 
| Pillar | Tool | What it does |
|--------|------|--------------|
| **Metrics** | Prometheus | Stores metrics in a **TSDB** (Time Series Database). Data is saved along with time, for example CPU usage every 15 seconds. |
| **Logs** | Loki | Grafana's log system, which stores and searches logs. |
| **Traces** | OpenTelemetry | A standard that collects traces, metrics and logs from your application. Traces are usually stored in **Tempo** or **Jaeger**. |
| **Dashboard** | Grafana | The dashboard / visualization layer. Connect Prometheus, Loki and Tempo to see graphs, logs and traces in one place. |
 
---
 
## Flow
 
```text
Application → OpenTelemetry (collects)
                 ├── Metrics → Prometheus (TSDB)
                 ├── Logs    → Loki
                 └── Traces  → Tempo / Jaeger
                          ↓
                       Grafana (everything on one screen)
```
 
---
 
## LGTM Stack
 
The Grafana ecosystem is often called the **LGTM stack**:
 
- **L**oki: logs
- **G**rafana: dashboards
- **T**empo: traces
- **M**imir: scalable Prometheus (metrics)
---
 
## Example
 
If a website becomes slow:
 
1. **Metrics** show that it is slow.
2. **Traces** show which service is slow.
3. **Logs** show what error occurred in that service.
 
