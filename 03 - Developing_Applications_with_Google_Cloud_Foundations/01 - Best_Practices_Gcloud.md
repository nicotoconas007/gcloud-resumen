## Módulo 1 – Best Practices for Cloud Application Development

### Resumen
Este módulo presenta las mejores prácticas para desarrollar aplicaciones en Google Cloud. Puntos clave:
- Global Reach, Escalabilidad y Alta Disponibilidad: diseñar apps responsivas, disponibles y con escalado elástico.
- Seguridad: aplicar buenas prácticas y cumplir regulaciones (p.ej., aislamiento de datos por región).
- Gestión de Código: usar control de versiones; no incluir binarios; declarar dependencias explícitamente.
- Configuración separada del código: variables de entorno en lugar de valores hardcodeados.
- Arquitectura: preferir microservicios frente a monolitos para despliegue y escalado independientes.
- Operaciones asíncronas: minimizar trabajo en el hilo del usuario; usar Pub/Sub, Eventarc, colas.
- Componentes stateless: no guardar estado local; persistir en bases de datos externas.
- Resiliencia: reintentos con backoff exponencial, circuit breakers y degradación elegante.
- Caching y CDN: usar Memorystore (Redis/Memcached) y Cloud CDN para bajar latencia.
- APIs y Gateways: exponer funcionalidades mediante APIs modernas (p.ej., Apigee) y conectar con legacy.
- Autenticación: delegar identidad a Identity Platform o proveedores externos (Google, GitHub, etc.).
- Observabilidad: logs como streams, Cloud Logging, métricas basadas en logs y trazas distribuidas.
- DevOps y CI/CD: pipelines con Cloud Build, Artifact Registry y Cloud Deploy; blue/green o canary.
- Modernización con Strangler Pattern: reemplazar gradualmente componentes de sistemas heredados.

### Quiz de práctica
1) Which of the following is an anti-pattern when designing a cloud application?
   - A) Cache application data and frontend content
   - B) Perform asynchronous operations
   - C) Embed configuration settings in your source code
   - D) Use APIs and API gateways to connect to legacy systems in applications
   - Respuesta: C) Embed configuration settings in your source code

2) For transient network issues, what error-handling approach should you implement?
   - A) Retry constantly until the call succeeds
   - B) Implement a circuit breaker
   - C) Display the error to the user
   - D) Retry with exponential backoff
   - Respuesta: D) Retry with exponential backoff

3) What is one advantage of using microservices instead of a monolithic architecture?
   - A) All components must be deployed together
   - B) Code changes are harder to identify
   - C) Each service can be scaled independently
   - D) Dependencies are tightly coupled
   - Respuesta: C) Each service can be scaled independently

4) What is the benefit of separating configuration from code using environment variables?
   - A) Makes the application slower but safer
   - B) Ensures the same code works across dev, test, and prod environments
   - C) Requires storing configs as constants
   - D) Eliminates the need for dependency managers
   - Respuesta: B) Ensures the same code works across dev, test, and prod environments

5) Which Google Cloud service provides a fully managed in-memory cache using Redis or Memcached?
   - A) Cloud Storage
   - B) Memorystore
   - C) Cloud CDN
   - D) Cloud Logging
   - Respuesta: B) Memorystore

6) Which deployment strategy minimizes risk by rolling out new builds to a small percentage of users first?
   - A) Blue/Green Deployment
   - B) Canary Deployment
   - C) Strangler Pattern
   - D) Rolling Restart
   - Respuesta: B) Canary Deployment