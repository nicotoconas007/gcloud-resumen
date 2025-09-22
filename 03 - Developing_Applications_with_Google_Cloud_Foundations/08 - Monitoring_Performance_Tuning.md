## Módulo 8 – Monitoring and Performance Tuning

### Resumen
Google Cloud Observability integra métricas, logs y metadata en una vista unificada para entender y diagnosticar aplicaciones en Google Cloud, AWS, on‑premises e híbridos. Es la base de la confiabilidad: permite detectar problemas y actuar rápido.

### Servicios principales
#### Cloud Monitoring
- Dashboards personalizados y out‑of‑the‑box; métricas, eventos y alertas.
- Golden Signals a monitorear: Latency, Traffic, Errors, Saturation.

#### Cloud Logging
- Ingesta y gestión de logs de plataformas y apps; Logs Explorer para búsqueda/filtrado.
- Log Analytics: consultas SQL sobre logs; crear log‑based alerts y log‑based metrics.
- Recomendación: usar structured logs (JSON) para mejor análisis.
- Ops Agent: recolecta logs/métricas en Compute Engine y apps de terceros (NGINX, Tomcat, Apache).

#### Error Reporting
- Cuenta, agrupa y deduplica errores con stack traces; notificaciones y dashboard.
- Integración automática en Cloud Run y Cloud Functions; soporta varios lenguajes.

#### Cloud Trace
- Tracing distribuido para analizar latencias entre servicios y requests.
- Conceptos: traces (operación) y spans (suboperación); Trace Explorer para análisis gráfico.
- Integración con OpenTelemetry y bibliotecas cliente.

#### Cloud Profiler
- Perfilador estadístico de bajo overhead (CPU/memoria) en producción; atribuye consumo al código fuente.

#### Prometheus y Managed Service for Prometheus
- Prometheus: métricas y alertas (PromQL) popular en Kubernetes.
- Servicio administrado en GCP compatible con Grafana y Cloud Monitoring.

### Mejores prácticas
- Dashboards con los 4 Golden Signals y alertas proactivas (no solo post‑mortem).
- Structured logs JSON; métricas basadas en logs para tendencias/umbrales.
- Usar Error Reporting para deduplicación y trazabilidad de fallos.
- Combinar Trace + Profiler para latencias y hotspots de CPU/memoria.
- Usar Managed Prometheus para cargas en Kubernetes.

### Ejemplos rápidos
- Monitoring: dashboard de latencia con alerta >200 ms.
- Logging: crear log‑based metric “HTTP 500 occurrences/minute”.
- Error Reporting: reportar errores con librería oficial (p.ej. Node.js).
- Trace: instrumentar con OpenTelemetry y visualizar spans.
- Profiler: habilitar en prod y detectar funciones de alto consumo.

Referencia: [Module 8 – Monitoring and performance tuning](https://storage.googleapis.com/cloud-training/devapps-foundations/en/on-demand/v1.2.0/Module8-MonitoringAndPerformanceTuning.pdf)
Docs: [Cloud Logging](https://cloud.google.com/logging/docs/overview), [Cloud Trace](https://cloud.google.com/trace/docs/overview), [Cloud Profiler](https://cloud.google.com/profiler/docs/about-profiler), [Ops Agent](https://cloud.google.com/stackdriver/docs/solutions/agents/ops-agent)

### Quiz (oficial)
1) Users are encountering errors in your application. You want to view the stack trace to determine where the error occurred. Which service helps?
   - A) Error Reporting
   - B) Cloud Logging
   - C) Cloud Trace
   - D) Cloud Monitoring
   - Respuesta: A) Error Reporting

2) You want to set up monitoring for a mission‑critical application. What signals should you monitor?
   - A) Contrast, Latency, Traffic, Errors
   - B) Security, Latency, Throttling, Errors
   - C) Saturation, Latency, Traffic, Errors
   - D) Saturation, Latency, Throttling, Errors
   - Respuesta: C) Saturation, Latency, Traffic, Errors

3) You want to stream logs into Cloud Logging from third‑party apps on Compute Engine. What should you use?
   - A) Cloud Monitoring
   - B) Ops Agent
   - C) Error Reporting
   - D) Cloud Trace
   - Respuesta: B) Ops Agent

### Preguntas extra (práctica estilo certificación)
4) Which service provides dashboards, metrics, and alerting to monitor app health?
   - A) Cloud Monitoring
   - B) Cloud Logging
   - C) Error Reporting
   - D) Cloud Trace
   - Respuesta: A) Cloud Monitoring

5) Which service helps deduplicate similar errors and shows stack traces?
   - A) Error Reporting
   - B) Cloud Logging
   - C) Cloud Monitoring
   - D) Cloud Trace
   - Respuesta: A) Error Reporting

6) You need to analyze latency between microservices. Which service do you use?
   - A) Cloud Trace
   - B) Cloud Monitoring
   - C) Cloud Logging
   - D) Cloud Profiler
   - Respuesta: A) Cloud Trace

7) Which tool provides low‑overhead continuous profiling of CPU/memory in production?
   - A) Cloud Profiler
   - B) Cloud Trace
   - C) Cloud Monitoring
   - D) Cloud Logging
   - Respuesta: A) Cloud Profiler

8) Which observability tool is recommended to monitor Kubernetes workloads with PromQL?
   - A) Prometheus
   - B) Cloud Monitoring
   - C) Cloud Logging
   - D) Grafana
   - Respuesta: A) Prometheus

9) Which type of logs are recommended for efficient querying and analysis?
   - A) Structured logs (JSON)
   - B) Plain text logs
   - C) CSV logs only
   - D) Syslog only
   - Respuesta: A) Structured logs (JSON)

10) Which four key metrics (Golden Signals) are essential for app monitoring?
   - A) Latency, Traffic, Errors, Saturation
   - B) CPU, Memory, Disk, Network
   - C) Throughput, Uptime, Cost, Requests
   - D) Security Incidents, Throttling, Retries, Timeouts
   - Respuesta: A) Latency, Traffic, Errors, Saturation