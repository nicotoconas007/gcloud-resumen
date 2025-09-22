## Hoja de Repaso Rápido – Índice (Módulos 01–08)

### Índice (click para abrir cada módulo)
- [01 – Best Practices for Cloud App Dev](01 - Best_Practices_Gcloud.md)
- [02 – Getting Started with Google Cloud Dev](02 - Getting_Started_Cloud.md)
- [03 – Data Storage Options](03 - Data_Storage_Options.md)
- [04 – Handling Authentication and Authorization](04 - Handling_Authr_And_Authz.md)
- [05 – Adding Intelligence to Your Application](05 - Adding_Intelligence_Application.md)
- [06 – Deploying Applications](06 - Deploying_Applicattions.md)
- [07 – Compute Options for Your Applications](07 - Compute_Options_Applications.md)
- [08 – Monitoring and Performance Tuning](08 - Monitoring_Performance_Tuning.md)

---

### Cheatsheets esenciales

#### 1) Compute: ¿qué usar?
| Requisito | Servicio recomendado |
| --- | --- |
| Máximo control de SO/red/licencias | Compute Engine |
| Contenedores con control medio o híbrido/multi-cloud | GKE (Standard/Autopilot) |
| Serverless contenedores HTTP/gRPC, escala 0->N | Cloud Run |

Nota: Cloud Run no expone puertos TCP arbitrarios; usa HTTP/1.1, HTTP/2 y gRPC.

#### 2) Storage: elección rápida
| Caso | Servicio |
| --- | --- |
| Archivos/objetos grandes, sitios estáticos | Cloud Storage |
| NoSQL documentos + tiempo real/offline | Firestore |
| NoSQL KV/wide-column, billones de filas/IoT | Bigtable |
| Relacional administrado (OLTP) | Cloud SQL |
| Relacional global + consistencia fuerte | Spanner |
| DW serverless (OLAP, BI) | BigQuery |
| Caché en memoria (ms) | Memorystore |
| Postgres optimizado OLTP+analítico | AlloyDB |

#### 3) Autenticación y Autorización
- Workloads en GCE/Cloud Run/Functions: adjuntar Service Account; tokens via metadata server.
- GKE: Workload Identity. Multi-cloud/on-prem: Workload Identity Federation.
- Usuario final: OAuth 2.0 / Identity Platform. Apps internas: IAP delante de HTTPS.
- IAM: roles predefinidos/custom + Conditions; mínimo privilegio.
- Secret Manager para credenciales; auditoría en Cloud Audit Logs.

#### 4) CI/CD y cadena de suministro
- Build: Cloud Build (triggers por branch/tag), metadatos verificables.
- Artefactos: Artifact Registry + Artifact Analysis (vulnerabilidades).
- Deploy: Cloud Deploy (aprobaciones 1-click, canary/blue-green, rollbacks).
- Confianza: Binary Authorization (attestations/políticas).
- End-to-end: Software Delivery Shield.

#### 5) Observabilidad (Golden Signals)
- Latency, Traffic, Errors, Saturation.
- Logging: structured logs (JSON), log-based metrics y alerts.
- Error Reporting: deduplicación y stack traces.
- Trace: latencias entre servicios; Profiler: hotspots CPU/memoria.
- Managed Prometheus para Kubernetes (PromQL).

#### 6) ML y Generative AI
- APIs pre-entrenadas: Vision, Speech, Translation, Natural Language, Video Intelligence.
- AutoML (Vertex AI): entrenar sin código (imagen/tabular/texto/video).
- Generative AI: Vertex AI Codey/Gemini para código; prompts -> generación/explicación/arreglo.

---

### Árboles de decisión rápidos

1) ¿Dónde desplegar?
- ¿HTTP/gRPC serverless, poco ops y escala 0->N? -> Cloud Run
- ¿Protocolos no HTTP, control fino de redes/nodos o híbrido? -> GKE
- ¿SO/licencias específicas o máximo control? -> Compute Engine

2) ¿Dónde guardar datos?
- ¿OLTP relacional? -> Cloud SQL (single/regional) o AlloyDB (alto rendimiento) o Spanner (global, fuerte consistencia)
- ¿OLAP/BI? -> BigQuery
- ¿NoSQL documentos y tiempo real/offline? -> Firestore
- ¿NoSQL KV/IoT/billones de filas? -> Bigtable
- ¿Archivos/estáticos? -> Cloud Storage
- ¿Cache ms? -> Memorystore

3) ¿Cómo autenticar?
- Workloads en GCP -> Service Account + ADC/metadata; evitar claves descargadas.
- GKE -> Workload Identity; Multi-cloud/on-prem -> Workload Identity Federation.
- Usuario final -> OAuth 2.0 / Identity Platform; apps internas -> IAP.

4) ¿Cómo observar y mejorar performance?
- Dashboards con 4 señales; logs estructurados + métricas basadas en logs.
- Investigar errores en Error Reporting; latencias con Trace; CPU/mem con Profiler.

---

### Links útiles
- M06 – CI/CD y contenedores: [Deploying applications](06 - Deploying_Applicattions.md)
- M07 – Compute: [Compute Options](07 - Compute_Options_Applications.md)
- M03 – Storage: [Data Storage Options](03 - Data_Storage_Options.md)
- M04 – AuthN/Z: [Handling AuthN/AuthZ](04 - Handling_Authr_And_Authz.md)
- M08 – Observabilidad: [Monitoring & Performance](08 - Monitoring_Performance_Tuning.md)
- M05 – IA/ML: [Adding Intelligence](05 - Adding_Intelligence_Application.md)


