## Módulo 02 – Introduction to Cloud Run and Google Kubernetes Engine

### Cloud Run (resumen)
- Plataforma serverless para ejecutar contenedores con autoescalado (hasta 0), URL HTTPS automática, revisiones inmutables y despliegues graduales/rollback.
- Flujos: basado en imagen (máximo control) o basado en código fuente (Buildpacks construyen la imagen).
- Modelos de precio: pay‑per‑use y CPU always allocated.
- Servicio regional con alta disponibilidad multi‑zona.
- Casos típicos: APIs/microservicios, sitios web, eventos (Pub/Sub), tareas programadas (Scheduler).

### Google Kubernetes Engine (GKE)
- Kubernetes administrado por Google: despliegue, gestión y escalado simplificados.
- Arquitectura: control plane (zonal/regional) y nodes (VMs de Compute Engine).
- Objetos clave: Pod (1+ contenedores), Deployment (estado deseado y réplicas), Service (IP/DNS estable y balanceo), Volume (datos compartidos/persistencia).
- Tooling: Cloud Code, Cloud Build, Artifact Registry, Cloud Deploy.

### Container‑Optimized OS
- SO de Compute Engine optimizado para contenedores (basado en Chromium OS): Docker preinstalado, hardening de seguridad, actualizaciones automáticas.
- Limitaciones: sin gestor de paquetes, solo apps en contenedor, sin módulos de kernel de terceros, solo en Google Cloud.
- Uso: ejecutar contenedores en VMs con mínima configuración y máxima seguridad.

### Quiz (oficial)
1) Which statements about Cloud Run are correct? (Select three)
   - A) You can use Cloud Run to execute scheduled tasks or jobs
   - B) Cloud Run runs and autoscales containers on‑demand
   - C) You must manually provision an HTTPS endpoint URL
   - D) You can deploy using Console, gcloud, YAML or Terraform
   - Respuestas: A, B, D

2) Which statements about Kubernetes and GKE are correct? (Select three)
   - A) You can manage resources imperatively or declaratively
   - B) A cluster consists of a control plane and nodes
   - C) GKE is a fully managed Kubernetes service on Google Cloud
   - D) A GKE cluster can only contain a single control plane
   - Respuestas: A, B, C

3) From which registries can Cloud Run pull images? (Select three)
   - A) Container Registry
   - B) Artifact Registry
   - C) Docker Hub
   - D) Only private on‑prem registries
   - Respuestas: A, B, C

4) In Kubernetes, a pod is:
   - A) A collection of services
   - B) Another name for a Deployment
   - C) A group of one or more containers
   - D) A set of nodes
   - Respuesta: C

5) Which two pricing models are supported by Cloud Run?
   - A) Pay per use
   - B) Based on number of containers deployed
   - C) CPU always allocated
   - D) Fixed fee per service
   - Respuestas: A, C

### Preguntas extra (práctica)
6) Deploy a new version to Cloud Run creates:
   - A) A new service
   - B) A new container instance
   - C) An immutable revision
   - D) A new HTTPS endpoint
   - Respuesta: C

7) In GKE, which object provides stable IP and load balancing for pods?
   - A) Deployment
   - B) Pod
   - C) Node
   - D) Service
   - Respuesta: D

8) OS image to run a Docker container on a VM with minimal setup and strong security?
   - A) Debian
   - B) Windows Server
   - C) Container‑Optimized OS
   - D) Ubuntu
   - Respuesta: C

9) Primary purpose of a ReplicaSet (managed by a Deployment)?
   - A) Provide persistent storage for pods
   - B) Expose pods to external traffic
   - C) Define network policy between pods
   - D) Maintain a stable set of replica pods
   - Respuesta: D

10) In source‑based deployment on Cloud Run, which tech builds your code into an image?
   - A) Dockerfile
   - B) Buildpacks
   - C) Jenkins
   - D) Skaffold
   - Respuesta: B