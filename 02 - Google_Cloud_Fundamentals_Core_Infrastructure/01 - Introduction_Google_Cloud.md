## Google Cloud Fundamentals: Core Infrastructure
Este módulo introduce los conceptos fundamentales de la computación en la nube y cómo Google Cloud implementa su infraestructura global.

### ¿Qué es Cloud Computing?
Definición: Es un modelo de TI con 5 características clave:

Características clave:
- Autoservicio bajo demanda: Obtienes recursos (CPU, almacenamiento) al instante a través de una web, sin intervención humana.
- Acceso amplio a la red: Accedes a los recursos desde cualquier lugar a través de internet.
- Conjunto de recursos: El proveedor tiene un gran "pool" de recursos y los asigna a los clientes, lo que permite economías de escala.
- Elasticidad rápida: Puedes escalar recursos hacia arriba o hacia abajo rápidamente según la demanda.
- Servicio medido: Pagas solo por lo que usas o reservas.

### Modelos de Servicio en la Nube
Infraestructura como Servicio (IaaS):
- Qué es: Te da los "bloques de construcción" básicos de la infraestructura: cómputo (VMs), almacenamiento (discos) y red. Tienes el máximo control.
- Analogía: Comprar los ladrillos y el cemento.
- Ejemplo en Google Cloud: Compute Engine.
- Pago: Pagas por lo que reservas o asignas.

Plataforma como Servicio (PaaS):
- Qué es: El proveedor gestiona la infraestructura subyacente y tú solo te preocupas de desplegar y ejecutar tu código.
- Analogía: Alquilar una casa amueblada; tú solo llevas tu ropa.
- Ejemplo en Google Cloud: App Engine.
- Pago: Pagas por lo que realmente usas.

Software como Servicio (SaaS):
- Qué es: El proveedor te da una aplicación completa y lista para usar. No gestionas nada.
- Analogía: Hospedarte en un hotel.
- Ejemplo de Google: Google Workspace (Gmail, Docs, Drive).

Serverless: Es la evolución de PaaS. Abstrae completamente los servidores. Tú solo subes tu código (funciones) o contenedores. Ejemplos: Cloud Functions, Cloud Run.

### La Red Global de Google Cloud
Estructura jerárquica: La infraestructura física de Google se organiza así:

- Regiones: Son áreas geográficas independientes alrededor del mundo (ej. us-central1, europe-west2).
- Zonas: Son "centros de datos" dentro de una región. Cada región tiene 3 o más zonas. Son dominios de fallo aislados.

Beneficios de esta estructura:
- Usar múltiples ZONAS dentro de una REGIÓN: Principalmente para alta disponibilidad y tolerancia a fallos. Si una zona falla, tu aplicación puede seguir funcionando en las otras zonas de la misma región.
- Usar múltiples REGIONES alrededor del mundo: Principalmente para reducir la latencia para usuarios globales (acercar la aplicación al usuario) y para recuperación ante desastres (si toda una región falla).
- Multi-región: Algunos servicios (como Cloud Storage o Spanner) pueden replicar datos automáticamente a través de múltiples regiones para máxima disponibilidad y baja latencia de lectura global.

### Principios Clave de Google Cloud
Seguridad: Es una responsabilidad compartida, pero Google protege la infraestructura "de la nube" con múltiples capas: seguridad física en los data centers, hardware personalizado (chips Titan), cifrado de datos en tránsito y en reposo por defecto.

Enfoque Abierto: Google promueve el código abierto para evitar el "vendor lock-in" (quedar atado a un proveedor).

Proyectos de código abierto:
- Kubernetes: Creado por Google y donado a la comunidad. GKE es la versión gestionada.
- TensorFlow: Librería de Machine Learning de código abierto.

### Precios y Facturación
Facturación por segundo: En servicios IaaS como Compute Engine y GKE.

Descuentos por uso continuo (Sustained-use discounts): Descuentos automáticos en Compute Engine si una VM corre más del 25% del mes.

Herramientas de control de costos: Presupuestos (Budgets) y Alertas (Alerts) para monitorear el gasto.

Cuotas (Quotas): Límites a nivel de proyecto para prevenir el consumo excesivo de recursos, ya sea por error o por un ataque. Hay de dos tipos:
- De Tasa (Rate): ej. N° de llamadas a una API por minuto
- De Asignación (Allocation): ej. N° de VMs que puedes crear

