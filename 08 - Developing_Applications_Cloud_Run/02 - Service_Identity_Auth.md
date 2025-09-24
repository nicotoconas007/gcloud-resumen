## Service Identity and Authentication
Cloud Run interactúa con APIs de Google Cloud usando identidades gestionadas por IAM.

### Cuentas de servicio e identidad
- Identidad: apps que llaman APIs (p.ej., Pub/Sub) requieren una identidad; IAM valida identidad y permisos.
- Service Account: identidad para workloads (apps, VMs, Cloud Run); sin contraseña; identificada por email.
- En Cloud Run, cada servicio o job se asocia a una service account (identidad de ejecución).

### Tokens y flujos
- Access Token (OAuth 2.0): para llamar APIs de Google (Storage, Pub/Sub, etc.).
- ID Token (OIDC): para invocar otro servicio de Cloud Run.
- Flujo API: app con librería cliente → usa SA para obtener token → llama API → IAM valida token/permisos.
- Servicio a servicio: SA llamadora obtiene ID token; servicio receptor debe otorgar `roles/run.invoker` a esa SA.

### Jerarquía y herencia de IAM
- Organización → Carpetas → Proyecto → Recurso (Cloud Run, Pub/Sub, etc.).
- Políticas heredadas hacia abajo; no se pueden “negar” en niveles inferiores.

### Least privilege y roles
- Roles básicos: Owner/Editor/Viewer (muy amplios) → evitar en producción.
- Roles predefinidos: granulares por servicio (p.ej., `roles/pubsub.publisher`, `roles/storage.objectAdmin`). Recomendados.
- Roles custom: permisos exactos cuando lo predefinido no alcanza.
- Default SA: Cloud Run usa por defecto la SA de Compute Engine (suele tener Editor a nivel proyecto) → riesgo. Crear SA dedicada por servicio y otorgar solo permisos mínimos necesarios.

### Secrets y variables de entorno
- Env vars: CLAVE=VALOR inyectadas al contenedor en despliegue; accesibles en runtime; prevalecen sobre ENV del Dockerfile.
- Secrets (Secret Manager): almacenar API keys, passwords, certs; exponer como volumen (recomendado: siempre última versión) o como env var (versionar fijo en startup). Requiere `roles/secretmanager.secretAccessor` para la SA de ejecución.

### Quiz (práctica)
1) Using environment variables with Cloud Run (Select two)
   - A) Once set, values cannot be updated
   - B) Injected into the container and accessed at runtime
   - C) Key‑value pairs set at deploy time (service/job)
   - D) Dockerfile ENV takes precedence over Cloud Run env vars
   - Respuestas: B, C

2) Methods to make a secret available to a Cloud Run service
   - A) Provide as environment variable at deploy time
   - B) Provide as query parameters
   - C) Not possible from Cloud Run
   - D) Mount as a volume (file)
   - Respuestas: A, D

3) Implement least privilege for a Cloud Run service
   - A) Use dedicated SA as service identity; grant minimal roles needed
   - B) Use only Google client libraries
   - C) Remove Editor from default SA but keep using it
   - D) Use secrets for needed data
   - Respuesta: A

4) IAM policy characteristics (Select three)
   - A) Attached to a Google Cloud resource
   - B) At most one binding per policy
   - C) Only one policy can be attached to a resource
   - D) A member can have only one role in a policy
   - E) A policy is a list of bindings mapping members to roles
   - Respuestas: A, E (y puedes adjuntar una política por recurso que contiene múltiples bindings; C/D/B son falsas)

5) Default role on the default service account linked to Cloud Run by default
   - A) Viewer
   - B) Billing Admin
   - C) Owner
   - D) Editor
   - Respuesta: D

6) Service A (SA) calling private service B over HTTP requires which role on B?
   - A) roles/run.serviceAgent
   - B) roles/run.viewer
   - C) roles/run.invoker
   - D) roles/run.editor
   - Respuesta: C

7) Grant roles/storage.objectViewer at Project level to a SA implies:
   - A) View objects in one specific bucket
   - B) View objects in all buckets in that project
   - C) Fails; roles cannot be granted at Project level
   - D) View and delete objects in all buckets
   - Respuesta: B

8) Prefer mounting a secret as a volume when:
   - A) Secret is very short
   - B) You want always latest version without redeploy
   - C) App is Python
   - D) Never; env vars are always better
   - Respuesta: B