## Containers in the Cloud
Este módulo introduce el concepto de contenedores como una forma de empaquetar y ejecutar aplicaciones de manera portable, y Kubernetes como el sistema para orquestar esos contenedores a gran escala.

### ¿Qué son los Contenedores?
Concepto Clave: Un contenedor es un paquete ligero y portable que incluye el código de una aplicación y todas sus dependencias. Virtualiza el sistema operativo, a diferencia de las VMs que virtualizan el hardware.

Beneficios:
- Portabilidad: Se construyen una vez y se ejecutan en cualquier lugar (laptop, staging, producción, diferentes nubes) sin cambios.
- Eficiencia: Son mucho más ligeros que las VMs, por lo que se inician en segundos y se pueden ejecutar muchos en un solo host.
- Escalabilidad: Se pueden duplicar (escalar) rápidamente para manejar más carga.
- Microservicios: Los contenedores son la base de la arquitectura de microservicios, donde una aplicación se divide en componentes pequeños, modulares e independientes que se comunican por red.

### Kubernetes y Google Kubernetes Engine (GKE)
¿Qué es Kubernetes (K8s)?: Es una plataforma de orquestación de contenedores de código abierto. Su trabajo es automatizar el despliegue, escalado y gestión de aplicaciones en contenedores.

### Arquitectura Básica de Kubernetes
- Clúster: Es el conjunto de máquinas que ejecutan Kubernetes. Está compuesto por un Plano de Control (Control Plane) y Nodos (Nodes).
- Plano de Control: Es el "cerebro" del clúster. Toma decisiones, programa los contenedores en los nodos y gestiona el estado del clúster.
- Nodos: Son las máquinas (VMs en GKE) donde realmente se ejecutan los contenedores.

### Objetos Clave de Kubernetes (¡esencial para el examen!)
Pod: Es la unidad de despliegue más pequeña. Encapsula uno o más contenedores. Todos los contenedores dentro de un Pod comparten la misma IP de red y volúmenes de almacenamiento. Generalmente es un contenedor por Pod.

Deployment: Gestiona un conjunto de réplicas de un Pod. Se asegura de que el número deseado de Pods siempre esté en ejecución. Maneja el escalado y las actualizaciones progresivas (rolling updates).

Service: Proporciona un punto de acceso de red estable (una IP y DNS fijos) para un conjunto de Pods. Como los Pods son efímeros y sus IPs cambian, el Service es crucial para que otras aplicaciones o usuarios externos puedan conectarse a ellos de forma fiable.

### Declarativo vs. Imperativo
- Imperativo: Dar órdenes directas (kubectl run, kubectl expose). Útil para aprender y pruebas rápidas.
- Declarativo: Escribir el estado deseado en un archivo de configuración (YAML) y dejar que Kubernetes se encargue de alcanzarlo (kubectl apply -f archivo.yaml). Es la forma recomendada y la más potente de usar Kubernetes.

### ¿Qué es Google Kubernetes Engine (GKE)?
Es el servicio gestionado de Kubernetes en Google Cloud.

Principal ventaja: GKE gestiona el Plano de Control por ti. Tú no tienes que preocuparte por su disponibilidad, actualizaciones o mantenimiento.

### Modos de Operación de GKE
- Standard: Te da control total sobre la configuración de los nodos (tipo de máquina, SO, etc.). Tú gestionas los nodos.
- Autopilot (recomendado): GKE gestiona todo por ti, tanto el plano de control como los nodos. Es un enfoque más "serverless". GKE se encarga de la seguridad, el escalado de nodos y la configuración. Tú solo despliegas tus Pods.

### Quiz (práctica)
1) ¿Cuál es la unidad atómica de programación y despliegue más pequeña en Kubernetes?
   - A) Un Contenedor
   - B) Un Deployment
   - C) Un Pod
   - D) Un Nodo
   - Respuesta: C ✅

2) En Google Kubernetes Engine (GKE), ¿de qué servicio de Google Cloud provienen los recursos (las máquinas virtuales) que forman los nodos del clúster?
   - A) App Engine
   - B) Cloud Storage
   - C) Bare Metal Solution
   - D) Compute Engine
   - Respuesta: D ✅