### Quiz (práctica)
1) ¿Cuál es el principal beneficio de desplegar una aplicación en múltiples zonas dentro de una misma región de Google Cloud?
   - A) Reducir la latencia para usuarios en otras partes del mundo.
   - B) Cumplir con los requisitos de residencia de datos.
   - C) Mejorar la tolerancia a fallos y la alta disponibilidad.
   - D) Obtener descuentos en los precios de cómputo.
   - Respuesta: C ✅

2) ¿Qué modelo de servicio en la nube te permite enfocarte únicamente en tu código y sus dependencias, mientras el proveedor gestiona toda la infraestructura subyacente, el sistema operativo y el runtime?
   - A) Infraestructura como Servicio (IaaS)
   - B) Software como Servicio (SaaS)
   - C) Plataforma como Servicio (PaaS)
   - D) Colocación (Colocation)
   - Respuesta: C ✅

3) Tu aplicación necesita servir a usuarios en Europa y Asia con la menor latencia posible. ¿Cuál sería la mejor estrategia de despliegue en Google Cloud?
   - A) Desplegar la aplicación en múltiples zonas dentro de una sola región en Europa.
   - B) Desplegar la aplicación en una región en Europa y en otra región en Asia.
   - C) Usar un solo clúster de GKE en una región de EE. UU.
   - D) Usar un servicio multi-regional como Cloud Spanner.
   - Respuesta: B ✅

4) ¿Cuál de las siguientes es una característica clave del cloud computing según el modelo NIST?
   - A) Servicios gestionados por terceros
   - B) Autoservicio bajo demanda
   - C) Infraestructura física dedicada
   - D) Contratos de servicio a largo plazo
   - Respuesta: B ✅

5) ¿Qué modelo de servicio en la nube proporciona el máximo control sobre la infraestructura?
   - A) Software como Servicio (SaaS)
   - B) Plataforma como Servicio (PaaS)
   - C) Infraestructura como Servicio (IaaS)
   - D) Backend como Servicio (BaaS)
   - Respuesta: C ✅

6) ¿Cuál es un ejemplo de Software como Servicio (SaaS) de Google?
   - A) Compute Engine
   - B) App Engine
   - C) Google Workspace (Gmail, Docs)
   - D) Cloud Functions
   - Respuesta: C ✅

7) ¿Qué tipo de cuota limita el número de llamadas a una API por minuto?
   - A) Cuota de asignación (Allocation)
   - B) Cuota de tasa (Rate)
   - C) Cuota de almacenamiento
   - D) Cuota de red
   - Respuesta: B ✅

8) ¿Cuál es el principal beneficio de usar servicios multi-regionales como Cloud Storage?
   - A) Menor costo de almacenamiento
   - B) Mayor control sobre los datos
   - C) Máxima disponibilidad y baja latencia de lectura global
   - D) Menor complejidad de configuración
   - Respuesta: C ✅

9) ¿Qué herramienta de Google Cloud ayuda a monitorear y controlar los costos?
   - A) Cloud Monitoring
   - B) Cloud Logging
   - C) Presupuestos (Budgets) y Alertas (Alerts)
   - D) Cloud Trace
   - Respuesta: C ✅

10) ¿Cuál es el enfoque de Google Cloud hacia el código abierto?
    - A) Evita el código abierto para proteger la propiedad intelectual
    - B) Promueve el código abierto para evitar vendor lock-in
    - C) Solo utiliza código abierto para servicios básicos
    - D) Requiere licencias propietarias para todos los servicios
    - Respuesta: B ✅

11) ¿Qué son las zonas en la arquitectura de Google Cloud?
    - A) Áreas geográficas independientes alrededor del mundo
    - B) Centros de datos dentro de una región que son dominios de fallo aislados
    - C) Servicios gestionados por Google
    - D) Herramientas de desarrollo
    - Respuesta: B ✅

12) ¿Qué descuento automático aplica Google Cloud a las VMs de Compute Engine?
    - A) Descuentos por compromiso (Committed use discounts)
    - B) Descuentos por uso continuo (Sustained-use discounts)
    - C) Descuentos por volumen
    - D) Descuentos por prepago
    - Respuesta: B ✅