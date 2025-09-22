## Módulo 7 – Compute Options for Your Applications

### Resumen
Opciones de cómputo en Google Cloud y cuándo elegir cada una. Más control implica más esfuerzo operativo; más abstracción reduce el mantenimiento.

#### Compute Engine (VMs)
- Control total sobre CPU, memoria, discos (Persistent/SSD), GPUs/TPUs y SO.
- Ideal para: lift & shift, requisitos de SO/software específico, protocolos no HTTP/S, personalización alta.
- Características: VMs preemptibles, autoscaling, load balancing, health checks.
- Costos: pagas por VMs dedicadas.

#### Google Kubernetes Engine (GKE)
- Kubernetes administrado por Google.
- Modos: Standard (más control) y Autopilot (Google gestiona el cluster completo).
- Integraciones: Cloud Monitoring/Logging, IAM, VPC, Artifact Registry.
- Ideal para: apps distribuidas/resilientes, híbridas/multi‑cloud, protocolos no HTTP/S, AI/ML con GPU/TPU.
- Costos: pagas la infraestructura subyacente.

#### Cloud Run (serverless containers)
- Contenedores serverless totalmente gestionados; escala 0→N en segundos y pago por uso.
- Modos de despliegue: imagen de contenedor (Artifact Registry/Docker Hub), código fuente (buildpacks), funciones/event‑driven (Pub/Sub, Eventarc), y Jobs (batch/cron con Cloud Scheduler).
- Ideal para: web apps y APIs, ETL/procesamiento, microservicios event‑driven, jobs batch bajo demanda.
- Protocolos: HTTP/1.1, HTTP/2 y gRPC; no expone puertos TCP arbitrarios.

### Comparación rápida
| Característica | Compute Engine | GKE | Cloud Run |
| --- | --- | --- | --- |
| Nivel de control | Máximo | Medio | Mínimo |
| Operación | Admin. completa (OS, parches, escalado) | Control plane por Google; apps por ti (o todo en Autopilot) | Google administra todo |
| Escalado | Manual/autoscaling | Autoscaling de pods y nodos | Automático 0→N |
| Costos | VM dedicada (predecible) | VM dedicada (predecible) | Pay‑per‑use |
| Protocolos | Cualquiera | Cualquiera (HTTP y no HTTP) | HTTP/HTTPS/gRPC |
| Casos típicos | Lift & shift, requisitos de SO/licencias | Distribuidas, híbridas, multi‑cloud, ML | Web APIs, event‑driven, batch |

Referencia: [Module 7 – Compute Options for Your Applications](https://storage.googleapis.com/cloud-training/devapps-foundations/en/on-demand/v1.2.0/Module7-ComputeOptionsForYourApplication.pdf)

### Quiz (oficial)
1) Your code needs to create a thumbnail of an image in response to a Pub/Sub event. Which execution environment should you consider?
   - A) Compute Engine
   - B) Google Kubernetes Engine
   - C) Cloud Run
   - D) App Engine (flexible environment)
   - Respuesta: C) Cloud Run

2) Your application uses network protocols other than HTTPS and runs partially on‑premises and partially in the cloud. Which environment should you consider?
   - A) App Engine (standard environment)
   - B) Google Kubernetes Engine
   - C) Cloud Run
   - D) Compute Engine
   - Respuesta: B) Google Kubernetes Engine

3) Your app is containerized, requires automatic scaling, and accepts requests over HTTP/gRPC. You do not want to manage infrastructure. Which is ideal?
   - A) Google Kubernetes Engine (Autopilot)
   - B) Cloud Run
   - C) App Engine (standard environment)
   - D) Compute Engine
   - Respuesta: B) Cloud Run

### Preguntas extra (práctica estilo certificación)
4) Which compute option provides the most control but the highest operational effort?
   - A) Compute Engine
   - B) GKE
   - C) Cloud Run
   - D) App Engine
   - Respuesta: A) Compute Engine

5) Which service is best suited for hybrid workloads across multiple clouds?
   - A) Compute Engine
   - B) Google Kubernetes Engine
   - C) Cloud Run
   - D) App Engine
   - Respuesta: B) Google Kubernetes Engine

6) Which service is best for event‑driven, pay‑per‑use workloads?
   - A) Compute Engine
   - B) GKE
   - C) Cloud Run
   - D) App Engine
   - Respuesta: C) Cloud Run

7) Which platform is recommended by Google for new services instead of App Engine?
   - A) Compute Engine
   - B) GKE
   - C) Cloud Run
   - D) App Engine Flexible
   - Respuesta: C) Cloud Run