3) Quieres actualizar tu aplicación a una nueva versión sin tiempo de inactividad, reemplazando gradualmente los Pods antiguos por los nuevos. ¿Qué objeto de Kubernetes gestiona este proceso?
   - A) Un Service
   - B) Un Deployment, a través de una "rolling update".
   - C) Un Pod directamente.
   - D) Un Ingress.
   - Respuesta: B ✅

4) ¿Cuál es la principal ventaja de usar el modo Autopilot en GKE en comparación con el modo Standard?
   - A) Permite usar tipos de máquinas más potentes.
   - B) GKE gestiona la configuración y el escalado de los nodos, reduciendo la carga operativa.
   - C) Es la única forma de usar contenedores de Windows.
   - D) Tiene un costo de cómputo más bajo por hora.
   - Respuesta: B ✅

5) ¿Qué problema resuelve un objeto Service de Kubernetes?
   - A) Asegura que siempre haya un número específico de Pods en ejecución.
   - B) Proporciona un punto de acceso de red estable (IP y DNS fijos) para un conjunto de Pods cuyas IPs individuales son volátiles.
   - C) Define las reglas de firewall para el tráfico entre Pods.
   - D) Construye la imagen del contenedor a partir de un Dockerfile.
   - Respuesta: B ✅

6) ¿Cuál es la diferencia fundamental entre un Contenedor y una Máquina Virtual (VM)?
   - A) Los contenedores solo pueden ejecutar aplicaciones de Linux, mientras que las VMs pueden ejecutar cualquier SO.
   - B) Los contenedores virtualizan el sistema operativo, compartiendo el kernel del host, mientras que las VMs virtualizan el hardware completo.
   - C) Las VMs son más portables que los contenedores.
   - D) No hay una diferencia fundamental, son dos nombres para la misma tecnología.
   - Respuesta: B ✅

7) ¿Cuál es la principal ventaja de GKE sobre Kubernetes autogestionado?
   - A) Mayor control sobre la configuración
   - B) GKE gestiona el Plano de Control automáticamente
   - C) Menor costo de operación
   - D) Mejor rendimiento
   - Respuesta: B ✅

8) ¿Qué enfoque de gestión en Kubernetes es considerado el más recomendado para aplicaciones en producción?
   - A) Imperativo (comandos directos)
   - B) Declarativo (archivos YAML)
   - C) Híbrido (ambos enfoques)
   - D) Automático (sin intervención manual)
   - Respuesta: B ✅

9) ¿Cuántos contenedores típicamente se ejecutan en un Pod de Kubernetes?
   - A) Múltiples contenedores siempre
   - B) Un contenedor por Pod generalmente
   - C) Mínimo 3 contenedores
   - D) Depende del tipo de aplicación
   - Respuesta: B ✅

10) ¿Qué característica comparten todos los contenedores dentro de un mismo Pod?
    - A) La misma imagen de contenedor
    - B) La misma IP de red y volúmenes de almacenamiento
    - C) El mismo puerto de aplicación
    - D) Los mismos recursos de CPU y memoria
    - Respuesta: B ✅

11) ¿Cuál es el propósito principal de un Deployment en Kubernetes?
    - A) Exponer aplicaciones a internet
    - B) Gestionar el estado deseado de un conjunto de Pods réplicas
    - C) Almacenar datos persistentes
    - D) Configurar reglas de red
    - Respuesta: B ✅

12) ¿Qué comando de kubectl se utiliza para aplicar un archivo de configuración YAML?
    - A) kubectl create -f archivo.yaml
    - B) kubectl apply -f archivo.yaml
    - C) kubectl deploy -f archivo.yaml
    - D) kubectl run -f archivo.yaml
    - Respuesta: B ✅

13) ¿Cuál es la principal diferencia entre el modo Standard y Autopilot de GKE?
    - A) Standard es más barato que Autopilot
    - B) Autopilot gestiona automáticamente los nodos, Standard requiere gestión manual
    - C) Standard solo funciona con Linux, Autopilot con Windows
    - D) No hay diferencia significativa
    - Respuesta: B ✅

14) ¿Qué tipo de arquitectura de aplicaciones se beneficia más del uso de contenedores?
    - A) Aplicaciones monolíticas grandes
    - B) Arquitectura de microservicios
    - C) Aplicaciones de escritorio
    - D) Sistemas embebidos
    - Respuesta: B ✅