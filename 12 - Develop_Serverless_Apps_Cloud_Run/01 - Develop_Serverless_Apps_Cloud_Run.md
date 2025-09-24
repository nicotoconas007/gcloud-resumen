## Develop Serverless Applications on Cloud Run
Este módulo se enfoca en patrones de arquitectura avanzados y casos de uso prácticos para Cloud Run, demostrando cómo construir sistemas robustos y escalables.

### Arquitectura Orientada a Eventos (Ej: Conversor de PDF)
Concepto Clave: Un servicio de Cloud Run se activa en respuesta a un evento en otro servicio de Google Cloud, sin que el servicio de origen sepa quién lo consume.

Flujo Típico:
- Un archivo se sube a un bucket de Cloud Storage.
- Cloud Storage emite una notificación de evento a un tema de Pub/Sub (configurado con gsutil notification create).
- Se crea una suscripción de tipo push a ese tema de Pub/Sub.
- Esta suscripción tiene como endpoint la URL de un servicio de Cloud Run.
- Cuando llega un mensaje, Pub/Sub invoca al servicio de Cloud Run enviándole una petición HTTP POST con los detalles del evento.

Seguridad: El servicio de Cloud Run se despliega como privado (--no-allow-unauthenticated). Para permitir que Pub/Sub lo invoque, se crea una cuenta de servicio dedicada (ej. pubsub-cloud-run-invoker) y se le otorga el rol roles/run.invoker en el servicio de Cloud Run. La suscripción push se configura para usar esta cuenta de servicio.

Dependencias del Contenedor: Si la aplicación necesita software a nivel de sistema operativo (como libreoffice), se debe instalar en el Dockerfile usando comandos como RUN apt-get update && apt-get install -y ....

### Microservicios Resilientes y Asíncronos
Concepto Clave: Desacoplar servicios para que la falla de uno no afecte al resto del sistema. La comunicación entre ellos se hace de forma asíncrona a través de un intermediario como Pub/Sub.

Flujo Típico:
- Un servicio "productor" (ej. api-gateway) recibe una petición y, en lugar de procesarla, publica un mensaje en un tema de Pub/Sub. Responde inmediatamente al cliente (204 No Content) para indicar que la tarea fue aceptada.
- Uno o más servicios "consumidores" (ej. email-service, sms-service) están suscritos a ese tema.
- Pub/Sub entrega el mensaje a todos los suscriptores para que cada uno realice su tarea de forma independiente.

Resiliencia (¡muy importante para el examen!):
- Si un servicio consumidor falla y devuelve un error (HTTP 500), Pub/Sub NO descarta el mensaje. Lo retendrá y reintentará la entrega automáticamente por un período configurable.
- Mientras tanto, los otros servicios consumidores que sí funcionan procesan el mensaje sin problemas.
- Una vez que el servicio que fallaba se arregla y se redespliega, Pub/Sub le entregará los mensajes pendientes que no pudo procesar. No se pierden datos.
- Un servicio confirma el procesamiento exitoso devolviendo un código HTTP 2xx a Pub/Sub.

### APIs REST y Comunicación Segura entre Servicios
Concepto Clave: Crear servicios de backend privados que solo pueden ser accedidos por otros servicios autorizados (ej. un frontend), pero no directamente desde internet.

Flujo Típico:
- Se despliega un servicio de backend (ej. billing-api) como privado (--no-allow-unauthenticated). Este servicio se conecta a una base de datos como Firestore.
- Se despliega un servicio de frontend como público (--allow-unauthenticated).

Para permitir que el frontend llame al backend, se sigue este patrón de seguridad:
- Se crea una cuenta de servicio dedicada para el frontend (ej. frontend-invoker-sa).
- Se le otorga el rol roles/run.invoker a frontend-invoker-sa sobre el servicio de backend billing-api.
- El servicio de frontend se despliega asociado a su cuenta de servicio (--service-account=...).
- Las librerías cliente de Google en el código del frontend usarán automáticamente esta identidad para obtener un token y hacer llamadas autenticadas al backend.

