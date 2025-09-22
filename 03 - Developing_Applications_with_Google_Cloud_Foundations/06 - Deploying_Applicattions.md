## Módulo 6 – Deploying Applications

### Resumen
Cómo construir un proceso repetible y seguro para construir y desplegar aplicaciones en Google Cloud.

#### 1) CI/CD pipeline
- Continuous Integration (CI): devs commitean en ramas de feature; un servicio de build como Cloud Build se dispara automáticamente; genera artefactos (contenedores/ejecutables) y los almacena en Artifact Registry.
- Continuous Delivery (CD): al push a main, se construyen imágenes y se despliegan a staging (Cloud Deploy → Cloud Run/GKE) para tests de integración y performance. Si todo pasa, se marca como release candidate. Aprobación manual opcional para producción (canary o blue/green). Continuous Deployment elimina la aprobación manual.
- Observabilidad: Cloud Monitoring para performance; posibilidad de rollback rápido.

#### 2) Seguridad de la cadena de suministro
- Software Delivery Shield: solución integral y administrada para seguridad end‑to‑end del pipeline.
- Assured Open Source Software: paquetes Java/Python verificados y mantenidos por Google.
- Cloud Build: ejecuta builds en infraestructura de Google y mantiene metadatos verificables (supply chain).
- Artifact Registry + Artifact Analysis: almacena artefactos y escanea vulnerabilidades (imágenes base, paquetes Maven y Go) con monitoreo continuo.
- Cloud Deploy: CD con aprobaciones de un clic, rollbacks y security insights.
- Binary Authorization: aplica políticas de confianza mediante attestations; impide desplegar imágenes no confiables.
- GKE y Cloud Run: paneles/insights de seguridad y recomendaciones.

Referencia: [Module 6 – Deploying applications](https://storage.googleapis.com/cloud-training/devapps-foundations/en/on-demand/v1.2.0/Module6-DeployingApplications.pdf)
Más info: [Software Delivery Shield](https://cloud.google.com/software-supply-chain-security/docs/sds/overview), [Assured OSS](https://cloud.google.com/assured-open-source-software/docs/overview), [Cloud Build](https://cloud.google.com/build/docs/overview), [Artifact Registry](https://cloud.google.com/artifact-registry/docs/overview), [Artifact Analysis](https://cloud.google.com/artifact-analysis/docs/artifact-analysis), [Cloud Deploy](https://cloud.google.com/deploy/docs/overview), [Binary Authorization](https://cloud.google.com/binary-authorization/docs/overview)

#### 3) Contenedores y construcción de imágenes
- Contenedores arrancan más rápido que VMs y usan menos recursos; aíslan dependencias a nivel SO; favorecen portabilidad (laptop → on‑prem → cloud).
- Cloud Build: define pipeline en YAML/JSON; cada paso es un contenedor; el código se monta en `/workspace`; artefactos intermedios persisten en `/workspace` para pasos siguientes; publica imágenes a Artifact Registry; triggers automáticos por commits/branches/tags; notificaciones vía Pub/Sub.
- Artifact Registry: gestiona imágenes/artefactos; estado e historial de builds; análisis de vulnerabilidades integrado.

### Quiz (oficial)
1) Which statements about CI/CD are accurate? Select two.
   - A) Continuous integration is a workflow where developers frequently pull from master and commit changes into a feature branch
   - B) If all tests pass, builds from CI in a feature branch can be released directly to production
   - C) To benefit from CI/CD you must use GitHub
   - D) Continuous delivery is triggered when changes are pushed to the main branch
   - E) Any CI/CD pipeline on Google Cloud automatically provides best security practices
   - Respuestas: A) CI workflow en feature branch, D) CD al push a main

2) How can Cloud Build and Artifact Registry help you build a CI/CD pipeline? Select two.
   - A) Install Cloud Build on GKE; it will autoscale with number of builds
   - B) Builds must be started manually with gcloud on every commit
   - C) Artifacts from each build step persist in /workspace for following steps
   - D) Each build step specifies how to build an application container image
   - E) You can create pipelines that are automatically triggered when you commit code to a repository
   - Respuestas: C) /workspace persiste artefactos, E) triggers automáticos por commits

### Preguntas extra (práctica estilo certificación)
3) Which Google Cloud service provides automated rollbacks and one‑click approvals for application delivery?
   - A) Cloud Build
   - B) Cloud Monitoring
   - C) Cloud Deploy
   - D) Binary Authorization
   - Respuesta: C) Cloud Deploy

4) Which service provides end‑to‑end CI/CD supply chain security?
   - A) Artifact Registry
   - B) Software Delivery Shield
   - C) Assured OSS
   - D) Cloud Run
   - Respuesta: B) Software Delivery Shield

5) Main advantage of containers vs VMs for application deployment?
   - A) Full OS‑level virtualization
   - B) Include hypervisors for better isolation
   - C) Lightweight, portable, and start much faster
   - D) Require fewer dependencies to run
   - Respuesta: C) Lightweight, portable, and start much faster

6) Which service enforces policies so only trusted images are deployed?
   - A) Artifact Analysis
   - B) Binary Authorization
   - C) Cloud Monitoring
   - D) Pub/Sub
   - Respuesta: B) Binary Authorization

7) When Cloud Build executes a pipeline, where are intermediate artifacts stored for subsequent steps?
   - A) /tmp
   - B) Cloud Storage
   - C) /workspace
   - D) Pub/Sub
   - Respuesta: C) /workspace