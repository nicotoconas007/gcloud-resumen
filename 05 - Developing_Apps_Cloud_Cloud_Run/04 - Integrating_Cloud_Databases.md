## Módulo 4 – Integrating with Cloud Databases

### Resumen
Integración de Cloud Run Functions con bases de datos de Google Cloud: Memorystore (Redis/Memcached) y Firestore; uso de variables de entorno y secretos; y BigQuery Remote Functions para invocar funciones desde SQL.

### Bases de datos soportadas
- Firestore (NoSQL, serverless, multi‑región)
- Cloud SQL (relacional)
- Spanner (SQL distribuido)
- Bigtable (NoSQL de baja latencia)
- BigQuery (analítica)
- Memorystore (Redis/Memcached)

### Conexión con Memorystore (Redis)
- Servicio gestionado (HA, escalable, failover, IAM/Monitoring).
- Pasos: identificar VPC autorizada → crear Serverless VPC Access connector (misma región) → adjuntar conector → setear env vars (host/puerto) → usar en código.

### Variables de entorno en Cloud Run Functions
- Key‑value pairs definidos en despliegue; almacenados por función.
- Configuración: gcloud, consola o archivo YAML versionado.
- Acceso: Python `os.environ` (otros lenguajes en docs oficiales).

### Conexión con Firestore
- DB serverless de documentos/colecciones.
- Triggers: create/update/delete/write en Native Mode (no en Datastore mode).
- Requiere document path + tipo de evento; snapshots incluyen datos before/after y referencias.
- SDKs: Firestore SDK (modificar el documento disparador) y Firebase Admin SDK (otros docs).

### Uso de Secrets
- Secret Manager guarda credenciales sensibles (API keys, passwords) con metadatos y versiones.
- Conceder `roles/secretmanager.secretAccessor` al runtime service account.
- Inyección: mounted volume (siempre última versión) o env var (versión fija al startup).
- Secretos en otros proyectos: dar permiso explícito y usar ruta `projects/PROJECT_ID/secrets/SECRET_NAME`.

### BigQuery Remote Functions
- Invocar Cloud Run Functions desde SQL.
- Requiere conexión `CLOUD_RESOURCE` y rol Invoker para el service account de la conexión.
- Crear con `CREATE FUNCTION ... REMOTE WITH CONNECTION`; ideal para validaciones/enriquecimiento.

Referencia: [Integrating with cloud databases](https://storage.googleapis.com/cloud-training/T-DVFUNC-I/v1.0.0/od/en/M4_Integrating_Cloud_Databases.pdf)

### Quiz (oficial)
1) Which statements about triggering functions from Firestore events are correct? (Select two)
   - A) Functions can be triggered on document create/update/delete
   - B) Triggers work in Datastore mode and Native mode
   - C) You must specify an event type and document path
   - D) Triggers can target specific document fields
   - Respuestas: A, C

2) What are two methods of making a secret available to a function?
   - A) Include the secret in source code
   - B) Provide as an environment variable at deploy time
   - C) Mount the secret as a volume (file)
   - D) Store in plaintext in ConfigMap
   - Respuestas: B, C

3) Which statements about environment variables are correct? (Select three)
   - A) Can be stored in a YAML file and passed at deploy time
   - B) Are key‑value pairs accessed by code at runtime
   - C) Are provided during function deployment
   - D) Are immutable and cannot be changed without redeploy
   - Respuestas: A, B, C

### Preguntas extra (práctica)
4) Which database services can functions integrate with directly?
   - A) Firestore, Cloud SQL, Spanner, Bigtable, BigQuery, Memorystore
   - Respuesta: A) Firestore, Cloud SQL, Spanner, Bigtable, BigQuery, Memorystore

5) When connecting functions to Memorystore Redis, what is required?
   - A) Public IP access
   - B) Serverless VPC Access connector in the same region
   - C) NAT Gateway
   - D) Private Service Connect
   - Respuesta: B) Serverless VPC Access connector in the same region

6) Which Firestore mode supports function triggers?
   - A) Datastore mode only
   - B) Native Mode only
   - C) Both modes
   - D) Neither
   - Respuesta: B) Native Mode only

7) Difference between mounting a secret as a volume vs env var?
   - A) Volume: latest version on each read; Env var: fixed version at startup
   - B) Volume: fixed version; Env var: always latest
   - C) Both always latest
   - D) Both fixed at deploy time
   - Respuesta: A) Volume latest; Env var fixed

8) In BigQuery Remote Functions, what is required to allow BigQuery to invoke Cloud Run?
   - A) VPN tunnel
   - B) CLOUD_RESOURCE connection with Cloud Run/Functions Invoker role
   - C) Expose function publicly
   - D) Shared VPC
   - Respuesta: B) CLOUD_RESOURCE connection with Invoker role