## Virtual Machines and Networks in the Cloud
Este módulo cubre los componentes fundamentales de la infraestructura IaaS en Google Cloud: Compute Engine para las máquinas virtuales y VPC para la red.

### Virtual Private Cloud (VPC)
¿Qué es?: Es tu propia red privada y aislada dentro de la nube pública de Google. Es la base sobre la que se construyen y comunican los recursos.

Alcance Global: Una característica clave de la VPC de Google es que es un recurso global. No está atada a una sola región.

### Subredes (Subnets)
- Una VPC se divide en subredes. A diferencia de la VPC, cada subred es un recurso regional.
- Una subred puede extenderse a todas las zonas dentro de su región. Esto significa que dos VMs en diferentes zonas (para alta disponibilidad) pueden estar en la misma subred y comunicarse con IPs privadas como si estuvieran lado a lado.

### Componentes Integrados de VPC
Rutas (Routes): Cada VPC tiene una tabla de rutas implícita que gestiona el tráfico entre subredes y hacia internet. No necesitas configurar un router virtual.

Reglas de Firewall (Firewall Rules): La VPC incluye un firewall distribuido y con estado. Las reglas controlan el tráfico entrante (ingress) y saliente (egress). Se pueden aplicar a VMs específicas usando etiquetas de red (network tags).

### Compute Engine (IaaS)
¿Qué es?: Es el servicio de Google Cloud para crear y gestionar máquinas virtuales (VMs). Es el principal componente de IaaS.

Flexibilidad: Permite usar imágenes de SO predefinidas (Linux, Windows), imágenes personalizadas o soluciones listas para usar del Cloud Marketplace.

### Modelo de Precios y Descuentos (¡importante!)
- Facturación por segundo: Con un mínimo de 1 minuto.
- Descuentos por uso continuo (Sustained-use discounts): Descuentos automáticos si una VM corre más del 25% del mes.
- Descuentos por compromiso de uso (Committed-use discounts): Descuentos significativos (hasta 57%) si te comprometes a usar una cierta cantidad de vCPU y memoria por 1 o 3 años. Ideal para cargas de trabajo predecibles.
- VMs Spot (antes Preemptible): VMs con un descuento de hasta el 90%, pero que Google puede detener en cualquier momento si necesita los recursos. Son ideales para cargas de trabajo tolerantes a fallos y sin estado, como trabajos de procesamiento por lotes.

### Almacenamiento en Compute Engine
- Persistent Disk: El almacenamiento en bloque más común, como un disco duro de red. Puede ser Zonal o Regional (para alta disponibilidad).
- Local SSD: Almacenamiento de muy alto rendimiento, pero efímero (los datos se pierden si la VM se detiene).

### Autoescalado (Autoscaling)
Permite añadir o quitar VMs de un grupo de instancias gestionado (Managed Instance Group o MIG) automáticamente, basándose en métricas como el uso de CPU.

### Balanceo de Carga y Entrega de Contenido
Cloud Load Balancing:
- Es un servicio gestionado, distribuido y definido por software. No tienes que gestionar VMs para el balanceador.
- Balanceador de Carga de Aplicación (Application Load Balancer): Opera en la Capa 7 (HTTP/HTTPS). Es ideal para tráfico web. Puede ser global (con una sola IP anycast para todo el mundo) o regional.
- Balanceador de Carga de Red (Network Load Balancer): Opera en la Capa 4 (TCP/UDP). Ideal para tráfico no HTTP o cuando se necesita preservar la IP original del cliente.

Cloud DNS: Servicio de DNS gestionado, programable y de alta disponibilidad para resolver los nombres de dominio de tus aplicaciones.

### Cloud CDN (Content Delivery Network)
- Almacena en caché el contenido (imágenes, videos, etc.) en los puntos de presencia (PoPs) de Google alrededor del mundo, más cerca de tus usuarios.
- Beneficios: Reduce la latencia, disminuye la carga en tus servidores de origen y ahorra costos de salida de datos.
- Se habilita con una sola casilla de verificación en un Application Load Balancer.

### Conexión de Redes a la VPC
Cloud VPN: Crea un túnel IPsec seguro a través de internet para conectar tu red local (on-premises) con tu VPC.

