## Applications in the Cloud
Este módulo se enfoca en las plataformas de computación sin servidor (serverless) de Google Cloud para ejecutar aplicaciones: Cloud Run y Cloud Functions.

### Cloud Run: Contenedores Serverless
¿Qué es?: Una plataforma de computación totalmente gestionada y sin servidor (serverless) que ejecuta contenedores sin estado (stateless).

Concepto Clave: Combina la flexibilidad de los contenedores (puedes empaquetar cualquier aplicación y dependencia) con la simplicidad de una plataforma serverless (no gestionas servidores). Es como "lo mejor de IaaS y PaaS".

### Flujos de Trabajo de Cloud Run
- Basado en Contenedor (Container-based): Tú creas la imagen del contenedor (usando un Dockerfile), la subes a Artifact Registry y la despliegas en Cloud Run.
- Basado en Código Fuente (Source-based): Tú subes tu código fuente directamente y Cloud Run usa Buildpacks para construir la imagen del contenedor por ti y desplegarla. Es el método más rápido y sencillo.
- Portabilidad: Construido sobre Knative (una capa de código abierto sobre Kubernetes), lo que significa que las aplicaciones son portables.

### Modelo de Precios de Cloud Run
- Pagas solo por los recursos (CPU/memoria) mientras tu contenedor está procesando activamente una solicitud, con una granularidad de 100 milisegundos.
- Si no hay tráfico, puede escalar hasta cero, lo que significa que no incurres en costos.
- Caso de uso principal: Ideal para alojar servicios web, APIs REST y microservicios que atienden peticiones HTTP de forma continua.

### Cloud Functions: Funciones Serverless
¿Qué es?: Una plataforma de Función-como-un-Servicio (FaaS). Es una solución ligera y asíncrona para ejecutar pequeñas piezas de código en respuesta a eventos.

Concepto Clave: Es el nivel más alto de abstracción. Tú solo escribes una función de un solo propósito, y Google Cloud se encarga de todo lo demás (servidores, runtime, escalado).

### Triggers (Disparadores) de Cloud Functions
Las funciones se ejecutan en respuesta a:
- Eventos de otros servicios de Google Cloud (ej. subir un archivo a Cloud Storage, recibir un mensaje en Pub/Sub).
- Una petición HTTP directa (para crear un microservicio muy simple).

### Modelo de Precios de Cloud Functions
Similar a Cloud Run, pagas solo mientras tu código se está ejecutando, facturado al milisegundo más cercano.

Caso de uso principal: Perfecto para procesamiento de eventos, tareas de "pegamento" entre servicios (ej. "cuando se suba una imagen, redimensiónala") o para crear webhooks simples.

### Cloud Run vs. Cloud Functions: ¿Cuándo usar cuál?
| Característica | Cloud Run | Cloud Functions |
|---------------|-----------|-----------------|
| Unidad de despliegue | Contenedor | Función (código fuente) |
| Flexibilidad | Muy alta: cualquier lenguaje, binario o dependencia que puedas poner en un contenedor | Alta: soporta lenguajes populares (Node.js, Python, Go, Java, etc.) con sus runtimes gestionados |
| Caso de Uso Principal | Servicios web y APIs completas | Lógica reactiva a eventos, tareas cortas |
| Ejemplo | Alojar un sitio web con React o una API REST completa con múltiples endpoints | Redimensionar una imagen cuando se sube a Cloud Storage |
### Quiz (práctica)
1) Tu aplicación es un servicio web complejo con múltiples endpoints que debe atender peticiones HTTP de forma continua. ¿Qué servicio serverless de Google Cloud es el más adecuado?
   - A) Cloud Functions
   - B) App Engine Standard
   - C) Cloud Run
   - D) Compute Engine
   - Respuesta: C ✅

