## Módulo 1 – Introduction to Microservices

### Resumen
Evolución de monolitos → SOA (con ESB) → microservicios. Microservicios son servicios pequeños y autónomos, cada uno con su lógica y base de datos, que se comunican vía APIs. Beneficios: desacoplamiento, escalado independiente, flexibilidad tecnológica y despliegues autónomos. Desafíos: mayor complejidad operativa, latencia en red, pruebas de integración y trazabilidad.

### Contexto y evolución
- Monolitos: app única con UI, lógica y datos; fuerte acoplamiento; difícil de escalar y mantener.
- SOA + ESB: servicios reutilizables con bus central (mensajería, seguridad, transformaciones). Beneficios de estandarización, pero ESB como cuello de botella y punto de falla.
- Microservicios: servicios pequeños, autónomos; cada uno con su base de datos y API.

### Beneficios
- Código más simple por servicio; equipos pequeños y dueños claros.
- Testing más claro por límites definidos; despliegues independientes → iteración rápida.
- Heterogeneidad tecnológica por servicio; escalado granular según carga.

### Desafíos
- Operación compleja: requiere CI/CD, observabilidad y automatización fuerte.
- Comunicación distribuida: mayor latencia que llamadas internas; fallos parciales.
- Testing de integración y trazabilidad (logs/traces) más exigentes.

### Buenas prácticas iniciales
- Si el conocimiento del dominio es limitado, empezar con monolito modular y migrar luego.
- Si agilidad/escalabilidad son críticas desde el día 1, considerar microservicios.
- Definir fronteras de servicio (bounded contexts) con cuidado desde el inicio.

Referencia: [Module 1 – Introduction to Microservices](https://storage.googleapis.com/cloud-training/orchestration-and-choreography/en/on-demand/Module1-IntroductionToMicroservices.pdf)

### Quiz (oficial)
1) In which situation does it make sense to start as a monolithic application instead of microservices?
   - A) Your team does not have expertise in the problem domain
   - B) Agile service delivery is a priority
   - C) You plan to grow the team
   - D) You need polyglot stacks from day one
   - Respuesta: A) Your team does not have expertise in the problem domain

2) Which of the following is a benefit of a microservices architecture?
   - A) Improved network latency vs monoliths
   - B) Simpler communication patterns
   - C) Separately deployable services
   - D) Single shared database for all services
   - Respuesta: C) Separately deployable services

### Preguntas extra (práctica estilo certificación)
3) What was the main bottleneck of SOA architectures with ESB?
   - A) Lack of service reuse
   - B) Centralized integration dependencies and upgrade bottlenecks
   - C) Inability to secure messages
   - D) No support for transformations
   - Respuesta: B) Centralized integration dependencies and upgrade bottlenecks

4) Which is a key challenge of microservices?
   - A) Reduced operational burden
   - B) Easier end‑to‑end testing
   - C) Increased operational burden with many deployable services
   - D) Simpler distributed tracing
   - Respuesta: C) Increased operational burden with many deployable services

5) Why do microservices enable teams to use different programming languages?
   - A) Because they share a single codebase
   - B) Because communication is via APIs decoupled from implementation details
   - C) Because all services use the same framework
   - D) Because the ESB enforces language choice
   - Respuesta: B) Because communication is via APIs decoupled from implementation details