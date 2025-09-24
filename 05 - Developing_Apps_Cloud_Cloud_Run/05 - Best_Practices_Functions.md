:

## Módulo 05 – Best Practices for Functions

### Resumen
Buenas prácticas para implementar, monitorear y operar Cloud Run Functions: idempotencia, manejo correcto de HTTP/eventos, logging/observabilidad, performance, retries, IAM mínimo privilegio y control de escalado/tráfico.

### Implementación de funciones
- Idempotencia para soportar reintentos sin inconsistencias.
- HTTP functions: siempre devolver respuesta; evitar tareas en background tras responder.
- Asincronismo: esperar finalización de operaciones async; capturar y reportar excepciones (Error Reporting). Evitar `process.exit()`/`sys.exit()`.
- Filesystem temporal: usar sólo `/tmp`, limpiar archivos para reducir cold starts.

### Logging y monitoreo
- Escribir a stdout/stderr → aparece en Cloud Logging.
- Reportar errores con códigos HTTP adecuados o mensajes claros en funciones de eventos.

### Performance y networking
- Minimizar cold start: reducir dependencias; inicialización lazy cuando aplique.
- Reusar clientes en global scope (HTTP, DB, SDKs); conexiones persistentes.
- Serverless VPC Access para recursos privados en VPC cuando corresponda.

### Retrying functions
- Disponible en funciones event‑driven; deshabilitado por defecto.
- Habilitar con consola o `--retry`; reintentos hasta 7 días para fallos transitorios.
- Evitar loops: timestamps/flags de corte.

### Configuración e IAM
- Mínimo privilegio; cada función con su propia service account administrada por el usuario.
- Limitar quién puede invocar/administrar; encadenar sólo funciones necesarias.

### Escalabilidad y tráfico
- min/max instances por función (min evita cold starts; max protege downstream).
- Concurrency: múltiples requests por instancia si el código es thread‑safe.
- Revisions: inmutables por despliegue; se puede dividir tráfico y hacer rollback.

Referencia: [Best Practices for Functions](https://storage.googleapis.com/cloud-training/T-DVFUNC-I/v1.0.0/od/en/M5_Best_Practices_for_Functions.pdf)

### Quiz (oficial)
1) IAM Policies: Which are good practices? (Select three)
   - A) Use default service account in production
   - B) Grant only minimum required permissions
   - C) Limit users and service accounts with access
   - D) Allow each function to call only necessary downstream functions
   - Respuestas: B, C, D

2) Networking: Which optimize networking for functions? (Select two)
   - A) Persistent HTTP connections
   - B) Serverless VPC Access for internal resources
   - C) Initialize connections inside local scope per request
   - D) Avoid global clients
   - Respuestas: A, B

3) Revisions: Which statements are correct? (Select one)
   - A) You cannot rollback
   - B) You can split traffic across revisions
   - C) A deployed revision is mutable
   - D) No new revision is created on each deploy
   - Respuesta: B

4) Retrying: Which are correct? (Select two)
   - A) Retries up to 7 days
   - B) Enabled by default
   - C) Available for HTTP and event‑driven
   - D) Enabled via console or `--retry`
   - Respuestas: A, D

5) Performance: Which practices help? (Select three)
   - A) Set min instances
   - B) Reuse clients/objects in global scope
   - C) Remove unused dependencies
   - D) Always eager‑initialize everything
   - Respuestas: A, B, C

6) Scalability: How to control scaling? (Select one)
   - A) Global config applies to all functions
   - B) Configure min/max per function
   - C) Scaling is uncontrolled in serverless
   - D) Functions do not scale
   - Respuesta: B

### Preguntas extra (práctica)
7) What happens if an HTTP function does not return a response?
   - A) Invocation auto‑cancels
   - B) Keeps running until timeout, incurring cost
   - C) Cloud Run restarts with cold start
   - D) Auto‑retries
   - Respuesta: B

8) Consequence of uncaught exceptions?
   - A) Only current execution is lost
   - B) May increase cold starts in future invocations
   - C) Cloud Logging ignores the error
   - D) Automatic retry is activated
   - Respuesta: B

9) Benefit of concurrency in functions?
   - A) Improves security by isolating requests
   - B) Reduces latency/cold starts handling multiple requests on warm instances
   - C) Reduces memory cost
   - D) Removes need for min instances
   - Respuesta: B