### Quiz (práctica)
1) En una arquitectura de microservicios que usa Pub/Sub, el email-service falla y devuelve un código HTTP 500, mientras que el sms-service funciona correctamente. ¿Qué sucede con el mensaje enviado por el productor?
   - A) El mensaje se descarta para ambos servicios para evitar inconsistencias.
   - B) El sms-service procesa el mensaje, y Pub/Sub reintentará la entrega al email-service más tarde.
   - C) Ambos servicios dejan de recibir mensajes hasta que el email-service se repare.
   - D) El productor recibe un error y debe reintentar el envío del mensaje a ambos servicios.
   - Respuesta: B ✅

2) Quieres que un servicio de Cloud Run se active automáticamente cada vez que se sube una imagen a un bucket de Cloud Storage. ¿Cuál es la secuencia correcta de componentes para lograr esto?
   - A) Cloud Storage -> Llamada HTTP directa -> Cloud Run
   - B) Cloud Storage -> Notificación de Evento -> Tema de Pub/Sub -> Suscripción Push -> Cloud Run
   - C) Cloud Run -> Monitorea el bucket de Cloud Storage -> Procesa el archivo
   - D) Cloud Storage -> Cloud Function -> Cloud Run
   - Respuesta: B ✅

3) Tu servicio frontend (público) necesita llamar a tu servicio backend-api (privado). ¿Qué configuración de IAM es la correcta?
   - A) Otorgar el rol roles/run.invoker a allUsers en el servicio backend-api.
   - B) Crear una cuenta de servicio para frontend, asociarla a él y otorgarle el rol roles/run.invoker en backend-api.
   - C) Crear una API Key y pasarla en las cabeceras de la petición desde el frontend.
   - D) Ambos servicios deben ejecutarse con la cuenta de servicio por defecto.
   - Respuesta: B ✅

4) ¿Qué comando de gcloud se utiliza para configurar las notificaciones de eventos de Cloud Storage a Pub/Sub?
   - A) gcloud storage notifications create
   - B) gsutil notification create
   - C) gcloud pubsub topics create-notification
   - D) gcloud storage events create
   - Respuesta: B ✅

5) En una arquitectura orientada a eventos con Pub/Sub y Cloud Run, ¿qué tipo de suscripción de Pub/Sub se utiliza para invocar directamente un servicio de Cloud Run?
   - A) Pull subscription
   - B) Push subscription
   - C) Batch subscription
   - D) Streaming subscription
   - Respuesta: B ✅

6) ¿Qué código de respuesta HTTP debe devolver un servicio de Cloud Run que recibe un mensaje de Pub/Sub para confirmar que procesó exitosamente el mensaje?
   - A) HTTP 200
   - B) HTTP 204
   - C) Cualquier código 2xx
   - D) HTTP 201
   - Respuesta: C ✅

7) ¿Qué sucede si un servicio de Cloud Run que recibe mensajes de Pub/Sub devuelve un código HTTP 4xx o 5xx?
   - A) El mensaje se descarta inmediatamente
   - B) Pub/Sub reintentará la entrega del mensaje automáticamente
   - C) Se envía el mensaje a una dead-letter queue
   - D) Se pausa toda la suscripción
   - Respuesta: B ✅

8) Para que un servicio de Cloud Run privado pueda ser invocado por Pub/Sub, ¿qué rol de IAM se debe otorgar a la cuenta de servicio de Pub/Sub?
   - A) roles/run.developer
   - B) roles/run.invoker
   - C) roles/run.admin
   - D) roles/pubsub.subscriber
   - Respuesta: B ✅

9) En el patrón de comunicación segura entre servicios, ¿qué librerías se utilizan en el frontend para hacer llamadas autenticadas al backend?
   - A) Librerías cliente de Google Cloud
   - B) Librerías de autenticación de terceros
   - C) Librerías HTTP estándar
   - D) Librerías de Firebase
   - Respuesta: A ✅

10) ¿Cuál es la principal ventaja de usar una arquitectura asíncrona con Pub/Sub en lugar de comunicación síncrona entre servicios?
    - A) Mayor velocidad de procesamiento
    - B) Menor uso de memoria
    - C) Mejor resiliencia y desacoplamiento
    - D) Menor costo de infraestructura
    - Respuesta: C ✅