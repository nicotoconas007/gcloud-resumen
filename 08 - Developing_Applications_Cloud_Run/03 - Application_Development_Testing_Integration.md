## Application development, testing, and integration
Este módulo cubre el ciclo de vida de una app para Cloud Run: desarrollo, pruebas, construcción/despliegue, revisiones/tráfico e integración.

### Desarrollo y pruebas
¿Mi app es apta para Cloud Run? Sí, si:

Atiende peticiones (HTTP, gRPC, WebSockets), eventos o es un job que termina.

No requiere un sistema de archivos local persistente (puede usar uno efímero en memoria o uno de red).

No necesita más de 8 vCPU u 32 GiB de RAM por instancia.

Ya está en un contenedor o se puede empaquetar en uno.

Contrato del contenedor (reglas clave):

Servicio: debe escuchar peticiones en un puerto (por defecto 8080, configurable con la variable $PORT).

Servicio: debe responder a las peticiones dentro del timeout configurado.

Job: debe finalizar con código de salida 0 si tiene éxito, y un código distinto de 0 si falla.

No implementar TLS (HTTPS): Cloud Run gestiona el HTTPS de forma transparente. El contenedor solo debe manejar tráfico HTTP.

Entornos de ejecución:
- 1ª Generación (servicios): mejores cold starts; emula syscalls Linux.
- 2ª Generación (jobs): compatibilidad total Linux; mejor CPU/red; requerido para NFS (Filestore/Storage FUSE).

Almacenamiento de archivos:
- Efímero: FS en memoria por instancia, no persistente.
- Persistente: 2ª gen + Filestore o Cloud Storage FUSE.

Herramientas y pruebas locales:
- Cloud Code (VS Code/IntelliJ) con emulador.
- gcloud CLI.
- Docker (correr el contenedor localmente).

### Construcción, despliegue y revisiones
Construcción de Contenedores: Se puede hacer con:

Docker: Localmente, usando un Dockerfile.

Cloud Build: En la nube, usando un Dockerfile o Buildpacks (que no requieren Dockerfile).

Cloud Run (despliegue desde fuente): Usa Buildpacks o un Dockerfile para construir y desplegar en un solo paso.

Registro de imágenes: Artifact Registry (recomendado) o Docker Hub.

Proceso de despliegue:
1) push a Artifact Registry
2) gcloud run deploy --image=...
3) Cloud Run copia la imagen a su almacenamiento interno (arranques rápidos y resiliencia si se borra del registry)

Revisiones:

Una revisión es una copia inmutable de la imagen del contenedor y su configuración.

Se crea una nueva revisión con cada despliegue o cada cambio de configuración (variables de entorno, memoria, etc.).

Gestión de tráfico:
- Estándar: 100% a la nueva revisión al estar lista.
- Traffic Splitting: porcentajes entre revisiones (canary/rollbacks).
- Revision tags: etiqueta con URL única (p.ej. https://green---service.run.app) para pruebas sin tráfico productivo.

### Integración con servicios de Google Cloud
Conexión a APIs de Google: Usar las librerías cliente de Google. Estas usan automáticamente la cuenta de servicio de Cloud Run para autenticarse.

Conexión a Bases de Datos y Caches:

Cloud SQL (MySQL, PostgreSQL, etc.):

Se establece la conexión a través de una "instance connection name".

La cuenta de servicio necesita roles como Cloud SQL Client.

Es crucial usar pools de conexiones para gestionar el límite de 100 conexiones por servicio.

Memorystore (Redis, Memcached):

La conexión se realiza a través de un Serverless VPC Access connector, ya que Memorystore vive dentro de una red VPC.

Integración con Pub/Sub:

Para enviar mensajes: Tu servicio llama a la API de Pub/Sub.

Para recibir mensajes: Se crea una suscripción de tipo push en Pub/Sub. Esta suscripción envía los mensajes como peticiones HTTP POST a la URL de tu servicio de Cloud Run. El servicio debe responder con un código 2xx para confirmar la recepción (ack), o un 4xx/5xx para que Pub/Sub reintente el envío.

Integrations: asistente en consola/gcloud para conexiones comunes (p.ej., Memorystore), creando VPC connector y recursos necesarios.

### Quiz (práctica)
1. Which of these statements regarding service revisions in Cloud Run are correct? (Select two)

A) A revision is created when you deploy a container image to a service in Cloud Run.

B) In Cloud Run, only the newest or latest service revision can receive and process requests to the service.

C) You cannot control the amount of request traffic received by a service revision.

D) A revision is created when you update the configuration of a service in Cloud Run.

Respuestas: A, D

2. To integrate a Cloud Run service with other Google Cloud APIs and resources, what are some steps you should take? (Select three)

A) Use the default runtime service account to access Google Cloud APIs and resources from a Cloud Run service.

B) To connect to internal cloud resources from your Cloud Run service, use Serverless VPC Access.

C) Use Secret Manager to store credentials required by downstream database services.

D) Connect to Google Cloud services from your Cloud Run service using client libraries.

Respuestas: B, C, D

3. What are some characteristics of applications that are a good fit for Cloud Run? (Select three)

A) When run as a service, the application listens for HTTP requests on a specified port.

B) The application is containerized.

C) When run as a service, the application responds to a request within a specified time.

D) The application depends on a local persistent file system.

Respuestas: A, B, C

4. What are some products or services that you can use to build containers? (Select three)

A) Cloud Build

B) Docker

C) Artifact Registry

D) Cloud Run

Respuestas: A, B, D (Nota: Cloud Run puede construir desde fuente, por lo que se incluye)

Preguntas Adicionales
5. You need your Cloud Run service to have access to a persistent file system for reading and writing files. What is a key requirement?

A) Using the first-generation execution environment.

B) Mounting a Persistent Disk from Compute Engine.

C) Using the second-generation execution environment and a network file system like Filestore.

D) Writing files directly to a Cloud Storage bucket as if it were a local disk.

Respuesta: C ✅

6. What is the main purpose of creating a "tagged revision" in Cloud Run?

A) To automatically delete the revision after a certain time.

B) To get a unique, stable URL for a specific revision for testing purposes, without sending production traffic to it.

C) To mark a revision as the only one that can be rolled back to.

D) To encrypt the revision's configuration.

Respuesta: B ✅

7. Your Cloud Run service is receiving messages from a Pub/Sub push subscription. If your service fails to process a message and returns an HTTP 500 error, what will Pub/Sub do?

A) Delete the message immediately to prevent further errors.

B) Send the message to a dead-letter queue, if configured.

C) Suspend the push subscription indefinitely.

D) Wait for the acknowledgment deadline and then attempt to redeliver the message.

Respuesta: D ✅ (Nota: Si después de varios reintentos sigue fallando, entonces iría a una dead-letter queue, si está configurada, pero la acción inmediata es el reintento).