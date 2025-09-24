## Módulo 3 – Orchestration and Choreography

### Resumen
Patrones para coordinar microservicios: coreografía (servicios independientes coordinados por eventos) y orquestación (orquestador central que dirige el flujo). En Google Cloud: coreografía con Pub/Sub y Eventarc (CloudEvents); orquestación con Workflows. Cloud Tasks y Cloud Scheduler complementan diseños asincrónicos.

### Service Choreography
- Servicios independientes que reciben/envían eventos en forma asincrónica siguiendo reglas acordadas y contratos de eventos.
- Desacoplado y escalable por servicio; lógica de negocio distribuida más difícil de rastrear.
- En Google Cloud: Pub/Sub (mensajería tiempo real) y Eventarc (eventing administrado con triggers y CloudEvents).

### Service Orchestration
- Orquestador central controla pasos del proceso; servicios no se conocen entre sí.
- Beneficios: visión unificada, observabilidad, manejo de errores, reintentos y procesos largos.
- Desafío: punto único de falla en el orquestador.
- En Google Cloud: Workflows.

### Ejemplo con Workflows
- Flujo de pedido: verificar inventario (Firestore) → invocar servicios en Cloud Run → actualizar inventario → enviar email/notificar Slack. Ejecuciones quedan registradas para inspección.

### Comparación y usos
- Coreografía: ideal para servicios descentralizados, equipos distintos, o cuando se aprovechan eventos de GCP/terceros.
- Orquestación: ideal para procesos complejos con visibilidad y control centralizado; aporta confiabilidad.
- Patrón combinado: Workflows para el proceso y Eventarc para disparadores/eventos entre servicios.

### Servicios de soporte
- Cloud Tasks: colas de tareas HTTP con scheduling, reintentos, rate limiting; control explícito del destino; entrega al menos‑una‑vez; puede adjuntar tokens (OIDC/OAuth) del service account.
- Cloud Scheduler: cron administrado (UNIX‑cron), dispara Pub/Sub, App Engine o HTTP; recomendado UTC.

Referencia: [Module 3 – Choreography and Orchestration](https://storage.googleapis.com/cloud-training/orchestration-and-choreography/en/on-demand/Module3-ChoreographyAndOrchestration.pdf)

### Quiz (oficial)
1) Which of the following are features of Eventarc? (Select two)
   - A) Pub/Sub is the transport layer
   - B) Eventarc can generate events from Cloud Audit Logs entries
   - C) Applications must poll an event queue to handle events
   - D) Event formats are arbitrary per source
   - Respuestas: A, B

2) Which of the following are features of Cloud Tasks? (Select two)
   - A) Tasks can be scheduled for delivery at a future time
   - B) HTTP destinations may include tokens attached for the queue's service account
   - C) At‑least‑once delivery is guaranteed
   - D) The creator has no control over which endpoint receives the task
   - Respuestas: A, B, C (todas verdaderas salvo D)

3) Which of the following are features of Workflows? (Select two)
   - A) Supports long‑running processes
   - B) Execution state is observable
   - C) Appropriate only for simple processes
   - D) Provides a decentralized view of events
   - Respuestas: A, B

4) Which of the following are benefits of service choreography? (Select two)
   - A) Decentralized control
   - B) Loosely coupled services
   - C) Business logic is easier to understand centrally
   - D) Producers keep full downstream control
   - Respuestas: A, B

### Preguntas extra (práctica)
5) What is a limitation of service orchestration?
   - A) Requires polling across services
   - B) Introduces a single point of failure at the orchestrator
   - C) Prevents retries
   - D) Cannot show process state
   - Respuesta: B) Introduces a single point of failure at the orchestrator

6) Which service standardizes event format using CloudEvents?
   - A) Pub/Sub
   - B) Eventarc
   - C) Workflows
   - D) Cloud Tasks
   - Respuesta: B) Eventarc

7) What is the main difference between Cloud Tasks and Pub/Sub?
   - A) Both are implicit invocation
   - B) Cloud Tasks is explicit invocation (control of destination); Pub/Sub is implicit (publish‑subscribe)
   - C) Both guarantee exactly‑once delivery
   - D) Pub/Sub requires specifying a single endpoint per message
   - Respuesta: B) Cloud Tasks explicit; Pub/Sub implicit