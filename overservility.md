what is overservility is process of monitoring logging and tracing your application so that tell that what is going  on application and why is that thing happening why did that happen.
Metrics: Prometheus. It stores metrics in a TSDB (Time Series Database), meaning data is saved along with time (for example, CPU usage every 15 seconds).
Logs: Loki. This is Grafana’s log system, which stores and searches logs.
Traces: OpenTelemetry (you wrote “open telimatic”). It is a standard that collects traces, metrics and logs from your application. To store traces, Tempo or Jaeger is usually used.
Grafana: this is the dashboard / visualization layer for everything. You can connect Prometheus, Loki and Tempo to it and see graphs and logs in one place.

The flow looks like this:

Application → OpenTelemetry (collects)
                 ├── Metrics → Prometheus (TSDB)
                 ├── Logs    → Loki
                 └── Traces  → Tempo / Jaeger
                          ↓
                       Grafana (everything on one screen)