2) ¿Cuál de las siguientes afirmaciones describe mejor el modelo de precios de Cloud Run?
   - A) Se paga una tarifa fija mensual por cada servicio desplegado.
   - B) Se paga por el tiempo que las instancias están en ejecución, incluso si están inactivas.
   - C) Se paga solo por los recursos de CPU y memoria utilizados mientras el contenedor está procesando activamente solicitudes.
   - D) Es un servicio completamente gratuito.
   - Respuesta: C ✅

3) Necesitas ejecutar una pequeña pieza de código que se active automáticamente cada vez que se publica un nuevo mensaje en un tema de Pub/Sub. ¿Qué servicio es el más eficiente para esta tarea?
   - A) Un clúster de GKE Autopilot.
   - B) Una máquina virtual de Compute Engine.
   - C) Un servicio de Cloud Run.
   - D) Una Cloud Function.
   - Respuesta: D ✅

4) ¿Qué tecnología subyacente permite que las aplicaciones de Cloud Run sean portables?
   - A) Docker Swarm
   - B) Knative
   - C) Apache Mesos
   - D) Kubernetes Engine
   - Respuesta: B ✅

5) ¿Cuál es la granularidad de facturación de Cloud Run?
   - A) Por segundo
   - B) Por minuto
   - C) 100 milisegundos
   - D) Por hora
   - Respuesta: C ✅

6) ¿Qué característica permite que Cloud Run y Cloud Functions escalen automáticamente hasta cero cuando no hay tráfico?
   - A) Auto Scaling
   - B) Serverless
   - C) Load Balancing
   - D) Container Registry
   - Respuesta: B ✅

7) ¿Cuál es la diferencia principal entre Cloud Run Container-based y Source-based?
   - A) Container-based es más barato
   - B) Source-based usa Buildpacks automáticamente
   - C) No hay diferencia
   - D) Source-based solo funciona con Node.js
   - Respuesta: B ✅

8) ¿Qué tipo de triggers puede usar Cloud Functions?
   - A) Solo eventos HTTP
   - B) Solo eventos de Cloud Storage
   - C) Eventos de servicios de Google Cloud y peticiones HTTP
   - D) Solo eventos de Pub/Sub
   - Respuesta: C ✅

9) ¿Cuál es el nivel de abstracción más alto entre Cloud Run y Cloud Functions?
   - A) Cloud Run
   - B) Cloud Functions
   - C) Ambos tienen el mismo nivel
   - D) Depende de la configuración
   - Respuesta: B ✅

10) ¿Qué ventaja principal ofrece el modelo serverless de Google Cloud?
    - A) Mayor control sobre el sistema operativo
    - B) Pago solo por recursos utilizados y gestión automática de infraestructura
    - C) Mejor rendimiento que las VMs
    - D) Acceso directo al hardware
    - Respuesta: B ✅

11) ¿Para qué caso de uso es ideal Cloud Functions?
    - A) Alojar aplicaciones web complejas
    - B) Procesamiento de eventos y tareas de "pegamento" entre servicios
    - C) Almacenamiento de datos
    - D) Gestión de bases de datos
    - Respuesta: B ✅

12) ¿Qué permite que Cloud Run combine lo mejor de IaaS y PaaS?
    - A) Flexibilidad de contenedores con simplicidad serverless
    - B) Uso de máquinas virtuales dedicadas
    - C) Gestión manual de servidores
    - D) Solo soporte para aplicaciones web simples
    - Respuesta: A ✅

13) ¿Cuál es la principal diferencia en la unidad de despliegue entre Cloud Run y Cloud Functions?
    - A) Cloud Run despliega contenedores, Cloud Functions despliega código fuente
    - B) Ambos despliegan contenedores
    - C) Ambos despliegan código fuente
    - D) No hay diferencia
    - Respuesta: A ✅

14) ¿Qué servicio es más adecuado para crear un webhook simple que procese notificaciones HTTP?
    - A) Cloud Run
    - B) Cloud Functions
    - C) Compute Engine
    - D) App Engine
    - Respuesta: B ✅