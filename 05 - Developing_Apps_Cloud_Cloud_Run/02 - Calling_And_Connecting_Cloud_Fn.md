## Módulo 2 – Calling and Connecting Cloud Run Functions

### Resumen
Cómo invocar Cloud Run Functions con triggers HTTP y de eventos (Eventarc), orquestarlas con Workflows y conectarlas a recursos internos mediante Serverless VPC Access.

### Triggers en Cloud Run Functions
- HTTP(S) triggers → invocan funciones HTTP, generan endpoint HTTPS; métodos: GET, POST, PUT, DELETE, OPTIONS.
- Event triggers → reaccionan a eventos vía Eventarc (90+ fuentes): Pub/Sub, Cloud Storage, Firestore, Firebase, Cloud Audit Logs, Cloud Scheduler, Gmail, etc.
- Reglas: una función = un trigger a la vez; múltiples funciones pueden compartir trigger; filtros de eventos por servicio/método/tipo.

### Tipos de triggers soportados
- HTTP: webhooks, APIs, tareas programadas (Scheduler/Tasks).
- Pub/Sub: al publicar en un tópico; CloudEvent (2nd gen) o Background (legacy).
- Cloud Storage: eventos en buckets (finalize/delete/archive/metadata update); CloudEvent o StorageObjectData.
- Firestore: create/update/delete/write a nivel documento en mismo proyecto.
- Firebase (1st gen): Analytics, Auth, Realtime DB, Remote Config.

### Conectar funciones con Workflows
- Workflows orquesta pasos (YAML/JSON): llamadas HTTP a funciones, APIs externas, manejo de estado/reintentos/esperas hasta 1 año; ejecuciones observables.

### Conexión a VPC con Serverless VPC Access
- Conecta funciones serverless a VPC interna para acceder a VMs, Memorystore, BBDD, etc., usando DNS/IP internos (sin Internet).
- Requisitos: habilitar API; crear conector por VPC/región; reservar subnet /28 exclusiva; adjuntar conector por función.
- Seguridad: reglas de firewall; soporta Shared VPC (host/service project).

Referencia: [Calling and Connecting Cloud Run functions](https://storage.googleapis.com/cloud-training/T-DVFUNC-I/v1.0.0/od/en/M2_Calling_and_Connecting_Cloud_Run_Functions.pdf)

### Quiz (oficial)
1) What are two reasons for using Serverless VPC Access?
   - A) Enable functions to access external HTTP endpoints
   - B) Expose VPC traffic to the Internet
   - C) Send requests and receive responses using internal DNS and IPs
   - D) Connect functions to internal resources in a VPC network
   - Respuestas: C, D

2) An HTTP trigger: (Select two)
   - A) Does not support DELETE
   - B) Generates a URL for the function
   - C) Enables a function to respond to HTTP requests
   - D) Enables a function to respond to cloud events
   - Respuestas: B, C

3) Which statements about Workflows are correct? (Select three)
   - A) Can combine services or functions hosted on Cloud Run
   - B) Data cannot be shared between steps
   - C) A step can make an HTTP call to a URL
   - D) Workflows is serverless
   - Respuestas: A, C, D

4) Which statements about Cloud Run functions triggers are correct? (Select three)
   - A) An event trigger reacts to cloud events
   - B) Multiple functions can share the same trigger settings
   - C) A function can be bound to multiple triggers at the same time
   - D) Triggers are specified during deployment
   - Respuestas: A, B, D