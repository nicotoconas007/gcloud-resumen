## Módulo 2 – Event-Driven Applications

### Resumen
Una aplicación orientada a eventos utiliza eventos (hechos inmutables) para comunicar cambios de estado entre servicios desacoplados a través de un intermediario (broker). En Google Cloud, Pub/Sub y Eventarc son componentes clave para EDA.

### Concepto de Evento
- Un evento es un registro de algo que sucedió (ej.: usuario inicia sesión, producto agregado al carrito).
- Inmutable: no se modifica ni elimina; puede existir aunque no haya consumidores.
- Puede persistirse y reproducirse; múltiples consumidores pueden procesarlo en paralelo.

### Problema punto a punto
- En microservicios, el patrón P2P genera acoplamiento fuerte y una red compleja de dependencias.

### Event-Driven Architecture (EDA)
- Productores publican en un broker; consumidores se suscriben y reciben eventos.
- Productores y consumidores no se conocen entre sí (desacoplados).
- Ejemplos en Google Cloud: Pub/Sub (mensajería), Eventarc (routing de eventos de origenes a destinos).

### Beneficios
- Auditoría y trazabilidad (eventos inmutables).
- Seguridad centralizada (authz/authn en el broker).
- Desacoplamiento y extensibilidad: nuevos consumidores sin cambiar productores.
- Resiliencia: asincronía evita bloqueos; recuperación procesando eventos pendientes.
- Eficiencia: push‑based messaging evita polling innecesario.

Referencia: [Module 2 – Event‑Driven Applications](https://storage.googleapis.com/cloud-training/orchestration-and-choreography/en/on-demand/Module2-EventDrivenApplications.pdf)

### Quiz (oficial)
1) When using an event‑driven architecture, which of the following is true about an event?
   - A) An event must always be consumed at least once
   - B) An event should be deleted immediately after it has been consumed
   - C) An event consumer does not need to know which service generated the event
   - D) Producers must know all their consumers in advance
   - Respuesta: C) An event consumer does not need to know which service generated the event

2) Which feature of event‑driven applications makes them more resilient than non‑event‑driven apps?
   - A) Events are created without waiting for a response
   - B) Events cannot be persisted
   - C) Only one service can consume an event
   - D) Polling is preferred over push
   - Respuesta: A) Events are created without waiting for a response

### Preguntas extra (práctica estilo certificación)
3) Which best describes the role of an event intermediary (broker)?
   - A) Stores application state for all services
   - B) Decouples producers and consumers by routing events
   - C) Validates business rules for each service
   - D) Replaces service databases
   - Respuesta: B) Decouples producers and consumers by routing events

4) Why is push‑based messaging more efficient than polling?
   - A) Because consumers periodically request updates
   - B) Because consumers receive updates only when events occur, reducing network I/O
   - C) Because producers buffer all requests
   - D) Because it eliminates authentication
   - Respuesta: B) Because consumers receive updates only when events occur, reducing network I/O

5) What is a benefit of persisting events indefinitely?
   - A) It prevents adding new consumers later
   - B) It allows replay for recovery/debugging and onboarding new consumers
   - C) It reduces storage costs to zero
   - D) It guarantees exactly‑once delivery
   - Respuesta: B) It allows replay for recovery/debugging and onboarding new consumers