Cloud Interconnect:
- Interconexión dedicada (Dedicated Interconnect): Una conexión física y privada directa entre tu centro de datos y la red de Google. Ofrece el máximo rendimiento, fiabilidad y seguridad. Cubierta por un SLA.
- Interconexión de socio (Partner Interconnect): Usa la red de un socio de Google para conectarte. Es más flexible si no puedes llegar a una ubicación de interconexión dedicada.
- Peering: Conecta tu red directamente a la red de Google en un punto de presencia. Direct Peering no está cubierto por un SLA.

### Quiz (práctica)
1) ¿Cuál es el alcance de una VPC de Google Cloud y el de una de sus subredes, respectivamente?
   - A) Regional, Zonal
   - B) Global, Regional
   - C) Zonal, Global
   - D) Regional, Global
   - Respuesta: B ✅

2) Tienes una carga de trabajo de análisis de datos que puede ser interrumpida y reiniciada sin perder el trabajo. Para optimizar costos, ¿qué tipo de VM de Compute Engine deberías usar?
   - A) Una VM con descuento por compromiso de uso.
   - B) Una VM con un tipo de máquina personalizado.
   - C) Una VM Spot.
   - D) Una VM con un disco persistente regional.
   - Respuesta: C ✅

3) ¿Qué servicio de Google Cloud se utiliza para distribuir tráfico HTTP/S a nivel global con una única dirección IP anycast?
   - A) Balanceador de Carga de Red (Network Load Balancer)
   - B) Cloud CDN
   - C) Balanceador de Carga de Aplicación Externo Global (Global External Application Load Balancer)
   - D) Cloud DNS
   - Respuesta: C ✅

4) ¿Cómo se aplican las reglas de firewall en una VPC de Google Cloud de manera eficiente a un grupo de VMs que cumplen una misma función, como ser servidores web?
   - A) Creando una regla para la dirección IP de cada VM.
   - B) Aplicando una etiqueta de red (network tag) a las VMs y creando una regla de firewall que apunte a esa etiqueta.
   - C) Creando una subred separada para cada VM.
   - D) Usando Cloud VPN para controlar el tráfico.
   - Respuesta: B ✅

5) ¿Qué opción de conectividad ofrece una conexión física, privada y de alta fiabilidad entre tu centro de datos y la red de Google, y además está cubierta por un SLA?
   - A) Direct Peering
   - B) Cloud VPN
   - C) Dedicated Interconnect
   - D) Cloud CDN
   - Respuesta: C ✅

6) ¿Cuál es la principal diferencia entre Persistent Disk y Local SSD en Compute Engine?
   - A) Persistent Disk es más rápido que Local SSD
   - B) Local SSD es persistente, Persistent Disk es efímero
   - C) Persistent Disk es persistente, Local SSD es efímero y de alto rendimiento
   - D) No hay diferencia entre ambos tipos de almacenamiento
   - Respuesta: C ✅

7) ¿Qué capa del modelo OSI opera el Balanceador de Carga de Red (Network Load Balancer)?
   - A) Capa 3 (Red)
   - B) Capa 4 (Transporte)
   - C) Capa 7 (Aplicación)
   - D) Capa 2 (Enlace de datos)
   - Respuesta: B ✅

8) ¿Cuál es el descuento máximo que puedes obtener con VMs Spot (Preemptible) en Compute Engine?
   - A) 25%
   - B) 57%
   - C) 90%
   - D) 100%
   - Respuesta: C ✅

9) ¿Qué servicio de Google Cloud se utiliza para habilitar CDN con una sola casilla de verificación?
   - A) Cloud DNS
   - B) Cloud Load Balancing
   - C) Application Load Balancer
   - D) Network Load Balancer
   - Respuesta: C ✅

10) ¿Qué tipo de descuento en Compute Engine se aplica automáticamente si una VM corre más del 25% del mes?
    - A) Descuentos por compromiso de uso (Committed-use discounts)
    - B) Descuentos por uso continuo (Sustained-use discounts)
    - C) Descuentos por volumen
    - D) Descuentos por prepago
    - Respuesta: B ✅

11) ¿Cuál es la principal ventaja de usar Cloud Interconnect sobre Cloud VPN?
    - A) Mayor seguridad
    - B) Menor costo
    - C) Mayor ancho de banda y menor latencia
    - D) Más fácil de configurar
    - Respuesta: C ✅

12) ¿Qué componente de VPC gestiona automáticamente el tráfico entre subredes sin necesidad de configurar un router virtual?
    - A) Reglas de Firewall
    - B) Tabla de rutas implícita
    - C) Cloud VPN
    - D) Cloud Interconnect
    - Respuesta: B ✅