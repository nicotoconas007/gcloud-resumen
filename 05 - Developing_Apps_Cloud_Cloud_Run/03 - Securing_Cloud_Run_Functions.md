## Módulo 3 – Securing Cloud Run Functions

### Resumen
Asegurar Cloud Run Functions implica controles de identidad (IAM), controles de red (ingress/egress, VPC Service Controls) y protección de datos con claves administradas por el cliente (CMEK).

### Identity & Access Control (IAM)
- Flujo: autenticación (verificar identidad) → autorización (verificar permisos IAM).
- Identidades: service accounts (workloads) y user accounts (personas/grupos).
- Tokens: OAuth 2.0 access token (APIs) e ID token (invocación entre servicios HTTP).
- Roles predefinidos (Cloud Functions): Admin, Developer, Invoker, Viewer.
- Runtime service account: cada función se ejecuta con una SA. Por defecto: Compute Engine default SA (o App Engine default SA en 1st gen). En prod, crear SA dedicada con mínimo privilegio.

### Network-based Access Control
- Ingress settings: controlar quién invoca (público, interno, interno + Cloud Load Balancing).
- Egress settings: enrutar tráfico saliente mediante Serverless VPC Access connector (todo el tráfico o solo IPs privadas).
- VPC Service Controls: perímetros para evitar fuga de datos; puede exigir uso de VPC connector y bloquear accesos fuera del perímetro.

### Protección con CMEK (Customer‑Managed Encryption Keys)
- Gestionás tus propias claves (Cloud KMS) para cifrar código/artefactos/transportes.
- Si la clave se deshabilita/destruye: instancias existentes pueden seguir corriendo; nuevas ejecuciones que requieran desencriptar fallan.
- Conceder acceso a service agents: Cloud Run Functions, Artifact Registry, Cloud Storage, etc.

Referencia: [Securing Cloud Run Functions](https://storage.googleapis.com/cloud-training/T-DVFUNC-I/v1.0.0/od/en/M3_Securing_Cloud_Run_Functions.pdf)

### Quiz (oficial)
1) To limit access to Cloud Run functions, what methods can you use? (Select two)
   - A) Identity‑based access controls (IAM)
   - B) Network‑based access controls (ingress/egress)
   - C) Disable Cloud Logging
   - D) Use only public endpoints
   - Respuestas: A, B

2) Which network setting routes all outbound traffic from a function through a VPC network?
   - A) Ingress: internal only
   - B) Ingress: internal + load balancer
   - C) Egress: all traffic through Serverless VPC connector
   - D) Egress: only public IPs through connector
   - Respuesta: C) Egress: all traffic through Serverless VPC connector

3) What is the impact of disabling/destroying a CMEK key?
   - A) Existing running instances are immediately terminated
   - B) Executions that require new function instances will fail
   - C) Existing logs are deleted
   - D) All invocations are blocked even if warm instances exist
   - Respuesta: B) Executions that require new function instances will fail

4) Which predefined IAM roles exist for Cloud Run functions? (Select four)
   - A) Cloud Functions Admin
   - B) Cloud Functions Developer
   - C) Cloud Functions Invoker
   - D) Cloud Functions Viewer
   - E) Cloud Functions Auditor
   - Respuestas: A, B, C, D

5) Which statements about function identity are correct? (Select three)
   - A) Every function has a runtime service account identity
   - B) Compute Engine default SA is the default runtime SA
   - C) App Engine default SA is default runtime SA in 1st gen
   - D) Functions cannot use custom service accounts
   - Respuestas: A, B, C