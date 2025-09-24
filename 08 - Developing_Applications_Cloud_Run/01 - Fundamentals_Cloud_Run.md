## Fundamentals Cloud Run
Cloud Run es una plataforma serverless para desplegar y ejecutar contenedores en Google Cloud. Te enfocas en el código; Google gestiona infraestructura, escalado y mantenimiento.

### Modos de ejecución
- Servicios (Services): diseñados para ejecutar continuamente y responder a HTTP(S), gRPC, WebSockets o eventos (Pub/Sub, Eventarc).
- Trabajos (Jobs): diseñados para tareas por lotes o puntuales; finalizan al completar el trabajo.

### Características clave
- URL HTTPS automática (.run.app)
- Serverless (sin servidores a gestionar)
- Integración nativa: Cloud SQL, Pub/Sub, Cloud Storage, IAM
- Pago por uso (CPU/memoria mientras procesa solicitudes)

### Modelo de recursos y revisiones
- Servicio: recurso regional; instancias distribuidas multi‑zona para alta disponibilidad.
- Revisión: se crea en cada despliegue/cambio; es inmutable; contiene imagen y configuración (env vars, memoria, concurrencia). Por defecto el tráfico va a la última revisión saludable; se puede dividir tráfico y hacer rollback.
- Job: 1+ tareas en paralelo; éxito si todas completan correctamente.

### Ciclo de vida del contenedor
- Starting: descarga imagen e inicia app; lista cuando escucha en el puerto (por defecto 8080).
- Serving requests: procesa 1 o varias solicitudes (según concurrencia).
- Idle: CPU estrangulada; sin costos por defecto; puede detenerse en cualquier momento.
- Shutting down: señal SIGTERM y hasta 10 s para limpieza; luego se fuerza cierre.
- Stopped: detenida (por fallo o límites de memoria).

### Autoescalado
- Ajuste automático de instancias según tráfico; escala a cero por defecto (posible cold start).
- Configuraciones clave: `--min-instances` (evita cold start), `--max-instances` (límite para proteger downstream/costos), `--concurrency` (solicitudes simultáneas por instancia; 1 = exclusivas).

### Control de acceso
- IAM (quién): servicios privados por defecto; rol clave `roles/run.invoker`. Público: asignar `run.invoker` a `allUsers` o usar `--allow-unauthenticated`.
- Ingress (desde dónde): All (internet), Internal (solo VPC/proyecto/perímetro VPC‑SC), Internal and Cloud Load Balancing (interno + LB externo HTTP(S)).
- Acceso a recursos privados: Serverless VPC Access connector.

### Quiz (práctica)
1) Which statements about autoscaling in Cloud Run are correct? (Select three)
   - A) A container instance can process only a single request at a time
   - B) When requests decrease, Cloud Run reduces the number of instances
   - C) Cloud Run automatically increases instances when necessary
   - D) As requests increase, active instances might decrease and idle increase
   - E) With no incoming requests, by default the last instance will be shut down
   - Respuestas: B, C, E

2) Which statements about Cloud Run are correct? (Select three)
   - A) You must manually provision an HTTP endpoint
   - B) Cloud Run cannot access internal resources in your VPC
   - C) Cloud Run is serverless
   - D) Code can run as a service or as a job
   - E) Integrates with other Google Cloud services
   - Respuestas: C, D, E

3) How to make a Cloud Run service publicly invokable without auth?
   - A) Not possible
   - B) Use --allow-unauthenticated on deploy
   - C) Public by default
   - D) Grant only roles/viewer
   - Respuesta: B

4) Characteristics of an idle container? (Select four)
   - A) CPU throttled
   - B) Does not service requests
   - C) Incurs charges by default
   - D) Can reliably run background tasks
   - E) Can be shut down at any time
   - Respuestas: A, B, E (y no incurre cargos por defecto)

5) Characteristics of Cloud Run services? (Select three)
   - A) A service revision is mutable
   - B) You must manually route to latest revision
   - C) Cloud Run automatically scales a service revision
   - D) Services are regional resources
   - E) Each deployment creates a service revision
   - Respuestas: C, D, E