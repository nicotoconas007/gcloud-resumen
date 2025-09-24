## Módulo 1 – Introduction to Cloud Run Functions

### Resumen
Cloud Run Functions es una plataforma serverless FaaS en Google Cloud para funciones HTTP y orientadas a eventos. Escala automáticamente, integra con IAM, Logging/Monitoring y servicios como Pub/Sub, Storage y Firestore. Hay 1st gen (legacy) y 2nd gen (sobre Cloud Run) con más triggers y flexibilidad.

### Versiones
- 2nd gen: basada en Cloud Run; triggers vía Eventarc/Pub/Sub; mayor flexibilidad y escalabilidad.
- 1st gen: versión original con menos triggers y opciones.

### Features principales
- Desarrollo y pruebas locales.
- Autenticación con service accounts (IAM).
- Tipos: HTTP Functions (requests HTTP/S) y Event‑driven Functions (eventos de Pub/Sub, Storage, Firestore, Firebase, etc.).
- Integración con Cloud SQL, Firestore, Bigtable, Spanner.
- Runtimes: Go, Node.js, Python, Java, .NET, Ruby.
- Autoscaling a gran escala; observabilidad (Logging/Monitoring).
- Pricing pay‑as‑you‑go.

### Beneficios
- Extensión de servicios cloud con lógica personalizada, sin gestionar servidores.
- Autoscaling según demanda; costos por uso real.
- Resiliencia y portabilidad con contenedores y triggers estándar.

### Tipos de funciones
#### HTTP Functions
- URL única; típicos: webhooks, APIs REST, endpoints externos.
- Deben responder con HTTP; por defecto requieren autenticación (se puede abrir).

#### Event‑driven Functions
- Responden a eventos de infraestructura (Storage, Pub/Sub, etc.).
- Implementaciones: CloudEvent Functions (recomendado en 2nd gen) y Background Functions (legacy en 1st gen).
- Casos: procesamiento de datos/medios, backend móvil con Firebase/Firestore, IoT vía Pub/Sub.

### Capacidades técnicas
- Hasta 32 GB RAM y 4 vCPU; hasta 1000 requests concurrentes por instancia.
- Timeouts: 60 min (HTTP), 10 min (event‑driven).
- Revisions por despliegue; rollback/split traffic.
- Integración con Artifact Registry y Cloud Build.

### Despliegue
- Métodos: Console, gcloud, Cloud Code, Cloud Build, repos (GitHub/Bitbucket/CSR).
- Requisitos: roles de IAM (Cloud Functions Developer, Service Account User), APIs de Cloud Build y Artifact Registry habilitadas.
- Flujo: código → build → imagen en Artifact Registry → ejecución en Cloud Run Functions.

### Casos de uso
- Data processing (imágenes, validación, ETL), webhooks/APIs, backends móviles, IoT con Pub/Sub.

Referencia: [Introduction to Cloud Run Functions](https://storage.googleapis.com/cloud-training/T-DVFUNC-I/v1.0.0/od/en/M1_Introduction_to_Cloud_Run_Functions.pdf)

### Quiz (oficial)
1) An HTTP function: (Select three)
   - A) Can be used to implement a webhook
   - B) Is triggered by a request to its URL endpoint
   - C) Must send back an HTTP response
   - D) Can only be invoked with authentication credentials
   - Respuestas: A, B, C

2) An event‑driven function: (Select three)
   - A) Responds to events that occur in your cloud infrastructure
   - B) Can be triggered from Eventarc sources
   - C) Uses triggers for services like Pub/Sub and Cloud Storage
   - D) Can only be implemented as a CloudEvent function
   - Respuestas: A, B, C

3) What are features/benefits of Cloud Run functions? (Select four)
   - A) Supports seamless authentication with IAM
   - B) Can be integrated with Cloud databases
   - C) Are triggered by HTTP requests and events from Cloud Services
   - D) Can be locally developed and tested
   - E) Uses a fixed pricing model
   - Respuestas: A, B, C, D

4) Which statements about Cloud Run functions are correct? (Select three)
   - A) Integrated with Cloud Logging
   - B) Scalable functions‑as‑a‑service platform
   - C) Can be used to extend Cloud services
   - D) Require servers or VMs to be provisioned
   - E) Can only be invoked by sending HTTP requests
   - Respuestas: A, B, C